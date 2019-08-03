# spring 事务传播级别
所以事务传播行为应该在`不同类的方法间传播`，
本类之间默认无法传播
可以通过获取代理的方式
``` java
@EnableAspectJAutoProxy(exposeProxy = true)
public class DemoApplication {
.....
....{
        AService o = (AService) AopContext.currentProxy();
    }
}
```