		- выполняется после окончания метода с основной логикой вне зависимости от того, завершается ли метод нормально или выбрасывается исключение.
```
@After("execution(* getStudents())")  
public void afterGetStudentsLoggingAdvice(JoinPoint joinPoint) {  
    System.out.println("логируем нормальное окончание getStudents или выброс исключения");  
}
---
логируем перед методом getStudents
start get students
логируем нормальное окончание getStudents или выброс исключения
Было поймано исключение java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
```

С помощью @After Advice невозможно:
	1) получить доступ к исключению, которое выбросилось из метода с основной логикой;
	2) получить доступ к возвращаемому методом результату.
Можно использовать JoinPoint