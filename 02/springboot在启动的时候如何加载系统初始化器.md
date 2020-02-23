# Springboot 源码分析: 工厂加载机制 
## 概述
- 工厂加载机制是Spring内部提供的一个约定俗成的加载方式。
- 从classpath下多个jar包特定的位置(META-INF目录下定义Properties格式的spring.factories文件)读取文件并初始化类
- 文件内容必须以kv形式。即propertie类型
- key是类/接口的全名，value是实现多个以逗号分隔。

## 如何加载初始化器
- 从 [Spring Boot 启动原理解析](https://blog.csdn.net/qq_33249725/article/details/104457410/ "Spring Boot 启动原理解析") 可知在框架初始化的时候，就会加载初始化器 ApplicationContextInitializer。
- 具体流程如下图所示:

![SpringBoot源码分析-加载系统初始化器.jpg](https://i.loli.net/2020/02/23/8cv1sEj9k2dyhWZ.jpg)


