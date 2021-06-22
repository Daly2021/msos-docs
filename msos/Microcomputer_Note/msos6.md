# msos-后端开发

> 负责人，进击的攻城狮成员--代镓丞

## msos项目功能介绍

根据msos的ui设计和数据库表的设计，负责实现功能模块的开发



## msos项目结构

```
    club.msos   
    ├── main  
      │ java
        │club
          │msos
    │       └── aop                    // 切面
    │       └── config                 // 全局配置
    │       └── controller             // 控制器
    │       └── dao                    // 数据访问层
    │       └── interceptors           // 拦截器
    │       └── pojo                   // pojo
    │       └── service                // service
    │       └── utils                  // 工具类
                ├── MsosApplication         // springboot项目启动主入口
    ├── resources 				
        ├── mybatis      
    │       └── mapper                       // 数据存储对象
        ├── static       
    │       └── admin                        // 后台页面
    │       └── component                    // 组件
    │       └── css                          //全局样式  
    │       └── editormd                     // md编辑器
    │       └── error                        // 错误页
    │       └── font                         // 字体
    │       └── font-awesome                 // 图标
    │       └── fonts                        // 字体
    │       └── html                         // 视图层
    │       └── image                        // 图片
    │       └── js                           // 交互脚本
    │       └── layui                        // ui框架
    │       	└── favicon.ico                     // logo
    │       	└── user.json                       // 用户数据
    │       └── application.yml                     // 配置文件   多环境配置
    │       └── application-dev.yml                 //开发环境配置
    │       └── application-prod.yml                // 生产环境配置
    │       └── banner.txt                          //  打印的横幅
    │       └── log4j.properties                           // 日志配置
    ├── test    //测试
pom.xml      //项目工程依赖
```

## 配置文件

- 通用配置 `application.yml`

```yml
spring:
  profiles:
    active: dev
```

- 配置 `application-dev.yml`

````yml
# 数据源配置
spring:
  datasource:
    username: root
    password: 123456
    url: jdbc:mysql://localhost:3306/msos?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=Asia/Shanghai&zeroDateTimeBehavior=CONVERT_TO_NULL
    driver-class-name: com.mysql.cj.jdbc.Driver
    type: com.alibaba.druid.pool.DruidDataSource
    #druid 数据源专有配置
      # 初始连接数
    initialSize: 5
      # 最小连接池数量
    minIdle: 5
      # 最大连接池数量
    maxActive: 20
      # 配置获取连接等待超时的时间
    maxWait: 60000
      # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
    timeBetweenEvictionRunsMillis: 60000
      # 配置一个连接在池中最小生存的时间，单位是毫秒
    minEvictableIdleTimeMillis: 300000
      # 配置检测连接是否有效
    validationQuery: SELECT 1 FROM DUAL
    testWhileIdle: true
    testOnBorrow: false
    testOnReturn: false
    poolPreparedStatements: true

    filters: stat,wall,log4j
    maxPoolPreparedStatementPerConnectionSize: 20
    useGlobalDataSourceStat: true
    connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500


  mvc:
    formcontent:
      filter:
        enabled: true

  thymeleaf:
    prefix: classpath:/static/
    suffix: .html
    cache: false
  freemarker:
    cache: false

  mail:
    username: 2574833532@qq.com
    password: 123456
    host: smtp.qq.com
    properties:
      mail:
        smtp:
          ssl:
            enable: true
  redis:
    host: 60.205.188.140
    port: 6666

server:
  port: 8888

aliyun:
  oss:
    endpoint: oss-cn-chengdu.aliyuncs.com
    accessKeyId: LTAI5t9ycf44Y7zrk1hZJqR7
    accessKeySecret: u8sMnVriJbfDOP1Tf3S0Myj3X1wFEW
    bucketName: msos-dyzz

mybatis:
  type-aliases-package: club.msos.pojo
  mapper-locations: classpath:mybatis/mapper/*.xml
  
  
````

- `log4j.properties`配置

  ````properties
  log4j.rootLogger=DEBUG,console,file
  
  log4j.appender.console = org.apache.log4j.ConsoleAppender
  log4j.appender.console.Target = System.out
  log4j.appender.console.Threshold=DEBUG
  log4j.appender.console.layout = org.apache.log4j.PatternLayout
  log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
  
  log4j.appender.file = org.apache.log4j.RollingFileAppender
  log4j.appender.file.File=./log/msos.log
  log4j.appender.file.MaxFileSize=10mb
  log4j.appender.file.Threshold=DEBUG
  log4j.appender.file.layout=org.apache.log4j.PatternLayout
  log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
  
  log4j.logger.org.mybatis=DEBUG
  log4j.logger.java.sql=DEBUG
  log4j.logger.java.sql.Statement=DEBUG
  log4j.logger.java.sql.ResultSet=DEBUG
  log4j.logger.java.sql.PreparedStatement=DEBUG
  ````

------

## 项目对象模型(Project Object Model)

### pom.xml 依赖配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.4</version>
        <relativePath/>
        <!-- lookup parent from repository -->
    </parent>
    <groupId>club.msos</groupId>
    <artifactId>Msos</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>msos</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.4</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-mail</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <version>2.4.4</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <!--阿里云存储依赖-->
        <dependency>
            <groupId>com.aliyun.oss</groupId>
            <artifactId>aliyun-sdk-oss</artifactId>
            <version>3.6.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.auth0/java-jwt -->
        <dependency>
            <groupId>com.auth0</groupId>
            <artifactId>java-jwt</artifactId>
            <version>3.15.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.5</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.23</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.60</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.4.5</version>
            </plugin>
        </plugins>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <excludes>
                    <exclude>static/**</exclude>
                </excludes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>false</filtering>
                <includes>
                    <include>static/**</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
                <excludes>
                    <exclude>static/**</exclude>
                </excludes>
            </resource>
        </resources>
    </build>
</project>

```

#### banner.txt设计

> msos启动banner

![](https://7.dusays.com/2021/06/21/6fa9e7503a0de.png)



## 核心技术

### SpringBoot框架

1、介绍
`Spring Boot`是一款开箱即用框架，提供各种默认配置来简化项目配置。让我们的`Spring`应用变的更轻量化、更快的入门。 在主程序执行`main`函数就可以运行。你也可以打包你的应用为`jar`并通过使用`java -jar`来运行你的Web应用。它遵循"约定优先于配置"的原则， 使用`SpringBoot`只需很少的配置，大部分的时候直接使用默认的配置即可。同时可以与`Spring Cloud`的微服务无缝结合。

2、优点

- 使编码变得简单： 推荐使用注解。
- 使配置变得简单： 自动配置、快速集成新技术能力 没有冗余代码生成和XML配置的要求
- 使部署变得简单： 内嵌Tomcat、Jetty、Undertow等web容器，无需以war包形式部署
- 使监控变得简单： 提供运行时的应用监控
- 使集成变得简单： 对主流开发框架的无配置集成。
- 使开发变得简单： 极大地提高了开发快速构建项目、部署效率。

### Thymeleaf模板

1、介绍
Thymeleaf是一个用于Web和独立Java环境的模板引擎，能够处理HTML、XML、JavaScript、CSS甚至纯文本。

能轻易的与Spring MVC等Web框架进行集成作为Web应用的模板引擎。 与其它模板引擎（比如FreeMaker）相比，Thymeleaf最大的特点是能够直接在浏览器中打开并正确显示模板页面，而不需要启动整个Web应用（更加方便前后端分离，比如方便类似VUE前端设计页面），抛弃JSP吧。 

Thymeleaf 3.0是一个完全彻底重构的模板引擎，极大的减少内存占用和提升性能和并发性，避免v2.1版因大量的输出标记的集合产生的资源占用。 Thymeleaf 3.0放弃了大多数面向DOM的处理机制，变成了一个基于事件的模板处理器，它通过处理模板标记或文本并立即生成其输出，甚至在新事件之前响应模板解析器/缓存事件。Thymeleaf是Spring Boot官方的推荐使用模板。

2、优点

- 国际化支持非常简单
- 语法简单，功能强大。内置大量常用功能，使用非常方便
- 可以很好的和Spring集成
- 静态html嵌入标签属性，浏览器可以直接打开模板文件，便于前后端联调
- Spring Boot 官方推荐，用户群广

------

## msos启动类设计

`MsosApplication`:

![](https://7.dusays.com/2021/06/21/91cfaf860c16f.png)

# mso功能实现部分

## aop部分

- `Aspect`（切面）： Aspect 声明类似于 Java 中的类声明，在 Aspect 中会包含着一些 Pointcut 以及相应的 Advice。

  ```java
  package club.msos.aop;
  
  import club.msos.pojo.UpdateArticle;
  import club.msos.pojo.UpdateUser;
  import club.msos.service.updateArticleService;
  import club.msos.service.updateUserService;
  import club.msos.util.GetIp;
  import org.aspectj.lang.ProceedingJoinPoint;
  import org.aspectj.lang.annotation.*;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Component;
  import org.springframework.web.context.request.RequestAttributes;
  import org.springframework.web.context.request.RequestContextHolder;
  import org.springframework.web.context.request.ServletRequestAttributes;
  
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpSession;
  import java.text.SimpleDateFormat;
  import java.util.Date;
  import java.util.TimeZone;
  
  
  @Component
  @Aspect
  public class aspect {
      @Autowired
      updateArticleService updateArticleService;
      @Autowired
      updateUserService updateUserService;
      @Pointcut("execution(public * club.msos.controller..*.*(..))")
      public void Pointcut() {
      }
  
  
      @Around(value ="Pointcut()&&@annotation(log)")
      public Object doAround(ProceedingJoinPoint joinPoint, Log log) throws Throwable {
          Object result = joinPoint.proceed();
          RequestAttributes requestAttributes = RequestContextHolder.getRequestAttributes();
               HttpServletRequest request = (HttpServletRequest) requestAttributes
                        .resolveReference(RequestAttributes.REFERENCE_REQUEST);
          ServletRequestAttributes attr = (ServletRequestAttributes)RequestContextHolder.currentRequestAttributes();
          HttpSession session=attr.getRequest().getSession(true);
          GetIp ip = new GetIp(request);
          SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
          dateFormat.setTimeZone(TimeZone.getTimeZone("Etc/GMT-8"));
          if (log.Type().equals("用户删除")||log.Type().equals("用户更新")||log.Type().equals("用户登录")||log.Type().equals("头像更新")){
                  UpdateUser updateUser = new UpdateUser();
                  updateUser.setUpdateUser_do(log.Type());
                  updateUser.setUpdateUser_id((String) request.getAttribute("UpdateUser_id"));
                  updateUser.setUser_id((String) session.getAttribute("id"));
                  updateUser.setUpdateUser_ip(ip.getIpAddress());
                  updateUser.setUpdateUser_time(dateFormat.format(new Date()));
                  updateUserService.insertUpdateUser(updateUser);
  
              }else {
              UpdateArticle updateArticle = new UpdateArticle();
              updateArticle.setUpdateArticle_do(log.Type());
              updateArticle.setArticle_id((Integer) request.getAttribute("UpdateArticle_id"));
              updateArticle.setUpdateArticle_id((String) session.getAttribute("id"));
              updateArticle.setUpdateArticle_ip(ip.getIpAddress());
              updateArticle.setUpdateArticle_time(dateFormat.format(new Date()));
              System.out.println(updateArticle);
              updateArticleService.insertUpdateArticle(updateArticle);
              }
  
          return result;
      }
  }
  
  ```

  

- `log`

  ```java
  package club.msos.aop;
  
  import java.lang.annotation.*;
  
  @Target(ElementType.METHOD)
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
   public @interface Log {
      String Type() default "";  // 操作类型
   }
  ```

  ------

  ## config部分

- `druidConfig`配置

  ````java
  package club.msos.config;
  
  
  import com.alibaba.druid.pool.DruidDataSource;
  import com.alibaba.druid.support.http.StatViewServlet;
  import org.springframework.boot.context.properties.ConfigurationProperties;
  import org.springframework.boot.web.servlet.ServletRegistrationBean;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  import javax.sql.DataSource;
  import java.util.HashMap;
  
  @Configuration
  public class druidConfig {
  
      @ConfigurationProperties(prefix = "spring.datasource")
      @Bean
      public DataSource dataSource(){
       return new DruidDataSource();
      }
  
      @Bean
      public ServletRegistrationBean statViewServlet(){
          ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
          HashMap<String, String> initParams  = new HashMap<>();
          initParams.put("loginUsername","root");
          initParams.put("loginPassword","123456");
          bean.setInitParameters(initParams);
          return bean;
      }
  }
  ````

  

`MyMvcConfig`配置

```java
package club.msos.config;

import club.msos.interceptors.jwtInterceptor;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.Ordered;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class MyMvcConfig implements WebMvcConfigurer {
    @Override
    public void addViewControllers( ViewControllerRegistry registry ) {
        registry.addViewController( "/" ).setViewName( "forward:/homepage" );

        registry.setOrder( Ordered.HIGHEST_PRECEDENCE );
        WebMvcConfigurer.super.addViewControllers( registry );
    }

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
            registry.addInterceptor(new jwtInterceptor())
            .addPathPatterns("/user/**")
            .addPathPatterns("/html/index")
            .addPathPatterns("/toUpdateUser")
             .addPathPatterns("/desktop")
             .addPathPatterns("/updatePassword")
            .excludePathPatterns("/user/toLogin","/user/insertUser","/user/forget","/static/**");
    }
}

```

------

`RedisConfig`配置

```java
package club.msos.config;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

import java.net.UnknownHostException;

@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {
        RedisTemplate<String, Object> template = new RedisTemplate();
        template.setConnectionFactory(redisConnectionFactory);

        // 序列化配置
        Jackson2JsonRedisSerializer<Object> objectJackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        ObjectMapper om = new ObjectMapper();
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        om.enableDefaultTyping();
        objectJackson2JsonRedisSerializer.setObjectMapper(om);
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();

        template.setKeySerializer(stringRedisSerializer);
        template.setHashKeySerializer(stringRedisSerializer);
        template.setValueSerializer(objectJackson2JsonRedisSerializer);
        template.setHashValueSerializer(objectJackson2JsonRedisSerializer);

        template.afterPropertiesSet();

        return template;
    }
}
```

------

`SwaggerConfig`配置

```java
package club.msos.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.oas.annotations.EnableOpenApi;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;

import java.util.ArrayList;

@Configuration
@EnableOpenApi
public class SwaggerConfig {

    @Bean
   public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("club.msos.controller"))
                .build()
                ;
    }

    private ApiInfo apiInfo(){

        Contact contact = new Contact("dyzz", "http://msos.club:8888/", "2574833532@qq.com");
        return new ApiInfo("fwTeam的API","相信美好的事物即将发生","v1.0","http://msos.club:8888/",contact,"Apache 2.0", "http://www.apache.org/licenses/LICENSE-2.0", new ArrayList());
    }
}

```

------

## Controller控制层部分

`articleController`功能部分

````java
package club.msos.controller;

import club.msos.aop.Log;
import club.msos.pojo.Article;
import club.msos.pojo.User;
import club.msos.util.Load;
import com.alibaba.fastjson.JSON;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

import javax.servlet.http.HttpServletRequest;
import java.io.File;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/article")
@CrossOrigin(origins = "*",maxAge = 3600)
@Api(value = "文章接口",tags = "文章接口")
public class articleController {

    @Autowired
    club.msos.service.articleService articleService;

    @Autowired
    club.msos.service.userService userService;
    @Log(Type = "删除文章")
    @PostMapping("/deleteArticle")
    public JSON deleteArticle(HttpServletRequest request,Integer article_id){
        HashMap<Object, Object> map = new HashMap<>();
        int i = articleService.deleteArticle(article_id);
        String status;
        if(i>0){
            request.setAttribute("UpdateArticle_id",article_id);
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @return: 上传图片
     */
    @ApiOperation(value = "上传图片接口",notes = "上传图片接口")
//    @ApiImplicitParams({ @ApiImplicitParam(paramType = "header", dataType = "String", name = "token", value = "token标记", required = true) })
    @PostMapping( "/insertImg")
    public JSON updateImg(HttpServletRequest request, String article_title, @RequestPart("file") MultipartFile file){
        HashMap<Object, Object> map = new HashMap<>();
        File file0 = null;
        System.out.println(file);
        try {
            file0=File.createTempFile("tmp", null);
            file.transferTo(file0);
            file0.deleteOnExit();
            Load load = new Load();
            load.upload(file0,article_title);
            map.put("status","200");
        }catch (Exception e) {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 查询所有文章
     */
    @GetMapping("/selectArticle")
    @ApiOperation(value = "查询所有文章接口",notes = "传值进来")
    public JSON selectAllArticle(Model model, Article article){
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            User user = new User();
            user.setUser_id(article1.getUser_id());
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(articles.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",articles.size());
        map.put("data",articles);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}

````

------

`commentController`评论功能部分

```java
package club.msos.controller;

import club.msos.pojo.Article;
import club.msos.pojo.Comment;
import club.msos.pojo.User;
import club.msos.util.dateTime;
import com.alibaba.fastjson.JSON;
import club.msos.service.commentService;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

import javax.servlet.http.HttpSession;
import java.util.Date;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/comment")
@CrossOrigin(origins = "*",maxAge = 3600)
@Api(value = "评论接口",tags = "评论接口")
public class commentController {

    @Autowired
    commentService commentService;
    @Autowired
    club.msos.service.userService userService;
    @Autowired
    club.msos.service.articleService articleService;
    @PostMapping("/deleteComment")
    public JSON deleteComment(Model model,Integer comment_id){
        HashMap<Object, Object> map = new HashMap<>();
        int i = commentService.deleteComment(comment_id);
        String status;
        if(i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }

    @PostMapping("/toComment")
    @ApiOperation(value = "评论接口",notes = "传值进来")
    public JSON toMessages(Model model, String comment_content,Integer article_id, HttpSession session){
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        Comment comment = new Comment();
        Date date = new Date();
        comment.setArticle_id(article_id);
        comment.setComment_id((int) date.getTime());
        comment.setComment_content(comment_content);
        comment.setComment_ip((String) session.getAttribute("ip"));
        comment.setUser_id((String) session.getAttribute("id"));
        dateTime dateTime = new dateTime();
        comment.setComment_time(dateTime.getTime());
        int i = commentService.insertComment(comment);
        Article article = new Article();
        article.setArticle_id(article_id);
        List<Article> articles = articleService.selectArticle(article);
        Article article1 = articles.get(0);
        int count = article1.getArticle_comment_count()+1;
        if(i>0){
            msg="200";
            article1.setArticle_comment_count(count);
            articleService.updateArticle(article1);
        }else {
            msg="500";
        }
        map.put("msg",msg);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 查询所有评论
     */
    @GetMapping("/selectComment")
    @ApiOperation(value = "查询所有评论接口",notes = "传值进来")
    public JSON selectAllArticle(Model model, Comment comment){
        List<Comment> comments = commentService.selectComment(comment);
        for (Comment comment1 : comments) {
            User user = new User();
            user.setUser_id(comment1.getUser_id());
            List<User> users = userService.selectUser(user);
            comment1.setUser_name(users.get(0).getUser_name());
        }
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(comments.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",comments.size());
        map.put("data",comments);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}


```

------

`JumpController`跳转功能部分

```java
package club.msos.controller;

import club.msos.aop.Log;
import club.msos.pojo.*;
import club.msos.util.GetIp;
import club.msos.util.dateTime;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.net.UnknownHostException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.TimeZone;

@Controller
public class JumpController {
    @Autowired
    club.msos.service.userService userService;
    @Autowired
    club.msos.service.messageService messageService;
    @Autowired
    club.msos.service.articleService articleService;
    @Autowired
    club.msos.service.commentService commentService;
    @Autowired
    club.msos.service.linksService linksService;
    @Autowired
    RedisTemplate redisTemplate;

    /**
     * @param:子评论
     */
    @PostMapping("/childMessages")
    public String childMessages(Model model, String child_message_content, Integer child_message_parant_id, HttpSession session){
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        Message message = new Message();
        Date date = new Date();
        if(session.getAttribute("id")==null){
            return "html/login";
        }else{
            message.setMessage_parant_id(child_message_parant_id);
            message.setMessage_id((int) date.getTime());
            message.setMessage_content(child_message_content);
            message.setMessage_ip((String) session.getAttribute("ip"));
            message.setUser_id((String) session.getAttribute("id"));
            dateTime dateTime = new dateTime();
            message.setMessage_time(dateTime.getTime());
            int i = messageService.insertMessage(message);
            return "redirect:/message";
        }
    }
    @RequestMapping("/toWrote")
    public String toWrite(Model model){
        Date date = new Date();
        model.addAttribute("article_id",(int) date.getTime());
        return "html/write";
    }
    /**
     * @param: 跳转aboutMe
     */
    @RequestMapping("/aboutMe")
    public String aboutMe(){
        return "html/aboutMe";
    }
    /**
     * @param: 跳转友链更新
     */
    @RequestMapping("/toUpdateLinks")
    public String toUpdateLinks(Model model, Links links){
        model.addAttribute("links",links);

        return "html/updateLinks";
    }
    /**
     * @param: 跳转用户更新
     */
    @RequestMapping("/toUpdateUser")
    public String toUpdateUser(){
        return "html/updateUser";
    }
    /**
     * @param: 跳转用户更新
     */
    @RequestMapping("/adminUpdateUser")
    public String adminUpdateUser(Model model, User user){
        model.addAttribute("user",user);
        return "html/admin-UpdateUser";
    }
    /**
     * @param: 提交文章
     */
    @Log(Type = "提交文章")
    @PostMapping("/addArticle")
    @ApiOperation(value = "新增文章接口",notes = "传值进来")
    public String addArticle(HttpServletRequest request, Article article, HttpSession session){
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        Date date = new Date();
        dateTime dateTime = new dateTime();
        String msg;
        article.setArticle_id((int) date.getTime());
        article.setArticle_views(0);
        article.setUser_name((String) session.getAttribute("name"));
        article.setUser_id((String) session.getAttribute("id"));
        article.setArticle_time(dateTime.getTime());
        article.setArticle_comment_count(0);
        request.setAttribute("UpdateArticle_id",article.getArticle_id());
        articleService.insertArticle(article);
        return "redirect:/article";
    }
    /**
     * @param: 跳转详细阅读
     */
    @RequestMapping("/read")
    public String read(Model model, String article_title){
        Article article = new Article();
        article.setArticle_title(article_title);
        List<Article> articles = articleService.selectArticle(article);
        System.out.println(articles);
        Article article1 = articles.get(0);
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
            model.addAttribute("article",article1);
            article1.setArticle_views(article1.getArticle_views()+1);
            articleService.updateArticle(article1);
        Comment comment = new Comment();
        comment.setArticle_id(article1.getArticle_id());
        List<Comment> comments = commentService.selectComment(comment);
        for (Comment comment1 : comments) {
            String user_id1 = comment1.getUser_id();
            User user1 = new User();
            user1.setUser_id(user_id1);
            List<User> user1s = userService.selectUser(user1);
            comment1.setUser_name(user1s.get(0).getUser_name());
        }
        model.addAttribute("comment",comments);
        return "html/read";
    }
    /**
     * @param: 跳转留言板
     */
    @RequestMapping("/message")
    public String message(Model model){
        Message message = new Message();
        List<Message> messages = messageService.selectMessage(message);
        for (Message message1 : messages) {
            String user_id = message1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            message1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("message",messages);
        return "html/message";
    }
    /**
     * @param: 跳转文章页面
     */
    @RequestMapping("/other")
    public String other(Model model){
        Article article = new Article();
        article.setArticle_type("其他");
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("article",articles);

        return "html/article";
    }
    @RequestMapping("/javaLu")
    public String javaLu(Model model){
        Article article = new Article();
        article.setArticle_type("我的Java路");
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("article",articles);

        return "html/article";
    }
    @RequestMapping("/wxArticle")
    public String wxArticle(Model model){
        Article article = new Article();
        article.setArticle_type("文学杂志");
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("article",articles);

        return "html/article";
    }
    @RequestMapping("/rzArticle")
    public String rzArticle(Model model){
        Article article = new Article();
        article.setArticle_type("个人日志");
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("article",articles);

        return "html/article";
    }
    @RequestMapping("/article")
    public String article(Model model){
        Article article = new Article();
        List<Article> articles = articleService.selectArticle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        List<Article> articlesDesc = articleService.selectArticleDesc();
        model.addAttribute("articleDesc",articlesDesc);
        model.addAttribute("article",articles);

        return "html/article";
    }
    @RequestMapping("/selectArticle")
    public String selectArticle(Model model,String article_title){
        Article article = new Article();
        article.setArticle_title(article_title);
        List<Article> articles = articleService.selectArticleByTitle(article);
        for (Article article1 : articles) {
            String user_id = article1.getUser_id();
            User user = new User();
            user.setUser_id(user_id);
            List<User> users = userService.selectUser(user);
            article1.setUser_name(users.get(0).getUser_name());
        }
        model.addAttribute("article",articles);

        return "html/article";
    }
    /**
     * @param: 跳转友链
     */
    @RequestMapping("/link")
    public String link(Model model, Links links){
        List<Links> linksList = linksService.selectLinks(links);
        model.addAttribute("links",linksList);
        return "html/link";
    }
    /**
     * @param: 博客主页
     */
    @RequestMapping("/homepage")
    public String homepage(Model model,HttpSession session){
        List<Article> articles = articleService.selectArticleDesc();
        model.addAttribute("article",articles);
        User user1 = new User();
        Article article1=new Article();
        Message message = new Message();
        Comment comment = new Comment();
        List<User> users1 = userService.selectUser(user1);
        List<Message> messages = messageService.selectMessage(message);
        List<Comment> comments = commentService.selectComment(comment);
        session.setAttribute("userCount",users1.size());
        session.setAttribute("articlesCount",articles.size());
        session.setAttribute("messageCount",messages.size());
        session.setAttribute("commentCount",comments.size());
        Date date = new Date();
        int day = date.getDay();
        String Day;
        if (day==1){
            Day="Monday";
        }else if(day==2){
            Day="Tuesday";
        }else if(day==3){
            Day="Wednesday";
        }else if(day==4){
            Day="Thursday";
        }else if(day==5){
            Day="Friday";
        }else if(day==6){
            Day="Saturday";
        }else {
            Day="Sunday";
        }
        redisTemplate.opsForHash().increment("DayTime",Day,1);
        session.setAttribute("Monday",redisTemplate.opsForHash().get("DayTime", "Monday"));
        session.setAttribute("Tuesday",redisTemplate.opsForHash().get("DayTime", "Tuesday"));
        session.setAttribute("Wednesday",redisTemplate.opsForHash().get("DayTime", "Wednesday"));
        session.setAttribute("Thursday",redisTemplate.opsForHash().get("DayTime", "Thursday"));
        session.setAttribute("Friday",redisTemplate.opsForHash().get("DayTime", "Friday"));
        session.setAttribute("Saturday",redisTemplate.opsForHash().get("DayTime", "Saturday"));
        session.setAttribute("Sunday",redisTemplate.opsForHash().get("DayTime", "Sunday"));
        return "html/homepage";
    }
    /**
     * @param: 退出登录
     */
    @RequestMapping("/loginOut")
    public String loginOut(HttpSession session){
        session.removeAttribute("token");
        session.removeAttribute("id");
        session.removeAttribute("ip");
        session.removeAttribute("name");
        session.removeAttribute("birthday");
        session.removeAttribute("email");
        session.removeAttribute("phone");
        return "html/login";
    }
    /**
     * @param: 我的桌面
     */
    @RequestMapping("/desktop")
    public String desktop(){
        return "html/welcome";
    }
    /**
     * @param: 登录
     */
    @Log(Type = "用户登录")
    @RequestMapping("/login")
    public String login(Model model,HttpServletRequest request, HttpServletResponse response, HttpSession session, String token, String user_id) throws UnknownHostException {
        String ip;
        User user = new User(user_id,null,null,null,null,null,null,null,null);
        List<User> users = userService.selectUser(user);
        request.setAttribute("UpdateUser_id",user.getUser_id());
        GetIp getIp = new GetIp(request);
        ip = getIp.getIpAddress();
        user.setUser_ip(ip);
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        dateFormat.setTimeZone(TimeZone.getTimeZone("Etc/GMT-8"));
        int i = userService.updateUser(user);
        session.setAttribute("token",token);
        session.setAttribute("id",user_id);
        session.setAttribute("name",users.get(0).getUser_name());
        session.setAttribute("email",users.get(0).getUser_email());
        session.setAttribute("birthday",users.get(0).getUser_birthday());
        session.setAttribute("phone",users.get(0).getUser_phone());
        session.setAttribute("ip",ip);
        session.setAttribute("time",dateFormat.format(new Date()));
        if (users.get(0).getUser_role().equals("admin")){
            User user1 = new User();
            user1.setUser_role("admin");
            List<User> users1 = userService.selectUser(user1);
            User user2 = new User();
            user2.setUser_role("user");
            List<User> users2 = userService.selectUser(user2);
            session.setAttribute("adminCount",users1.size());
            session.setAttribute("hyCount",users2.size());
            Article article = new Article();
            List<Article> articles = articleService.selectArticle(article);
            Article article1 = new Article();
            article1.setArticle_type("我的Java路");
            List<Article> articles1 = articleService.selectArticle(article1);
            session.setAttribute("Javalu",articles1.size());
            Article article2 = new Article();
            article2.setArticle_type("文学杂志");
            List<Article> articles2 = articleService.selectArticle(article2);
            session.setAttribute("wxzz",articles2.size());
            Article article3 = new Article();
            article3.setArticle_type("个人日志");
            List<Article> articles3 = articleService.selectArticle(article3);
            session.setAttribute("grrz",articles3.size());
            session.setAttribute("qt1",articles.size()-articles1.size()-articles2.size()-articles3.size());
            return "html/index";
        }else {

            return "redirect:/article";
        }

    }

    /**
     * @param: 修改密码
     */
    @PostMapping("/updatePassword")
    @ResponseBody
    public String updatePassword(String user_id,String user_name){
        User user = new User(user_id,user_name,null,null,null,null,null,null,null);
        int i = userService.updateUser(user);
        if (i>0){
            return "修改成功请返回登录页面!";
        }else {
            return "修改失败!";
        }

    }
    /**
     * @param: 跳转修改密码页面
     */
    @RequestMapping("/ToUpdatePassword")
    public String ToUpdatePassword(Model model,String user_id){
        model.addAttribute("user_id",user_id);
        return "forward:/updatePassword.html";
    }
}

```

------

`linksController` 友链跳转

```java
package club.msos.controller;

import club.msos.pojo.Links;
import com.alibaba.fastjson.JSON;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/links")
public class linksController {

    @Autowired
    club.msos.service.linksService linksService;
    /**
     * @return: 友链更新
     */
    @PostMapping("/updateLinks")
    public JSON updateUser(Links links){
        int i = linksService.updateLinks(links);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String status;
        if(i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 友链注册
     */
    @PostMapping("/insertLinks")
    public JSON insertUser(Links links){

        int i = linksService.insertLinks(links);
        String status;
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        if (i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     *
     * @param: 友链删除
     */
    @PostMapping("/deleteLinks")
    public JSON delete(Integer links_id){
        int i = linksService.deleteLinks(links_id);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String status;
        if(i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 查询所有友链
     */
    @GetMapping("/selectLinks")
    public JSON selectLinks(Model model,Links link){
        List<Links> links = linksService.selectLinks(link);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(links.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",links.size());
        map.put("data",links);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}
```

------

`messageController` 留言部分

```java
package club.msos.controller;

import club.msos.pojo.Message;
import club.msos.pojo.User;
import club.msos.util.dateTime;
import com.alibaba.fastjson.JSON;
import club.msos.service.messageService;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

import javax.servlet.http.HttpSession;
import java.util.*;

@RestController
@RequestMapping("/message")
@Api(value = "留言接口",tags = "留言接口")
public class messageController {

    @Autowired
    messageService messageService;
    @Autowired
    club.msos.service.userService userService;
    @PostMapping("/deleteMessage")
    public JSON deleteArticle(Model model,Integer message_id){
        HashMap<Object, Object> map = new HashMap<>();
        int i = messageService.deleteMessage(message_id);
        String status;
        if(i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }

    @PostMapping("/toMessages")
    @ApiOperation(value = "去留言接口",notes = "传值进来")
    public JSON toMessages(Model model, String message_content,Integer message_parant_id, HttpSession session){
        System.out.println("==>"+message_content);
        System.out.println("==>"+message_parant_id);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        Message message = new Message();
        Date date = new Date();
        message.setMessage_parant_id(message_parant_id);
        message.setMessage_id((int) date.getTime());
        message.setMessage_content(message_content);
        message.setMessage_ip((String) session.getAttribute("ip"));
        message.setUser_id((String) session.getAttribute("id"));
        dateTime dateTime = new dateTime();
        message.setMessage_time(dateTime.getTime());
        int i = messageService.insertMessage(message);

        if(i>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("msg",msg);
        JSON json = (JSON) JSON.toJSON(map);
        System.out.println(json);
        return json;
    }
    /**
     * @param: 查询所有留言
     */
    @GetMapping("/selectMessage")
    @ApiOperation(value = "查询所有留言接口",notes = "传值进来")
    public JSON selectAllMessages(Model model, Message message){
        List<Message> messages = messageService.selectMessage(message);
        for (Message messages1 : messages) {
            User user = new User();
            user.setUser_id(messages1.getUser_id());
            List<User> users = userService.selectUser(user);
            messages1.setUser_name(users.get(0).getUser_name());
        }
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(messages.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",messages.size());
        map.put("data",messages);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}

```

------

`updateArticleController` 更新文章跳转功能

```java
package club.msos.controller;

import club.msos.pojo.UpdateArticle;
import com.alibaba.fastjson.JSON;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/updateArticleList")
public class updateArticleController {

    @Autowired
    club.msos.service.updateArticleService updateArticleService;
    @GetMapping("/selectUpdateArticleList")
    public JSON selectUpdateArticleList(){
        List<UpdateArticle> updateArticles = updateArticleService.selectUpdateArticle();
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(updateArticles.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",updateArticles.size());
        map.put("data",updateArticles);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}
```

------

`updateUserController` 更新用户信息功能

```java
package club.msos.controller;

import club.msos.pojo.UpdateUser;
import com.alibaba.fastjson.JSON;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/updateUserList")
public class updateUserController {

    @Autowired
    club.msos.service.updateUserService updateUserService;
    @GetMapping("/selectUpdateUserList")
    public JSON selectUpdateArticleList(){
        List<UpdateUser> updateUsers = updateUserService.selectUpdateUser();
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(updateUsers.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",updateUsers.size());
        map.put("data",updateUsers);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}

```

------

`userController` 用户功能

```java
package club.msos.controller;

import club.msos.aop.Log;
import club.msos.pojo.User;
import club.msos.util.JwtToken;
import club.msos.util.Load;
import com.alibaba.fastjson.JSON;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiImplicitParam;
import io.swagger.annotations.ApiImplicitParams;
import io.swagger.annotations.ApiOperation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

import javax.mail.MessagingException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.List;

@RestController
@RequestMapping("/user")
@CrossOrigin(origins = "*",maxAge = 3600)
@Api(value = "用户信息接口",tags = "用户信息接口")
public class userController {

    @Autowired
    club.msos.service.userService userService;

    @Autowired
    club.msos.util.emileSend emileSend;

    /**
     * @param: 忘记密码
     */
    @PostMapping("/forget")
    @ApiOperation(value = "忘记密码接口",notes = "修改密码")
    public JSON forgetPassword(String user_email,String user_id){
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String status;
        try {
            emileSend.Send(user_email,user_id);

        } catch (MessagingException e) {
            map.put("status","500");
        }
        map.put("status","200");

        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     *
     * @param: 用户删除
     */
    @Log(Type = "用户删除")
    @PostMapping("/deleteUser")
    @ApiOperation(value = "用户删除接口",notes = "用户删除!")
    @ApiImplicitParams({ @ApiImplicitParam(paramType = "header", dataType = "String", name = "token", value = "token标记", required = true) })
    public JSON delete(String user_id,HttpServletRequest request){
        int i = userService.deleteUser(user_id);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String status;
        if(i>0){
            request.setAttribute("UpdateUser_id",user_id);
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @return: 头像更新
     */
    @Log(Type = "头像更新")
    @ApiOperation(value = "上传头像接口",notes = "上传头像接口")
//    @ApiImplicitParams({ @ApiImplicitParam(paramType = "header", dataType = "String", name = "token", value = "token标记", required = true) })
    @PostMapping( "/updateImg")
    public JSON updateImg(HttpServletRequest request,String user_id, @RequestPart("file") MultipartFile file){
        HashMap<Object, Object> map = new HashMap<>();
        File file0 = null;
        System.out.println(file);
        try {
            file0=File.createTempFile("tmp", null);
            file.transferTo(file0);
            file0.deleteOnExit();
            Load load = new Load();
            load.upload(file0,user_id);
            request.setAttribute("UpdateUser_id",user_id);
            map.put("status","200");
        }catch (Exception e) {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @return: 用户更新
     */
    @Log(Type = "用户更新")
    @PostMapping("/updateUser")
    @ApiOperation(value = "用户更新接口",notes = "用户修改!")
    public JSON updateUser(User user, HttpServletRequest request){
        System.out.println(user);
        int i = userService.updateUser(user);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String status;
        if(i>0){
            request.setAttribute("UpdateUser_id",user.getUser_id());
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 用户注册
     */
    @PostMapping("/insertUser")
    @ApiOperation(value = "用户注册接口",notes = "用户注册!")
    public JSON insertUser(String user_id,String user_password,String user_name,String user_email,String user_phone,String user_sex,String user_ip,String user_birthday){
        User user0 = new User(user_id, user_password, user_name, user_email, user_phone, user_sex, user_ip, "user",user_birthday);
        int i = userService.insertUser(user0);
        String status;
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        if (i>0){
            map.put("status","200");
        }else {
            map.put("status","500");
        }
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 用户登录
     */
    @PostMapping("/toLogin")
    @ApiOperation(value = "登录接口",notes = "传值哈!")
    public JSON Login(HttpServletRequest request, HttpServletResponse response, Model model, String user_id, String user_password){
        User user0 = new User(user_id, user_password, null, null, null, null, null, null,null);
        List<User> users = userService.selectUser(user0);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String token = JwtToken.createToken(user0.getUser_id());
        String status;
        if(users.size()==1){
            status="200";
            map.put("message","ok");
            map.put("token",token);
            map.put("user_id",users.get(0).getUser_id());
            map.put("user_name",users.get(0).getUser_name());
        }else {
            status="500";
            map.put("message","error");
        }
        map.put("status",status);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 获取用户信息
     */
    @GetMapping("/selectAdmin")
    @ApiOperation(value = "获取用户信息接口",notes = "传值进来")
    @ApiImplicitParams({ @ApiImplicitParam(paramType = "header", dataType = "String", name = "token", value = "token标记", required = true) })
    public JSON selectAdmin(Model model,User user){
        user.setUser_role("admin");
        List<User> users = userService.selectUser(user);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(users.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",users.size());
        map.put("data",users);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
    /**
     * @param: 获取用户信息
     */
    @GetMapping("/selectUser")
    @ApiOperation(value = "获取用户信息接口",notes = "传值进来")
    @ApiImplicitParams({ @ApiImplicitParam(paramType = "header", dataType = "String", name = "token", value = "token标记", required = true) })
    public JSON selectAllUser(Model model,User user){
        List<User> users = userService.selectUser(user);
        LinkedHashMap<Object, Object> map = new LinkedHashMap<>();
        String msg;
        if(users.size()>0){
            msg="200";
        }else {
            msg="500";
        }
        map.put("code",0);
        map.put("msg",msg);
        map.put("count",users.size());
        map.put("data",users);
        JSON json = (JSON) JSON.toJSON(map);
        return json;
    }
}
```

------

`ossController`,oss阿里云存储跳转功能

```java
package club.msos.controller;

import club.msos.util.OssUtil;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;


import java.util.HashMap;
import java.util.Map;

@RestController
@RequestMapping("/oss")
public class ossController {

    @Autowired
    OssUtil ossUtil;  //注入OssUtil

    @PostMapping("/uploadfile")
    public Object fileUpload(@RequestParam("file") MultipartFile file,String fileName)
    {
        try {
            String url = ossUtil.uploadFile(file,fileName); //调用OSS工具类
            Map<String, Object> returnbody = new HashMap<>();
            Map<String, Object> returnMap = new HashMap<>();
            returnMap.put("url", url);
            returnbody.put("data",returnMap);
            returnbody.put("status","200");
            returnbody.put("message","上传成功");
            return returnbody;
        }
        catch (Exception e) {
            Map<String, Object> returnbody = new HashMap<>();
            returnbody.put("data",null);
            returnbody.put("status","500");
            returnbody.put("message","上传失败");
            return  returnbody;
        }
    }
    @PostMapping("/articleUpload")
    public Object articleUpload(@RequestParam(value = "editormd-image-file", required = false) MultipartFile file,String fileName)
    {
        try {
            String url = ossUtil.uploadFile(file,fileName); //调用OSS工具类
            Map<String, Object> returnbody = new HashMap<>();
            returnbody.put("url", url);
            returnbody.put("success",1);
            returnbody.put("status","200");
            returnbody.put("message","上传图片成功");
            return returnbody;
        }
        catch (Exception e) {
            Map<String, Object> returnbody = new HashMap<>();
            returnbody.put("success",0);
            returnbody.put("status","500");
            returnbody.put("message","上传图片失败");
            return  returnbody;
        }
    }
}
```

------

## DAO层

1.`articleMapper` :

```java
package club.msos.dao;
import club.msos.pojo.Article;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import org.springframework.stereotype.Repository;
import java.util.List;

@Mapper
@Repository
public interface articleMapper {
    List<Article> selectArticleDesc();

    List<Article> selectArticle(Article article);

    List<Article> selectArticleByTitle(Article article);

    int deleteArticle(@Param("article_id") Integer article_id);

    int insertArticle(Article article);

    int updateArticle(Article article);
}
```

2.`commentMapper`:

```java
package club.msos.dao;
import club.msos.pojo.Comment;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import org.springframework.stereotype.Repository;
import java.util.List;

@Mapper
@Repository
public interface commentMapper {
    List<Comment> selectComment(Comment comment);

    int deleteComment(@Param("comment_id") Integer comment_id);

    int insertComment(Comment comment);

    int updateComment(Comment comment);
}
```

3.`linksMapper`:

```java
package club.msos.dao;

import club.msos.pojo.Links;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import org.springframework.stereotype.Repository;
import java.util.List;

@Mapper
@Repository
public interface linksMapper {
    List<Links> selectLinks(Links links);

    List<Links> selectLinksByTitle(Links links);

    int deleteLinks(@Param("links_id") Integer links_id);

    int updateLinks(Links links);

    int insertLinks(Links links);
}
```

------

 4.`messageMapper`:

```java
package club.msos.dao;

import club.msos.pojo.Message;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import org.springframework.stereotype.Repository;

import java.util.List;

@Mapper
@Repository
public interface messageMapper {

    List<Message> selectMessage(Message message);

    int deleteMessage(@Param("message_id")Integer message_id);

    int insertMessage(Message message);

    int updateMessage(Message message);

}

```

5.`updateArticleMapper`:

```java
package club.msos.dao;

import club.msos.pojo.UpdateArticle;
import org.apache.ibatis.annotations.Mapper;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
@Mapper
public interface updateArticleMapper {

    List<UpdateArticle> selectUpdateArticle();

    int insertUpdateArticle(UpdateArticle updateArticle);
}

```

6.`updateUserMapper`:

```java
package club.msos.dao;

import club.msos.pojo.UpdateUser;
import org.apache.ibatis.annotations.Mapper;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
@Mapper
public interface updateUserMapper {

    List<UpdateUser> selectUpdateUser();

    int insertUpdateUser(UpdateUser updateUser);
}

```

7.`userMapper`:

```java
package club.msos.dao;

import club.msos.pojo.User;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;
import org.springframework.stereotype.Repository;

import java.util.List;

@Mapper
@Repository
public interface userMapper {
    List<User> selectUser(User user);

    int insertUser(User user);

    int updateUser(User user);

    int deleteUser(@Param("user_id") String user_id);
}

```

------

## 拦截器Interceptors

### jwt拦截器

```java
package club.msos.interceptors;

import club.msos.util.JwtToken;
import com.alibaba.fastjson.JSON;
import org.springframework.web.servlet.HandlerInterceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.util.HashMap;

public class jwtInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        HttpServletRequest httpRequest = (HttpServletRequest) request;
        HttpSession session = httpRequest.getSession();
        HashMap<String, Object> map = new HashMap<>();
        String token = (String) session.getAttribute("token");
        try {
            JwtToken.isToken(token);
            map.put("message","ok");
            return true;
        } catch (Exception e) {
            session.removeAttribute("id");
            session.removeAttribute("ip");
            session.removeAttribute("name");
            session.removeAttribute("birthday");
            session.removeAttribute("email");
            session.removeAttribute("phone");
            response.sendRedirect("/html/login.html");
            map.put("message","error");
        }
        JSON json = (JSON) JSON.toJSON(map);
        response.setContentType("application/json;charset=UTF-8");
        response.getWriter().println(json);
        return false;
    }
}

```

## pojo

> 使用注解方式实现

`Article` :

```java
package club.msos.pojo;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@ApiModel(value = "文章实体类",description = "文章对象")
public class Article {
    @ApiModelProperty(value = "文章id")
    private Integer article_id;
    @ApiModelProperty(value = "文章标题")
    private String article_title;
    @ApiModelProperty(value = "用户名")
    private String user_id;
    @ApiModelProperty(value = "文章内容")
    private String article_content;
    @ApiModelProperty(value = "观看人数")
    private  Integer article_views;
    @ApiModelProperty(value = "文章评论数量")
    private  Integer article_comment_count;
    @ApiModelProperty(value = "发表时间")
    private  String article_time;
    @ApiModelProperty(value = "文章类型")
    private  String article_type;
    private String user_name;
}
```

`Comment`:

```java
package club.msos.pojo;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@ApiModel(value = "评论实体类",description = "评论对象")
public class Comment {
    @ApiModelProperty(value = "评论id")
    private  Integer comment_id;
    @ApiModelProperty(value = "用户名")
    private String user_id;
    @ApiModelProperty(value = "文章id")
    private Integer article_id;
    @ApiModelProperty(value = "发表时间")
    private String comment_time;
    @ApiModelProperty(value = "评论内容")
    private String comment_content;
    private String user_name;
    private String comment_ip;
}
```

`Links`:

```java
package club.msos.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class Links {
    private Integer links_id;
    private String links_name;
    private String links_title;
    private String links_url;
    private String links_img;
}
```

`Message`:

```java
package club.msos.pojo;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@ApiModel(value = "留言实体类",description = "留言对象")
public class Message {
    @ApiModelProperty(value = "留言id")
    private Integer message_id;
    @ApiModelProperty(value = "用户名")
    private String user_id;
    @ApiModelProperty(value = "留言内容")
    private String message_content;
    @ApiModelProperty(value = "发表时间")
    private String message_time;
    @ApiModelProperty(value = "父评论id")
    private  Integer message_parant_id;
    @ApiModelProperty(value = "评论ip")
    private String message_ip;
    private String user_name;
}

```

`UpdateArticle`:

```java
package club.msos.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class UpdateArticle {
    private String updateArticle_id;
    private Integer article_id;
    private String updateArticle_do;
    private String updateArticle_time;
    private String updateArticle_ip;
}

```

`UpdateUser`:

```java
package club.msos.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class UpdateUser {
    private String updateUser_id;
    private String user_id;
    private String updateUser_do;
    private String updateUser_time;
    private String updateUser_ip;
}

```

`User`:

```java
package club.msos.pojo;

import com.alibaba.fastjson.annotation.JSONType;
import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@JSONType(orders={"username","password","name","email","phone","xb","location","role"})
@ApiModel(value = "用户实体类",description = "用户对象")
public class User {
    @ApiModelProperty(value = "用户名")
    private String user_id;
    @ApiModelProperty(value = "密码")
    private String user_password;
    @ApiModelProperty(value = "姓名")
    private String user_name;
    @ApiModelProperty(value = "邮箱")
    private String user_email;
    @ApiModelProperty(value = "电话号")
    private String user_phone;
    @ApiModelProperty(value = "性别")
    private String user_sex;
    @ApiModelProperty(value = "ip地址")
    private String user_ip;
    @ApiModelProperty(value = "权限")
    private String user_role;
    @ApiModelProperty(value = "用户生日")
    private String user_birthday;
}

```

------

## Service 层 ，接口+实现

1. `articleServiceImpl`

   ```java
   package club.msos.service;
   
   import club.msos.pojo.Article;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public class articleServiceImpl implements articleService{
   
       @Autowired
       club.msos.dao.articleMapper articleMapper;
   
       @Override
       public List<Article> selectArticleDesc() {
           return articleMapper.selectArticleDesc();
       }
   
       @Override
       public List<Article> selectArticle(Article article) {
           return articleMapper.selectArticle(article);
       }
   
       @Override
       public List<Article> selectArticleByTitle(Article article) {
           return articleMapper.selectArticleByTitle(article);
       }
   
       @Override
       public int deleteArticle(Integer article_id) {
           return articleMapper.deleteArticle(article_id);
       }
   
       @Override
       public int insertArticle(Article article) {
           return articleMapper.insertArticle(article);
       }
   
       @Override
       public int updateArticle(Article article) {
           return articleMapper.updateArticle(article);
       }
   }
   
   ```

   `articleService`:

   ```java
   package club.msos.service;
   
   import club.msos.pojo.Article;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public interface articleService {
       List<Article> selectArticleDesc();
   
       List<Article> selectArticle(Article article);
   
       List<Article> selectArticleByTitle(Article article);
   
       int deleteArticle(Integer article_id);
   
       int insertArticle(Article article);
   
       int updateArticle(Article article);
   }
   
   ```

   2. `commentServiceImpl`

   ```java
   package club.msos.service;
   
   import club.msos.pojo.Comment;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public class commentServiceImpl implements commentService{
   
       @Autowired
       club.msos.dao.commentMapper commentMapper;
       @Override
       public List<Comment> selectComment(Comment comment) {
           return commentMapper.selectComment(comment);
       }
   
       @Override
       public int deleteComment(Integer comment_id) {
           return commentMapper.deleteComment(comment_id);
       }
   
       @Override
       public int insertComment(Comment comment) {
           return commentMapper.insertComment(comment);
       }
   
       @Override
       public int updateComment(Comment comment) {
           return commentMapper.updateComment(comment);
       }
   }
   
   ```

   `commentService`:

   ```java
   package club.msos.service;
   
   import club.msos.pojo.Comment;
   import org.springframework.stereotype.Service;
   
   import java.util.List;
   
   @Service
   public interface commentService {
       List<Comment> selectComment(Comment comment);
   
       int deleteComment(Integer comment_id);
   
       int insertComment(Comment comment);
   
       int updateComment(Comment comment);
   }
   ```

   3. `linksServiceImpl`:

      ```java
      package club.msos.service;
      
      import club.msos.pojo.Links;
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Service;
      
      import java.util.List;
      
      @Service
      public class linksServiceImpl implements linksService{
      
          @Autowired
          club.msos.dao.linksMapper linksMapper;
          @Override
          public List<Links> selectLinks(Links links) {
              return linksMapper.selectLinks(links);
          }
      
          @Override
          public List<Links> selectLinksByTitle(Links links) {
              return linksMapper.selectLinksByTitle(links);
          }
      
          @Override
          public int deleteLinks(Integer links_id) {
              return linksMapper.deleteLinks(links_id);
          }
      
          @Override
          public int updateLinks(Links links) {
              return linksMapper.updateLinks(links);
          }
      
          @Override
          public int insertLinks(Links links) {
              return linksMapper.insertLinks(links);
          }
      }
      
      ```

      `linksService`:

      ```java
      package club.msos.service;
      
      import club.msos.pojo.Links;
      import org.springframework.stereotype.Service;
      
      import java.util.List;
      
      @Service
      public interface linksService {
      
          List<Links> selectLinks(Links links);
      
          List<Links> selectLinksByTitle(Links links);
      
          int deleteLinks(Integer links_id);
      
          int updateLinks(Links links);
      
          int insertLinks(Links links);
      }
      
      ```

      4. `longinCountService`:

      ```java
      package club.msos.service;
      
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.data.redis.core.RedisTemplate;
      import org.springframework.scheduling.annotation.Scheduled;
      import org.springframework.stereotype.Service;
      
      import java.util.Date;
      
      @Service
      public class longinCountService {
      
          @Autowired
          RedisTemplate redisTemplate;
          @Scheduled(cron = "0 0 0 * * ?")
          public void longinCount(){
              Date date = new Date();
              int day = date.getDay();
              String Day;
              if (day==1){
                  Day="Monday";
              }else if(day==2){
                  Day="Tuesday";
              }else if(day==3){
                  Day="Wednesday";
              }else if(day==4){
                  Day="Thursday";
              }else if(day==5){
                  Day="Friday";
              }else if(day==6){
                  Day="Saturday";
              }else {
                  Day="Sunday";
              }
              redisTemplate.opsForHash().put("DayTime",Day,0);
          }
      }
      ```

      

5. `messageServiceImpl`:

````java
package club.msos.service;

import club.msos.pojo.Message;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class messageServiceImpl implements messageService{

    @Autowired
    club.msos.dao.messageMapper messageMapper;
    @Override
    public List<Message> selectMessage(Message message) {
        return messageMapper.selectMessage(message);
    }

    @Override
    public int deleteMessage(Integer message_id) {
        return messageMapper.deleteMessage(message_id);
    }

    @Override
    public int insertMessage(Message message) {
        return messageMapper.insertMessage(message);
    }

    @Override
    public int updateMessage(Message message) {
        return messageMapper.updateMessage(message);
    }
}

````

`messageService`:

````java
package club.msos.service;

import club.msos.pojo.Message;
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public interface messageService {
    List<Message> selectMessage(Message message);

    int deleteMessage(Integer message_id);

    int insertMessage(Message message);

    int updateMessage(Message message);
}

````

6. `updateArticleServiceImpl`:

```java
package club.msos.service;

import club.msos.pojo.UpdateArticle;
import org.apache.ibatis.annotations.Mapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class updateArticleServiceImpl implements updateArticleService{
    @Autowired
    club.msos.dao.updateArticleMapper updateArticleMapper;

    @Override
    public List<UpdateArticle> selectUpdateArticle() {
        return updateArticleMapper.selectUpdateArticle();
    }

    @Override
    public int insertUpdateArticle(UpdateArticle updateArticle) {
        return updateArticleMapper.insertUpdateArticle(updateArticle);
    }
}

```

` updateArticleService`:

```java
package club.msos.service;

import club.msos.pojo.UpdateArticle;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public interface updateArticleService {

    List<UpdateArticle> selectUpdateArticle();

    int insertUpdateArticle(UpdateArticle updateArticle);
}

```

7. `updateUserServiceImpl`:

```java
package club.msos.service;

import club.msos.pojo.UpdateUser;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class updateUserServiceImpl implements updateUserService{

    @Autowired
    club.msos.dao.updateUserMapper updateUserMapper;

    @Override
    public List<UpdateUser> selectUpdateUser() {
        return updateUserMapper.selectUpdateUser();
    }

    @Override
    public int insertUpdateUser(UpdateUser updateUser) {
        return updateUserMapper.insertUpdateUser(updateUser);
    }
}

```

`updateUserService`:

```java
package club.msos.service;

import club.msos.pojo.UpdateUser;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public interface updateUserService {

    List<UpdateUser> selectUpdateUser();

    int insertUpdateUser(UpdateUser updateUser);
}

```

8. `userServiceImpl`:

```java
package club.msos.service;

import club.msos.pojo.User;
import org.apache.ibatis.annotations.Mapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@Mapper
public class userServiceImpl implements userService{

    @Autowired
    club.msos.dao.userMapper userMapper;

    @Override
    public List<User> selectUser(User user) {
        return userMapper.selectUser(user);
    }

    @Override
    public int insertUser(User user) {
        return userMapper.insertUser(user);
    }

    @Override
    public int updateUser(User user) {
        return userMapper.updateUser(user);
    }

    @Override
    public int deleteUser(String user_id) {
        return userMapper.deleteUser(user_id);
    }
}

```

`userService`：

```java
package club.msos.service;

import club.msos.pojo.User;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public interface userService {

    List<User> selectUser(User user);

    int insertUser(User user);

    int updateUser(User user);

    int deleteUser(String user_id);
}

```

------

## Util工具类实现

1. `dateTime` 时间日期工具类

```java
package club.msos.util;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.TimeZone;

public class dateTime {
    public String getTime(){
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        dateFormat.setTimeZone(TimeZone.getTimeZone("Etc/GMT-8"));
        return dateFormat.format(new Date());
    }
}
```

2. `emileSend`:

```java
package club.msos.util;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.mail.javamail.JavaMailSenderImpl;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.scheduling.annotation.Async;

import javax.mail.MessagingException;
import javax.mail.internet.MimeMessage;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Configuration
@Async
public class emileSend {

    @Autowired
    JavaMailSenderImpl mailSender;

    public  void Send(String user_email,String user_id) throws MessagingException {

        MimeMessage mimeMessage = mailSender.createMimeMessage();
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage,true);
        messageHelper.setSubject("亲爱的"+user_id+"您正在通过邮箱修改密码");
//        String url = "<a href=http://localhost:8088/ToUpdatePassword?username=" + name + " style='color:red'/>点击此处前往修改密码!</a>";
        messageHelper.setText("<a href=http://msos:8888/ToUpdatePassword?user_id="+user_id+" style='color:red'/>点击此处前往修改密码!</a>",true);
        messageHelper.setFrom("2574833532@qq.com");
        messageHelper.setTo(user_email);

        mailSender.send(mimeMessage);
    }

}

```

3. `IP`:获取ip

```java
package club.msos.util;

import org.apache.catalina.connector.Request;
import org.springframework.http.HttpRequest;

import javax.servlet.http.HttpServletRequest;
import java.net.InetAddress;

public class GetIp {

    HttpServletRequest request;

    public GetIp(HttpServletRequest request) {
        this.request = request;
    }

    public void setRequest(HttpServletRequest request) {
        this.request = request;
    }

    public String getIpAddress() {

        String ip = request.getHeader("x-forwarded-for");
        if (ip == null || ip.length() == 0 || "unknow".equalsIgnoreCase(ip)) {
            ip = request.getHeader("Proxy-Client-IP");
        }
        if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {
            ip = request.getHeader("WL-Proxy-Client-IP");
        }
        if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {
            ip = request.getRemoteAddr();
            if (ip.equals("127.0.0.1")) {
                //根据网卡取本机配置的IP
                InetAddress inet = null;
                try {
                    inet = InetAddress.getLocalHost();
                } catch (Exception e) {
                    e.printStackTrace();
                }
                ip = inet.getHostAddress();
            }
        }
        // 多个代理的情况，第一个IP为客户端真实IP,多个IP按照','分割
        if (ip != null && ip.length() > 15) {
            if (ip.indexOf(",") > 0) {
                ip = ip.substring(0, ip.indexOf(","));
            }
        }
        return ip;
    }
}

```

4. `JwtToken`:

```java
package club.msos.util;

import com.auth0.jwt.JWT;
import com.auth0.jwt.JWTVerifier;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.interfaces.DecodedJWT;

import java.util.Date;
import java.util.HashMap;
import java.util.Map;

public class JwtToken {
    private static final long EXPIRE_TIME = 15 * 60 * 1000;
    private static final String TOKEN_SECRET = "qqdqylyq";

    /**
     * 生成签名，15分钟过期
     */
    public static String createToken(String user_id) {
        try {
            Date date = new Date(System.currentTimeMillis() + EXPIRE_TIME);
            Algorithm algorithm = Algorithm.HMAC256(TOKEN_SECRET);
            Map<String, Object> header = new HashMap<>(2);
            header.put("Type", "Jwt");
            header.put("alg", "HS256");
            return JWT.create()
                    .withHeader(header)
                    .withClaim("user_id", user_id)
                    .withExpiresAt(date)
                    .sign(algorithm);
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
    /**
     * 检验token是否正确
     * @param **token**
     */
    public static String isToken(String token) {
            Algorithm algorithm = Algorithm.HMAC256(TOKEN_SECRET);
            JWTVerifier verifier = JWT.require(algorithm).build();
            DecodedJWT jwt = verifier.verify(token);
            String user_id = jwt.getClaim("user_id").asString();
            return user_id;
    }
}
```

5. `Load`

```java
package club.msos.util;
import org.springframework.util.ResourceUtils;

import java.io.*;

public class Load {
    private static String  path;

    static {
        try {
            //path = ResourceUtils.getURL("classpath:").getPath()+ "static/image";
            path="/usr/local/Blog.jar/BOOT-INF/classes/static/image";
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * @param :图片上传
     */
    public void upload(File uploadFile, String fileName) throws UnsupportedEncodingException {
        path = java.net.URLDecoder.decode(path, "utf-8");
        System.out.println(path);
        FileOutputStream fos = null;
        BufferedOutputStream bos = null;
        FileInputStream is = null;
        BufferedInputStream bis = null;
        File file = new File(path);
        if(!file.exists()){
            file.mkdirs();
        }
        File f = new File(path+"/"+fileName+".jpg");
        try {
            is = new FileInputStream(uploadFile);
            bis = new BufferedInputStream(is);
            fos = new FileOutputStream(f);
            bos = new BufferedOutputStream(fos);
            byte[] bt = new byte[4096];
            int len;
            while((len = bis.read(bt))>0){
                bos.write(bt, 0, len);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            try {
                if(null != bos){
                    bos.close();
                    bos = null;}
                if(null != fos){
                    fos.close();
                    fos= null;
                }
                if(null != is){
                    is.close();
                    is=null;
                }

                if (null != bis) {
                    bis.close();
                    bis = null;
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }

}

```

6. `ossUtil`

```java
package club.msos.util;

import com.aliyun.oss.OSSClient;
import com.aliyun.oss.model.ObjectMetadata;
import com.aliyun.oss.model.PutObjectResult;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.web.multipart.MultipartFile;

import java.io.IOException;
import java.io.InputStream;
import java.net.URL;
import java.util.*;

/**
 * 阿里云OSS服务器工具类
 */
@Component
public class OssUtil {

    //---------变量----------
    protected static final Logger log = LoggerFactory.getLogger(OssUtil.class);

    @Value("${aliyun.oss.endpoint}")
    private String endpoint;
    @Value("${aliyun.oss.accessKeyId}")
    private String accessKeyId;
    @Value("${aliyun.oss.accessKeySecret}")
    private String accessKeySecret;
    @Value("${aliyun.oss.bucketName}")
    private String bucketName;

    //文件存储目录
    private String filedir = "/";

    /**
     * 1、单个文件上传
     * @param file
     * @return 返回完整URL地址
     */
    public String uploadFile(MultipartFile file) {
        String fileUrl = uploadImg2Oss(file);
        String str = getFileUrl(fileUrl);
        return  str.trim();
    }

    /**
     * 1、单个文件上传(指定文件名（带后缀）)
     * @param file
     * @return 返回完整URL地址
     */
    public String uploadFile(MultipartFile file,String fileName) {
        try {
            InputStream inputStream = file.getInputStream();
            this.uploadFile2OSS(inputStream, fileName);
            return fileName;
        }
        catch (Exception e) {
            return "上传失败";
        }
    }

    /**
     * 2、多文件上传
     * @param fileList
     * @return 返回完整URL，逗号分隔
     */
    public String uploadFile(List<MultipartFile> fileList) {
        String  fileUrl = "";
        String  str = "";
        String  photoUrl = "";
        for(int i = 0;i< fileList.size();i++){
            fileUrl = uploadImg2Oss(fileList.get(i));
            str = getFileUrl(fileUrl);
            if(i == 0){
                photoUrl = str;
            }else {
                photoUrl += "," + str;
            }
        }
        return photoUrl.trim();
    }

    /**
     * 3、通过文件名获取文完整件路径
     * @param fileUrl
     * @return 完整URL路径
     */
    public String getFileUrl(String fileUrl) {
        if (fileUrl !=null && fileUrl.length()>0) {
            String[] split = fileUrl.split("/");
            String url =  this.getUrl(this.filedir + split[split.length - 1]);
            return url;
        }
        return null;
    }

    //获取去掉参数的完整路径
    private String getShortUrl(String url) {
        String[] imgUrls = url.split("\\?");
        return imgUrls[0].trim();
    }

    // 获得url链接
    private String getUrl(String key) {
        // 设置URL过期时间为20年  3600l* 1000*24*365*20
        Date expiration = new Date(new Date().getTime() + 3600l * 1000 * 24 * 365 * 20);
        // 生成URL
        OSSClient ossClient = new OSSClient(endpoint, accessKeyId, accessKeySecret);
        URL url = ossClient.generatePresignedUrl(bucketName, key, expiration);
        if (url != null) {
            return  getShortUrl(url.toString());
        }
        return null;
    }

    // 上传文件
    private String uploadImg2Oss(MultipartFile file) {
        //1、限制最大文件为20M
        if (file.getSize() > 1024 * 1024 *20) {
            return "图片太大";
        }

        String fileName = file.getOriginalFilename();
        String suffix = fileName.substring(fileName.lastIndexOf(".")).toLowerCase(); //文件后缀
        String uuid = UUID.randomUUID().toString();
        String name = uuid + suffix;

        try {
            InputStream inputStream = file.getInputStream();
            this.uploadFile2OSS(inputStream, name);
            return name;
        }
        catch (Exception e) {
            return "上传失败";
        }
    }


    // 上传文件（指定文件名）
    private String uploadFile2OSS(InputStream instream, String fileName) {
        String ret = "";
        try {
            //创建上传Object的Metadata
            ObjectMetadata objectMetadata = new ObjectMetadata();
            objectMetadata.setContentLength(instream.available());
            objectMetadata.setCacheControl("no-cache");
            objectMetadata.setHeader("Pragma", "no-cache");
//            objectMetadata.setContentType(getcontentType(fileName.substring(fileName.lastIndexOf("."))));
//            System.out.println(objectMetadata);
            objectMetadata.setContentDisposition("inline;filename=" + fileName);
            //上传文件
            OSSClient ossClient = new OSSClient(endpoint, accessKeyId, accessKeySecret);
            PutObjectResult putResult = ossClient.putObject(bucketName, fileName+".jpg", instream, objectMetadata);
            ret = putResult.getETag();
        } catch (IOException e) {
            log.error(e.getMessage(), e);
        } finally {
            try {
                if (instream != null) {
                    instream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return ret;
    }

   private static String getcontentType(String FilenameExtension) {
       if (FilenameExtension.equalsIgnoreCase(".bmp")) {
           return "image/bmp";
       }
       if (FilenameExtension.equalsIgnoreCase(".gif")) {
           return "image/gif";
       }
       if (FilenameExtension.equalsIgnoreCase(".jpeg") ||
               FilenameExtension.equalsIgnoreCase(".jpg") ||
               FilenameExtension.equalsIgnoreCase(".png")) {
           return "image/jpeg";
       }

       return "image/jpeg";
   }
}
```

7. `uuid`

```java
package club.msos.util;
import java.text.DecimalFormat;

public class uuid {

    public static String getUUID()
    {
        java.util.Random r=new java.util.Random();
        //如生成的随机位数不足6位则自动加零补充
        DecimalFormat g=new DecimalFormat("1000000");
        //返回时间增量+随机数的序列
        return String.format("%s%s",System.currentTimeMillis(),g.format(r.nextInt(1000000)));
    }
}
```

## Mybatis配置

> 持久化映射层,servive业务逻辑处理层

1.`articleMapper` 配置

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="club.msos.dao.articleMapper">
<select id="selectArticleDesc"  resultType="Article">
    select * from article
    order by article_views desc
        limit 6
</select>
    <select id="selectArticle" parameterType="Article" resultType="Article">
        select * from article
        <where>
            <if test="article_id!=null">article_id=#{article_id}</if>
            <if test="article_title!=null">and article_title=#{article_title}</if>
            <if test="user_id!=null">and user_id=#{user_id}</if>
            <if test="article_content!=null">and article_content=#{article_content}</if>
            <if test="article_views!=null">and article_views=#{article_views}</if>
            <if test="article_comment_count!=null">and article_comment_count=#{article_comment_count}</if>
            <if test="article_time!=null">and article_time=#{article_time}</if>
            <if test="article_type!=null">and article_type=#{article_type}</if>
        </where>
    </select>
    <select id="selectArticleByTitle" parameterType="Article" resultType="Article">
        select * from article
        where article_title like concat('%',#{article_title},'%')
    </select>
    <delete id="deleteArticle" parameterType="int">
        delete
        from article
        where article_id=#{article_id}
    </delete>
    <update id="updateArticle" parameterType="Article">
        update article
        <set>
            <if test="article_title!=null">article_title=#{article_title},</if>
            <if test="user_id!=null">user_id=#{user_id},</if>
            <if test="article_content!=null">article_content=#{article_content},</if>
            <if test="article_views!=null">article_views=#{article_views},</if>
            <if test="article_comment_count!=null">article_comment_count=#{article_comment_count},</if>
            <if test="article_time!=null">article_time=#{article_time},</if>
            <if test="article_type!=null">article_type=#{article_type}</if>
        </set>
        where article_id=#{article_id}
    </update>
    <insert id="insertArticle" parameterType="Article">
        insert into article(article_id,article_title,user_id,article_content,article_views,article_comment_count,article_time,article_type)
        values (#{article_id},#{article_title},#{user_id},#{article_content},#{article_views},#{article_comment_count},#{article_time},#{article_type})
    </insert>
</mapper>
```

2. `commentMapper`配置

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="club.msos.dao.commentMapper">
    <select id="selectComment" parameterType="Comment" resultType="Comment">
        select * from comment
        <where>
            <if test="comment_id!=null">comment_id=#{comment_id}</if>
            <if test="user_id!=null">and user_id=#{user_id}</if>
            <if test="article_id!=null">and article_id=#{article_id}</if>
            <if test="comment_time!=null">and comment_time=#{comment_time}</if>
            <if test="comment_content!=null">and comment_content=#{comment_content}</if>
            <if test="comment_ip!=null">and comment_ip=#{comment_ip}</if>
        </where>
    </select>
    <delete id="deleteComment" parameterType="int">
        delete
        from comment
        where comment_id=#{comment_id}
    </delete>
    <update id="updateComment" parameterType="Comment">
        update comment
        <set>
            <if test="user_id!=null">user_id=#{user_id},</if>
            <if test="article_id!=null">article_id=#{article_id},</if>
            <if test="comment_time!=null">comment_time=#{comment_time},</if>
            <if test="comment_content!=null">comment_content=#{comment_content},</if>
            <if test="comment_ip!=null">comment_ip=#{comment_ip}</if>
        </set>
        where comment_id=#{comment_id}
    </update>
    <insert id="insertComment" parameterType="Comment">
        insert into comment(comment_id,user_id,article_id,comment_time,comment_content,comment_ip)
        values (#{comment_id},#{user_id},#{article_id},#{comment_time},#{comment_content},#{comment_ip})
    </insert>
</mapper>
```

3. `linksMapper`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="club.msos.dao.linksMapper">
       <select id="selectLinks" parameterType="Links" resultType="Links">
           select * from links
           <where>
               <if test="links_id!=null">links_id=#{links_id}</if>
               <if test="links_name!=null">and links_name=#{links_name}</if>
               <if test="links_title!=null">and links_title=#{links_title}</if>
               <if test="links_url!=null">and links_url=#{links_url}</if>
               <if test="links_img!=null">and links_img=#{links_img}</if>
           </where>
       </select>
       <select id="selectLinksByTitle" parameterType="Links" resultType="Links">
           select * from links
           where links_name like concat('%',#{links_name},'%')
       </select>
       <delete id="deleteLinks" parameterType="int">
           delete
           from links
           where links_id=#{links_id}
       </delete>
       <update id="updateLinks" parameterType="Links">
           update links
           <set>
               <if test="links_name!=null">links_name=#{links_name},</if>
               <if test="links_title!=null">links_title=#{links_title},</if>
               <if test="links_url!=null">links_url=#{links_url},</if>
               <if test="links_img!=null">links_img=#{links_img}</if>
           </set>
           where links_id=#{links_id}
       </update>
       <insert id="insertLinks" parameterType="Links">
           insert into links(links_id,links_name,links_title,links_url,links_img)
           values (#{links_id},#{links_name},#{links_title},#{links_url},#{links_img})
       </insert>
   </mapper>
   ```

   4. `messageMapper`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="club.msos.dao.messageMapper">
       <select id="selectMessage" parameterType="Message" resultType="Message">
           select * from message
           <where>
               <if test="message_id!=null">message_id=#{message_id}</if>
               <if test="user_id!=null">and user_id=#{user_id}</if>
               <if test="message_content!=null">and message_content=#{message_content}</if>
               <if test="message_time!=null">and message_time=#{message_time}</if>
               <if test="message_parant_id!=null">and message_parant_id=#{message_parant_id}</if>
               <if test="message_ip!=null">and message_ip=#{message_ip}</if>
           </where>
       </select>
       <delete id="deleteMessage" parameterType="int">
           delete
           from message
           where message_id=#{message_id}
       </delete>
       <update id="updateMessage" parameterType="Message">
           update message
           <set>
               <if test="user_id!=null">user_id=#{user_id},</if>
               <if test="message_content!=null">message_content=#{message_content},</if>
               <if test="message_time!=null">message_time=#{message_time},</if>
               <if test="message_parant_id!=null">message_parant_id=#{message_parant_id},</if>
               <if test="message_ip!=null">message_ip=#{message_ip}</if>
           </set>
           where message_id=#{message_id}
       </update>
       <insert id="insertMessage" parameterType="Message">
           insert into message(message_id,user_id,message_content,message_time,message_parant_id,message_ip)
           values (#{message_id},#{user_id},#{message_content},#{message_time},#{message_parant_id},#{message_ip})
       </insert>
   </mapper>
   ```

   5. `updateArticleMapper`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="club.msos.dao.updateArticleMapper">
       <select id="selectUpdateArticle" resultType="UpdateArticle">
           select * from updatearticle
       </select>
       <insert id="insertUpdateArticle" parameterType="UpdateArticle">
           insert into updatearticle(updateArticle_id,article_id,updateArticle_do,updateArticle_time,updateArticle_ip)
           values (#{updateArticle_id},#{article_id},#{updateArticle_do},#{updateArticle_time},#{updateArticle_ip})
       </insert>
   </mapper>
   ```

   6. `updateUserMapper`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="club.msos.dao.updateUserMapper">
   <select id="selectUpdateUser" resultType="UpdateUser">
       select * from updateuser
   </select>
       <insert id="insertUpdateUser" parameterType="UpdateUser">
           insert into updateuser(updateUser_id,user_id,updateUser_do,updateUser_time,updateUser_ip)
           values (#{updateUser_id},#{user_id},#{updateUser_do},#{updateUser_time},#{updateUser_ip})
       </insert>
   </mapper>
   ```

   7. `userMapper`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="club.msos.dao.userMapper">
   
       <select id="selectUser" parameterType="User" resultType="User">
           select * from tuser
          <where>
              <if test="user_id!=null">user_id=#{user_id}</if>
              <if test="user_password!=null">and user_password=#{user_password}</if>
              <if test="user_name!=null">and user_name=#{user_name}</if>
              <if test="user_email!=null">and user_email=#{user_email}</if>
              <if test="user_phone!=null">and user_phone=#{user_phone}</if>
              <if test="user_sex!=null">and user_sex=#{user_sex}</if>
              <if test="user_ip!=null">and user_ip=#{user_ip}</if>
              <if test="user_role!=null">and user_role=#{user_role}</if>
              <if test="user_birthday!=null">and user_birthday=#{user_birthday}</if>
          </where>
       </select>
       <delete id="deleteUser" parameterType="String">
           delete
           from tuser
           where user_id=#{user_id}
       </delete>
       <update id="updateUser" parameterType="User">
           update tuser
           <set>
               <if test="user_password!=null">user_password=#{user_password},</if>
               <if test="user_name!=null">user_name=#{user_name},</if>
               <if test="user_email!=null">user_email=#{user_email},</if>
               <if test="user_phone!=null">user_phone=#{user_phone},</if>
               <if test="user_sex!=null">user_sex=#{user_sex},</if>
               <if test="user_ip!=null">user_ip=#{user_ip},</if>
               <if test="user_role!=null">user_role=#{user_role},</if>
               <if test="user_birthday!=null">user_birthday=#{user_birthday}</if>
           </set>
           where user_id=#{user_id}
       </update>
       <insert id="insertUser" parameterType="User">
           insert into tuser(user_id,user_password,user_name,user_email,user_phone,user_sex,user_ip,user_role,user_birthday)
           values (#{user_id},#{user_password},#{user_name},#{user_email},#{user_phone},#{user_sex},#{user_ip},#{user_role},#{user_birthday})
       </insert>
   </mapper>
   ```

   ### Msos测试

   `启动类`

   ```
   package club.msos;
   
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.test.context.SpringBootTest;
   import org.springframework.data.redis.core.RedisTemplate;
   
   import java.util.Date;
   
   @SpringBootTest
   class MsosApplicationTests {
   
       @Autowired
       RedisTemplate redisTemplate;
       @Test
       void redisTest() {
   
   //        redisTemplate.opsForValue().set("username","501664112");
   //        System.out.println(redisTemplate.opsForValue().get("username"));
           Date date = new Date();
   //        int day = date.getDay();
   //        System.out.println(day);
           System.out.println(redisTemplate.opsForHash().get("DayTime", "Wednesday"));
           System.out.println(redisTemplate.opsForHash().values("DayTime"));
       }
   
   }
   ```

