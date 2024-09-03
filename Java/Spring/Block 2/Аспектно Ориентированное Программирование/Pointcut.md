Pointcut - выражение, описывающее где должен быть применен Advice.
Spring AOP используется AspectJ Pointcut expression language. Т.е. определенные правила в написании выражений для создания Pointcut.

execution( modifiers-pattern? **return-type-pattern** declaring-type-pattern? **method-name-pattern(parameters-pattern)** throws-pattern? )
```
@Before("execution(public void aop.UniLibrary.getBook())")  
public void beforeGetBookAdvice() {  
    System.out.println("попытка получить книгу");  
}
```