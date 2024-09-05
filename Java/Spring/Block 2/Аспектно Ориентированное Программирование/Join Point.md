		- это точка или момент в выполняемой программе когда следует применять Advice. Т.е. это точка переплетения метода с бизнес-логикой и метода со служебным функционалом.
	Прописав Joint Point  в параметре метода Advice, мы получаем доступ к информации о сигнатуре и параметрах метода с бизнес-логикой.
```
@Before("aop.aspects.Mypointcuts.allGetMethods()")
public void methodeAdvice(JoinPoint joinPoint){
	MethodSignature methodSgnature = (MethodSignature) joinPoint.getSignature();
	Object[] arguments = joinPoint.getArgs();
}
```