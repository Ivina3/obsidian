	- выполняется только после нормального окончания метода с основной логикой(таргет метода).
	- подходит для транзакционных действий
```
@Component  
@Aspect  
public class UniversityLogginAspect {  
    @Before("execution(* getStudents())")  
    public void beforeGetStudentsLoggingAdvice(JoinPoint joinPoint) {  
        System.out.println("логируем перед методом getStudents");  
    }  
    @AfterReturning("execution(* getStudents())")  
    public void afterReturningGetStudentsLoggingAdvice(JoinPoint joinPoint) {  
        System.out.println("логируем после методом getStudents");  
    }  
}

---
логируем перед методом getStudents
info about getStudents: 
[Student{name='Ivi', course=3, averageGrade=5.0}, Student{name='Ivi2', course=1, averageGrade=3.0}, Student{name='Ivina', course=3, averageGrade=9.0}]
логируем после методом getStudents
[Student{name='Ivi', course=3, averageGrade=5.0}, Student{name='Ivi2', course=1, averageGrade=3.0}, Student{name='Ivina', course=3, averageGrade=9.0}]
```

---
