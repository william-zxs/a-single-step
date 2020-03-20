```shell
#!/bin/bash

h1=192.168.10.210
h2=192.168.10.211
pass=123456
user=root
port=3306
temp=/tmp/dbstatus

mysql -u$user -p$pass -P $port -h $h1 > $temp <<EOF
show master status
EOF
st=`tail -n 1 /tmp/dbstatus`
binlog=`echo $st | cut -d' ' -f 1`
pos=`echo $st | cut -d' ' -f 2`

echo change  master to master_host="$h1",master_port=$port, master_user="$user",master_password="$pass",master_log_file="$binlog",master_log_pos=$pos

mysql -u$user -p$pass -P $port -h $h2  <<EOF
change  master to master_host="$h1",master_port=$port, master_user="$user",master_password="$pass",master_log_file="$binlog",master_log_pos=$pos;
start slave
EOF


mysql -u$user -p$pass -P $port -h $h2 >> $temp <<EOF
show master status
EOF

st=`tail -n 1 /tmp/dbstatus`
binlog=`echo $st | cut -d' ' -f 1`
pos=`echo $st | cut -d' ' -f 2`

echo change  master to master_host="$h2",master_port=$port, master_user="$user",master_password="$pass",master_log_file="$binlog",master_log_pos=$pos

mysql -u$user -p$pass -P $port -h $h1  <<EOF
change  master to master_host="$h2",master_port=$port, master_user="$user",master_password="$pass",master_log_file="$binlog",master_log_pos=$pos;
start slave
EOF
```

