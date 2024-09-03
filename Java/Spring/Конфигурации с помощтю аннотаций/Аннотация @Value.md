Для внедрения строк и других значений. В этом случае в сеттерах нет необходимости, как это было при конфигурации с помощью XML.
```
@Value("Eva")  
private String name;  
@Value("18")  
private int age;
```
	всегда в ""
Можно использовать xml и properties
```
<context:property-placeholder location="classpath:myApplication.properties"/>
```
тогда:
```
@Value("${person.name}")  
private String name;  
@Value("${person.age}")  
private int age;
```
