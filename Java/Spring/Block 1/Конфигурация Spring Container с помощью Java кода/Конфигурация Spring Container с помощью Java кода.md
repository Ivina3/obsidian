
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
```
@Configuration  
public class MyConfig {  
  
    @Bean  
    public Pet catBean(){  
        return new Cat();  
    }  
}

---

public static void main(String[] args) {  
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);  
    Pet cat = context.getBean("catBean", Pet.class);  
  
    //        Person person = context.getBean("personBean", Person.class);  
    context.close();  
}


---

@Configuration  
public class MyConfig {  
  
    @Bean  
    @Scope("singleton")  
    public Pet catBean(){  
        return new Cat();  
    }  
  
    @Bean  
    public Person personBean(){  
        return new Person(catBean());  
    }  
}
```
- Данный способ не использует сканирование пакета и поиск бинов. Здесь бины описываются в конфиг классе.
- Данный способ не использует аннотацию @Autowired. Здесь зависимости прописываются вручную.
- Название метода - это bean id.
- Аннотация @Bean перехватывает все обращения к бину и регулирует его создание.