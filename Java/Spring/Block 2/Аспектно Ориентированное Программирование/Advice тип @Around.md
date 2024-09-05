		- выполняется до и после метода с основной логикой.
С помощью @Around Advice возможно:
	1) произвести какие-либо действия до работы target метода;
	2) произвести какие-либо действия после работы target метода;
	3) получить результат работы target метода/изменить его;
	4) предпринять какие-либо действия, если из target метода выбрасывается исключение. 
```
@Component  
@Aspect  
public class NewLoggingAspect {  
    @Around("execution(public String returnBook())")  
    public Object aroundReturnBookLiggingAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {  
        System.out.println("try return book -_-");  
        Object targetMethodresult = proceedingJoinPoint.proceed();  
  
        System.out.println("return book success -_-");  
        return targetMethodresult;  
    }  
}
---
  
public class test3 {  
    public static void main(String[] args) {  
        System.out.println("main start");  
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);  
       UniLibrary uniLibrary = context.getBean("uniLibrary", UniLibrary.class);  
       String bookName = uniLibrary.returnBook();  
        System.out.println("return "+bookName);  
  
        context.close();  
        System.out.println("main end");  
    }  
}
---
main start
try return book -_-
вернем книгу 
return book success -_-
return Война и мир
main end
```
---
## Работа с исключениями
Можно предпринять следующие действия, если из target метода выбрасываются исключение:
	- ничего не делать
	- обрабатывать исключение
	- пробрасывать исключение дальше
Example 2
```
@Around("execution(public String returnBook())")  
public Object aroundReturnBookLiggingAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {  
    System.out.println("try return book -_-");  
    Object targetMethodresult= null;  
    try {  
        targetMethodresult = proceedingJoinPoint.proceed();  
    } catch (Exception e) {  
        System.out.println("around " + e);  
        targetMethodresult = "неизвестое значение книги";  
    }  
      
    System.out.println("return book success -_-");  
    return targetMethodresult;  
}
---
main start
try return book -_-
around java.lang.ArithmeticException: / by zero
return book success -_-
return неизвестое значение книги
main end
---
public class test3 {  
    public static void main(String[] args) {  
        System.out.println("main start");  
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);  
       UniLibrary uniLibrary = context.getBean("uniLibrary", UniLibrary.class);  
       String bookName = uniLibrary.returnBook();  
        System.out.println("return "+bookName);  
  
        context.close();  
        System.out.println("main end");  
    }  
}
```
Example 3
```
@Component  
@Aspect  
public class NewLoggingAspect {  
    @Around("execution(public String returnBook())")  
    public Object aroundReturnBookLiggingAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {  
        System.out.println("try return book -_-");  
        Object targetMethodresult= null;  
        try {  
            targetMethodresult = proceedingJoinPoint.proceed();  
        } catch (Exception e) {  
            System.out.println("around " + e);  
            targetMethodresult = proceedingJoinPoint.proceed();  
            throw e;  
        }  
  
        System.out.println("return book success -_-");  
        return targetMethodresult;  
    }  
}
---
main start
try return book -_-
around java.lang.ArithmeticException: / by zero
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at aop.UniLibrary.returnBook(UniLibrary.java:22)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:569)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:355)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:196)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
```