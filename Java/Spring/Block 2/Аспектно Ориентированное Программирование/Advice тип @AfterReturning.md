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
```
@Component  
@Aspect  
public class UniversityLogginAspect {  
    @Before("execution(* getStudents())")  
    public void beforeGetStudentsLoggingAdvice(JoinPoint joinPoint) {  
        System.out.println("логируем перед методом getStudents");  
    }  
    @AfterReturning(pointcut = "execution(* getStudents())", returning = "students")  
    public void afterReturningGetStudentsLoggingAdvice(List<Student> students) {  
        Student firstStudent = students.get(0);  
        String firstName = firstStudent.getName();  
        firstName = "Mr." + firstName;  
        firstStudent.setName(firstName);  
        System.out.println("логируем после методом getStudents");  
    }  
}
---
логируем перед методом getStudents
info about getStudents: 
[Student{name='Ivi', course=3, averageGrade=5.0}, Student{name='Ivi2', course=1, averageGrade=3.0}, Student{name='Ivina', course=3, averageGrade=9.0}]
логируем после методом getStudents
[Student{name='Mr.Ivi', course=3, averageGrade=5.0}, Student{name='Ivi2', course=1, averageGrade=3.0}, Student{name='Ivina', course=3, averageGrade=9.0}]

```

@AfterReturning Advice выполняется только после нормального окончания метода с основной логикой, но до присвоения результата этого метода какой-либо переменной. Поэтому с помощью @Afterreturning Advice возможно изменять возвращаемый результат метода.
		**returning = "students" значит в параметрах тоже должен быть students!!!**
		