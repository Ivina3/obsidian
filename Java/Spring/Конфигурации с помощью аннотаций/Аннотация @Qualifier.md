Для предотвращения  выброса исключения - использование @Autowired подходящих по типу бинов больше 1 - можно конкретно указать, какой бин должен внедрен.
```
@Autowired  
@Qualifier("dog")  
public void setPet(Pet pet) {  
    System.out.println("Pet set");  
    this.pet = pet;  
}
```

для конструктора - мы пишем как для параметра:
```
@Autowired  
@Qualifier("dog")  
public Person(@Qualifier("dog")Pet pet) {  
    System.out.println("Pet set");  
    this.pet = pet;  
}
```
