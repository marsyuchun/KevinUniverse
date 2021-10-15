# Spring回顾
## 什么是Spring
Spring是一个开源框架，2003 年兴起的一个轻量级的Java 开发框架，作者：Rod Johnson。  
Spring是为了解决企业级应用开发的复杂性而创建的，简化开发。

## Spring如何简化Java开发
1、基于POJO的轻量级和最小侵入性编程，所有东西都是bean；  
2、通过IOC，依赖注入（DI）和面向接口实现松耦合；  
3、基于切面（AOP）和惯例进行声明式编程；  
4、通过切面和模版减少样式代码，RedisTemplate，xxxTemplate；  

## Spring Boot的主要优点：
- 为所有Spring开发者更快的入门
- 开箱即用，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

# Springboot原理初探
## 自动配置
### pom.xml
- spring-boot-dependencies：核心依赖在父工程中！
- 我们在写或者引入一些Springboot依赖的时候，不需要指定版本，就因为有这些版本仓库

### 启动器
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```
- 启动器：说白了就是Springboot的启动场景
- 比如说spring-boot-starter-web，他就会帮我们自动导入web环境所有的依赖！
- springboot会将所有的功能场景，都变成一个个的启动器
- 我们要使用什么功能，就只需要找到对应的启动器就可以了 `starter`

### 主程序
```java
// @SpringBootApplication :标注这个类是一个springboot的应用
@SpringBootApplication
public class Springboot01HelloworldApplication {
    // 将springboot应用启动
    public static void main(String[] args) {
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }
}
```
- 注解  
    ```
    @SpringBootConfiguration : springboot的配置
        @Configuration： spring配置类
        @Component： 说明这也是一个spring的组件

    @EnableAutoConfiguration ： 自动配置
        @AutoConfigurationPackage : 自动配置包
            @Import(AutoConfigurationPackages.Registrar.class) : 导入选择器`包注册`
        @Import(AutoConfigurationImportSelector.class) : 自动配置导入选择
    ```



结论：springboot所有自动配置都是在启动的时候扫描并加载：spring.factories所有的自动配置类都在这里面，但是不一定生效，要判断条件是否成立，只要导入了对应的start，就有对应的启动器了，有了启动器，我们自动装配就会生效，然后就配置成功！

1、springboot在启动的时候，从类路径下 /META-INF/`spring.factories`获取指定的值；  
2、将这些自动配置的类导入容器，自动配置就会生效，帮我们进行自动配置！  
3、以前我们需要自动配置的东西，现在springboot帮我们做了   
4、整合javaEE，解决方案和自动配置的东西都在spring-boot-autoconfigure-2.5.5.jar这个包下   
5、他会把所有需要导入的组件，以类名的方式返回，这些组件就会被添加到容器中
6、容器中也会存在非常多的xxxAutoConfiguration的文件（@Bean），就是这些类给容器中导入了这个场景需要的所有组件，并自动配置，@Configuration，JavaConfig！
7、有了自动配置类，免去了我们手动编写配置文件的工作！


Springboot的两个关键点：
- 自动装配
- run方法：
    - 判断是普通项目还是web项目
    - 监听器
### Spring自动装配的原理！（精髓）
1、SpringBoot启动会加载大量的自动配置类  
2、我们看我们需要的功能有没有在SpringBoot默认写好的自动配置类当中  
3、我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件存在在其中，我们就不需要再手动配置了）  
4、给容器中自动配置类添加组件的时候，会从properties类中获取某些属性。我们只需要在配置文件中指定这些属性的值即可；  
xxxAutoCoonfiguration： 自动配置类  给容器中添加组件  
xxxProperties： 封装配置文件中相关属性  


## 全面接管SpringMVC的配置
















