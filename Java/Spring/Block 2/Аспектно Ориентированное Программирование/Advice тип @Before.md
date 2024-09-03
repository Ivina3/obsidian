@EnableAspectJAutoProxy - позволяет нам за кулисами использоваться Spring AOP Proxy.
```
@Configuration  
@ComponentScan("aop")  
@EnableAspectJAutoProxy  
public class MyConfig {  
}
```
@Aspect - говорит о том, что это не простой класс,  а Aspect. Поэтому к данному классу Spring будет относиться по другому.
```
@Component  
@Aspect  
public class LoggingAspect {  
}
```
Aspect - класс, отвечающий за сквозную функциональность.