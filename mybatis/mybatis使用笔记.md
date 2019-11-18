# mybatis使用笔记

[TOC]
1. 启动报lambda错误

```java
Error parsing property name 'lambda$18'. Didn't start with 'is', 'get' or 's
```

 解决方式

```java
 List<Test> test = this.list(queryWrapper); //使用this
```



