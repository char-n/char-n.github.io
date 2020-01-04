# mybatis使用笔记

[TOC]
1. mybatis and 和or连用

   ```java
   queryWrapper.and(wrapper->wrapper.in(User::getId,userIds).or().eq(User::getName,userName));
   ```

