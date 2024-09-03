
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