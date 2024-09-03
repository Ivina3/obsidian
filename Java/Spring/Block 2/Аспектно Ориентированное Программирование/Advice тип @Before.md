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

---
## Advice типы
- Before - выполняется до метода с основной логикой
- Afterreturning - выполняется только после нормального окончания метода с основной логикой.
- After throwing - выполняется после окончания метода с основной логикой только, если было выброшено исключение.
- After/ After finally - выполняется после окончания метода с основной логикой.
- Around - выполняется до и после метода с основной логикой.