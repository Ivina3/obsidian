@EnableAspectJAutoProxy - позволяет нам за кулисами использоваться Spring AOP Proxy.
```
@Configuration  
@ComponentScan("aop")  
@EnableAspectJAutoProxy  
public class MyConfig {  
}
```
