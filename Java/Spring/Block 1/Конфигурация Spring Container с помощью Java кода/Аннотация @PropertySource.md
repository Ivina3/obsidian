```
@Value("${person.name}")
private String name;
---
@Comfiguration
@PropertySourse("classpath:myApp.properties")
public class MyConfig{...}
```
	Аннотация @PropertySourse указывает на property файл откуда мы можем использовать значения для полей