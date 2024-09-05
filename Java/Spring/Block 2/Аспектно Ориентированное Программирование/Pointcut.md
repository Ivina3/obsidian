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
## Объявление Pointcut
Для того, чтобы не пользоваться copy-paste когда для нескольких Advice-ов подходит один и тот же Pointcut, есть возможность объявить данный Pointcut и затем использовать его несколько раз.

```
@Pointcut("pointcut_expression")
private void pointcut_reference(){}

---

@Before("pointcut_reference()")
public void advice_name(){ some code }
```

```
@Pointcut("execution(* get*())")  
private void allGetMethode(){}  
  
@Before("allGetMethode()")  
public void beforeGetBookLoggingAdvice() {  
    System.out.println("попытка получить книгу");  
}  
  
@Before("allGetMethode()")  
public void beforeGetBookSecurityAdvice() {  
    System.out.println("proverka prav");  
}
```
Плюсы объявления Pointcut:
- Возможность использования созданного Pointcut для множества Advice-ов
- Возможность быстрого изменения Pointcut expression для множества Advice-ов
- Возможность комбинирования Pointcut-ов
---
## Комбинирование Pointcut

Комбинирование Pointcut - это их объединение с помощью логических операторов && || !

```
@Pointcut("execution(* aop.UniLibrary.get*())")  
private void allGetMethodFromUniLibrary() {  
}  
@Pointcut("execution(* aop.UniLibrary.return*())")  
private void allReturnMethodFromUniLibrary() {  
}  
@Pointcut("allGetMethodFromUniLibrary() || allReturnMethodFromUniLibrary()")  
private void allGetAndReturnMethodFromUniLibrary() {}  
  
@Before("allGetAndReturnMethodFromUniLibrary()")  
public void beforeGetAndReturnMethodFromUniLibrary() {  
    System.out.println("Before all get and return method from uni-library");  
}  
@Before("allReturnMethodFromUniLibrary()")  
public void beforeReturnLoggingAdvice(){  
    System.out.println("Before Return Method from UniLibrary");  
}  
  
@Before("allGetMethodFromUniLibrary()")  
public void beforeGetLoggingAdvice(){  
    System.out.println("Before getting logging advice");  
}
```