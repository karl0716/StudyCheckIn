# SpringBoot源码分析 - 监听器的实现
## 监听器模式
 我们要先了解监听器的设计模式的要素:
    1. 事件
    2. 监听器
    3. 广播器
    4. 触发机制

- 图解:

![SpringBoot源码分析-监听器模式图解.jpg](https://i.loli.net/2020/02/23/KIZc6LdkmNvSRYl.jpg)

## SpringBoot 系统监听器的实现
### 系统监听器 - ApplicationListener
- 其主要作用是监听事件
- 源码如下所示

``` java
@FunctionalInterface
public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {
	/**
	 * Handle an application event.
	 * @param event the event to respond to
	 */
	void onApplicationEvent(E event);
}
```
- 源码解读:
    - 01 首先是一个函数式接口,只有一个抽象方法 onApplicationEvent
    - 02 EventListener为空实现，只是声明其子类都是事件监听器
    - 03 ApplicationListener<E extends ApplicationEven> 泛型定义其监听的事件是ApplicationEven的子类。

    
### 广播器 - ApplicationEventMulticaster
- 其主要作用是管理监听器和广播事件
- 其源码主要有三种接口 添加/删除/监听器和广播事件

### 系统事件
- 有很多事件，其中的关系如下图所示:
![事件类型类图.jpg](https://i.loli.net/2020/02/24/UoutbvQxXPhDmy7.jpg)

### SpringBoot启动的时候事件发生顺序

- 框架启动的时候事件发布顺序如下图所示:

![SpringBoot源码分析-SpringBoot框架启动事件发送顺序.jpg](https://i.loli.net/2020/02/23/LWZp2fyxCN9hQI3.jpg)
- 具体的流程可以参考 [Spring Boot 启动原理解析](https://blog.csdn.net/qq_33249725/article/details/104457410/ "Spring Boot 启动原理解析")  进行对比理解。

### 监听器的注册
- 源码如下所示：
![加载监听器.jpg](https://i.loli.net/2020/02/24/cwel7f2KkQUh9sj.jpg)

- 其注册流程和系统初始化器注册流程一直，只是传入的对象不同而已。具体的流程可参看 [Springboot 源码分析: 工厂加载机制以及如何加载系统初始化器](https://blog.csdn.net/qq_33249725/article/details/104460404/ "Springboot 源码分析: 工厂加载机制以及如何加载系统初始化器") 

### 监听器的触发机制
- 流程如下图所示:
![SpringBoot源码分析-监听器的触发机制01.jpg](https://i.loli.net/2020/02/24/WYSofx3yPli8zcV.jpg)

- 简单的流程图

![SpringBoot源码分析-监听器的触发机制02.jpg](https://i.loli.net/2020/03/01/IlZuzbvm9itMOG3.jpg)

