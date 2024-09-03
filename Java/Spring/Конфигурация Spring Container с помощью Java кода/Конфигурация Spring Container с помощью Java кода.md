
---
## Способ 1
```
@Configuration
@ComponentScan("spring")
public class MyConfig{
}
```
Аннотация @Configuration означает, что данный класс является конфигурацией.
С помощью аннотации @ComponentScan мы показываем, какой пакет нужно сканировать на наличие бинов и разных аннотаций.
```
public static void main(String[] args) {  
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);  
    Person person = context.getBean("personBean", Person.class);  
    context.close();  
}
```
---
## Способ 2
