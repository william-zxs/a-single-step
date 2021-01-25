

# micrometer

```
index_cost.record(() -> {
    try {
        my_time();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
});
```

**判断是否为空**
```
ObjectUtils.isEmpty(order)
```


