## springboot2.1.6集成activiti6.0.0

[TOC]

### 1.pom配置

```xml
<properties>
        <java.version>1.8</java.version>
        <activiti.version>6.0.0</activiti.version>
</properties>

<dependencies>
	<!-- swagger api 生成器套件 -->
	<dependency>
	  <groupId>com.spring4all</groupId>
	  <artifactId>swagger-spring-boot-starter</artifactId>
	  <version>1.9.0.RELEASE</version>
	</dependency>

	<!-- json <-> obj 转化工具 -->
	<dependency>
		<groupId>com.alibaba</groupId>
		<artifactId>fastjson</artifactId>
		<version>1.2.58</version>
	</dependency>

	  <!-- getter setter 简化插件 -->
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<optional>true</optional>
	</dependency>

	  <!-- mybatis-plus 插件，mybatis 功能增强插件 -->
	<dependency>
		<groupId>com.baomidou</groupId>
		<artifactId>mybatis-plus-boot-starter</artifactId>
		<version>3.1.2</version>
	</dependency>

	<!-- mysql -->
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
		<version>5.1.47</version>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<scope>runtime</scope>
		<optional>true</optional>
	</dependency>

	<!-- mybatis-plus code generator 插件，mybatis plus 代码生成器插件 -->
	<dependency>
		<groupId>com.baomidou</groupId>
		<artifactId>mybatis-plus-generator</artifactId>
		<version>3.1.2</version>
	</dependency>

	<!-- mybatis-plus code generator 插件，必须指定任意模板，作为必要依赖添加 -->
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-freemarker</artifactId>
	</dependency>

	<!-- activit 6.0.0-->
    <!-- 忽略activiti自带的mybatis，否则会和项目中的mybatis冲突-->
	<dependency>
		<groupId>org.activiti</groupId>
		<artifactId>activiti-spring-boot-starter-basic</artifactId>
		<version>${activiti.version}</version>
		<exclusions>
			<exclusion>
				<artifactId>mybatis</artifactId>
				<groupId>org.mybatis</groupId>
			</exclusion>
		</exclusions>
	</dependency>
</dependencies>
```



