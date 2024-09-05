Если при вызове 1-го метода с бизнес-логикой срабатывают несколько Advice, то нет никакой гарантии в порядке выполнения этих Advice.
Создадим несколько классов:
```
public class MyPointcuts {  
    @Pointcut("execution(* get*())")  
    public void allGetMethode(){}  
}
---
@Component  
@Aspect  
@Order(1)  
public class LoggingAspect {  
  
  
    @Before("aop.aspect.MyPointcuts.allGetMethode()")  
    public void beforeGetBookLoggingAdvice() {  
        System.out.println("попытка получить книгу");  
    }

---
@Component  
@Aspect  
@Order(2)  
public class SecurityAspect {  
    @Before("aop.aspect.MyPointcuts.allGetMethode()")  
    public void beforeGetBookSecurityAdvice() {  
        System.out.println("proverka prav");  
    }  
}
---
@Component  
@Aspect  
@Order(3)  
public class ExceptionHandlingAspect {  
    @Before("aop.aspect.MyPointcuts.allGetMethode()")  
    public void beforeGetExceptionHandlingAdvice(){  
        System.out.println("Lovim popitki");  
    }  
}
```
Для соблюдения порядка такие Advice нужно распределять по отдельным упорядоченным Aspect-ам.
@Order(2) - чем меньше число, тем выше приоритет. 