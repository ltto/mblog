#spring bean循环依赖处理
##循环依赖是什么
>循环依赖其实就是循环引用，也就是两个或者两个以上的bean互相持有对方，最终形成闭环。比如A依赖于B，B依赖于C，C又依赖于A。如下图：
##spring注入方式
1. 构造方法注入
``` java 
 @Autowired
public BService(AService aService) {
    this.aService = aService;
}
```
>构造器的循环依赖问题无法解决，只能拋出`BeanCurrentlyInCreationException异常`
<br>
<br>
2. 字段注入
```java
 @Autowired                 
 private  AService aService;
```
>在解决属性循环依赖时，spring采用的是`提前暴露对象(读取缓存)`的方法。
> 使用3级缓存,只能解决`单例状态`下的循环依赖  因为`非单例bean spring不进行缓存`
### 具体步骤如下：
       1、Spring容器创建单例“circleA” Bean，首先根据无参构造器创建Bean，并暴露一个“ObjectFactory ”用于返回一个提前暴露一个创建中的Bean，并将“circleA” 标识符放到“当前创建Bean池”；然后进行setter注入“circleB”；
       2、Spring容器创建单例“circleB” Bean，首先根据无参构造器创建Bean，并暴露一个“ObjectFactory”用于返回一个提前暴露一个创建中的Bean，并将“circleB” 标识符放到“当前创建Bean池”，然后进行setter注入“circleC”；
       3、Spring容器创建单例“circleC” Bean，首先根据无参构造器创建Bean，并暴露一个“ObjectFactory ”用于返回一个提前暴露一个创建中的Bean，并将“circleC” 标识符放到“当前创建Bean池”，然后进行setter注入“circleA”；进行注入“circleA”时由于提前暴露了“ObjectFactory”工厂从而使用它返回提前暴露一个创建中的Bean；
4、最后在依赖注入“circleB”和“circleA”，完成setter注入。

##检测循环依赖
>检测循环依赖相对比较容易，Bean在创建的时候可以给该Bean打标，如果递归调用回来发现正在创建中的话，即说明了循环依赖了。
- - - - - - - - - - - - - - - - - - - 
##3月5日更新
循环依赖的字段注入时
需要如果类中存在加入`@Async`的方法 需要在`@Autowired`下加入 `@Lazy(value = true)`