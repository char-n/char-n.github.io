## activiti学习笔记

[TOC]

### 1.主键重复问题

背景：

```xml
在生产环境上部署的项目，某一天发现执行的办理任务的时候报错，报错内容如下：
org.apache.ibatis.exceptions.PersistenceException: 
### Error updating database.  Cause: com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '90093' for key 'PRIMARY'
```

解决方案：

```java
import org.activiti.engine.impl.history.HistoryLevel;
import org.activiti.spring.SpringProcessEngineConfiguration;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.transaction.PlatformTransactionManager;
import javax.sql.DataSource;

@Configuration
public class ActivitiConfig {
    @Autowired
    PlatformTransactionManager transactionManager;
    @Autowired
    DataSource dataSource;
    @Bean
    public SpringProcessEngineConfiguration getProcessEngineConfiguration(){
        SpringProcessEngineConfiguration config =
                new SpringProcessEngineConfiguration();
        config.setDataSource(dataSource);
        config.setTransactionManager(transactionManager);
        config.setDatabaseType("mysql");
        //使用uuid生成器
        config.setIdGenerator(new UUIDGenerator());
        config.setHistoryLevel(HistoryLevel.FULL);
        String activityFontName = "宋体";
        String labelFontName = "微软雅黑";
        String annotationFontName = "微软雅黑";
        config.setActivityFontName(activityFontName);
        config.setLabelFontName(labelFontName);
        config.setAnnotationFontName(annotationFontName);
        return config;
    }
}
```

```java
import org.activiti.engine.impl.cfg.IdGenerator;
import org.springframework.stereotype.Component;
import java.util.UUID;

@Component
public class UUIDGenerator implements IdGenerator {

    @Override
    public String getNextId() {
        return UUID.randomUUID().toString().replaceAll("-", "");
    }
}
```

### 2.任务监听器的使用

1. 流程图中配置任务监听器

   ```bash
   1.使用eclipse的activiti设计工具在流程节点上选择Listeners--Execution listeners
   2.Execution listeners的Type选择Delegate expression
   3.具体的expression中使用${taskListener}(taskListener是监听器名称，首字母小写)
   ```

2. 编写监听器实现类

   ```java
   public class TaskListener implements ExecutionListener {
       @Override
       public void notify(DelegateExecution execution) {
   	
   	}
   }
   ```

