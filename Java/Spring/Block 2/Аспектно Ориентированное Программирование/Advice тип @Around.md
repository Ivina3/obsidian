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
