		- это точка или момент в выполняемой программе когда следует применять Advice. Т.е. это точка переплетения метода с бизнес-логикой и метода со служебным функционалом.
	Прописав Joint Point  в параметре метода Advice, мы получаем доступ к информации о сигнатуре и параметрах метода с бизнес-логикой.
```
@Before("aop.aspects.Mypointcuts.allGetMethods()")
public void methodeAdvice(JoinPoint joinPoint){
	MethodSignature methodSgnature = (MethodSignature) joinPoint.getSignature();
	Object[] arguments = joinPoint.getArgs();
}

---
@Before("aop.aspect.MyPointcuts.allAddMethode()")  
public void beforeAddBookLoggingAdvice(JoinPoint joinPoint) {  
    MethodSignature methodSignature = (MethodSignature) joinPoint.getSignature();  
    System.out.println(methodSignature);  
    System.out.println(methodSignature.getMethod());  
    System.out.println(methodSignature.getReturnType());  
    System.out.println(methodSignature.getName());  
  
    System.out.println("попытка получить книгу");  
    System.out.println("--------------------");  
}
---
void aop.UniLibrary.addBook(String,Book)
public void aop.UniLibrary.addBook(java.lang.String,aop.Book)
void
addBook
попытка получить книгу
```
---
```
@Before("aop.aspect.MyPointcuts.allAddMethode()")  
public void beforeAddBookLoggingAdvice(JoinPoint joinPoint) {  
    MethodSignature methodSignature = (MethodSignature) joinPoint.getSignature();  
    System.out.println(methodSignature);  
    System.out.println(methodSignature.getMethod());  
    System.out.println(methodSignature.getReturnType());  
    System.out.println(methodSignature.getName());  
    if(methodSignature.getName().equals("addBook")) {  
        Object[] args = joinPoint.getArgs();  
        for(Object arg : args) {  
            if(arg instanceof Book) {  
                Book book = (Book) arg;  
                System.out.println("Info about book: " + book.getName()+ " "+ book.getAuthor() + " " + book.getYear());  
            }  
            else if(arg instanceof String) {  
                System.out.println("Info about book: " + arg);  
            }  
        }  
    }  
    System.out.println("попытка получить книгу");  
    System.out.println("--------------------");  
}
---
void aop.UniLibrary.addBook(String,Book)
public void aop.UniLibrary.addBook(java.lang.String,aop.Book)
void
addBook
Info about book: Ira
Info about book: Evo4ka Evaa 1996
попытка получить книгу
```