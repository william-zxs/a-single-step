

#micrometer

```
index_cost.record(() -> {
    try {
        my_time();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
});
```

