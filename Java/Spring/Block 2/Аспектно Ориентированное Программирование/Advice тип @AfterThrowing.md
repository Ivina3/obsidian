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