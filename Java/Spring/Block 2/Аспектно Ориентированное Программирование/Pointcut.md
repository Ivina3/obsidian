Pointcut - выражение, описывающее где должен быть применен Advice.
Spring AOP используется AspectJ Pointcut expression language. Т.е. определенные правила в написании выражений для создания Pointcut.

execution( modifiers-pattern? **return-type-pattern** declaring-type-pattern? **method-name-pattern(parameters-pattern)** throws-pattern? )
```
@Before("execution(public void aop.UniLibrary.getBook())")  
public void beforeGetBookAdvice() {  
    System.out.println("попытка получить книгу");  
}
```

execution(public void get*()) - метод без параметра, где бы он ни находился, начинается на get.
execution(public void get*(..)) - с любым количеством параметров.
execution(public void getBook(aop.Book)) - если мы указываем объект в параметре, надо писать весь путь!

---
#### Объявление Pointcut
Для того, чтобы не пользоваться copy-paste когда для нескольких Advice-ов подходит один и тот же Pointcut, есть возможность объявить данный Pointcut и затем использовать его несколько раз.

> @Pointcut("pointcut_expression")
> private void pointcut_reference(){}

