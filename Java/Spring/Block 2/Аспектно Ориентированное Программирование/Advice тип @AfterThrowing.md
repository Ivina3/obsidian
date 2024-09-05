		-выполняется после окончания работы метода, если в нем было выброшено исключение.
```
@AfterThrowing("execution(* getStudents())")  
public void afterThrowingGetStudentsLoggingAdvice(JoinPoint joinPoint) {  
    System.out.println("логирум выброс исключения");  
}
---
public List<Student> getStudents() {  
    System.out.println("start get students");  
    System.out.println(students.get(3));  
    System.out.println("info about getStudents: ");  
    System.out.println(students);  
    return students;  
}
---
start get students
логирум выброс исключения
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
	at java.base/jdk.internal.util.Preconditions.outOfBounds(Preconditions.java:64)
	at java.base/jdk.internal.util.Preconditions.outOfBoundsCheckIndex(Preconditions.java:70)
	at java.base/jdk.internal.util.Preconditions.checkIndex(Preconditions.java:266)
	at java.base/java.util.Objects.checkIndex(Objects.java:361)
	at java.base/java.util.ArrayList.get(ArrayList.java:427)
```
---
```

public class test2 {  
    public static void main(String[] args) {  
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);  
        University university = context.getBean("university",University.class);  
        university.addStudent();  
        try {  
            List<Student> students = university.getStudents();  
            System.out.println(students);  
        } catch (Exception e) {  
            System.out.println("Было поймано исключение " + e);  
        }  
  
  
        context.close();  
    }  
}
---
логируем перед методом getStudents
start get students
логирум выброс исключения
Было поймано исключение java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3

Process finished with exit code 0
```
---
```
@AfterThrowing(pointcut = "execution(* getStudents())", throwing = "exeption")  
public void afterThrowingGetStudentsLoggingAdvice(Throwable exeption) {  
  
    System.out.println("логирум выброс исключения"+ exeption);  
}
---
логируем перед методом getStudents
start get students
логирум выброс исключенияjava.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
Было поймано исключение java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
```
@AfterThrowing Advice не влияет на протекание программы при выбрасывании исключения. С помощью @AfterThrowing Advice можно получить доступ к исключению, которое выбросилось из метода с основной логикой.