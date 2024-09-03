Scope (область видимости) определяет:
- жизненный цикл бина
- возможное количество создаваемых бинов
Разновидность bean scope:
1. Singletone - default 
2. Prototype
3. Request
4. Session
5. Global-session
---
##### Singletone -  дефолтный scope
	1. Такой бин создается сразу после прочтения Spring Container-ом конфиг файла
	2. Является общим для всех, кто запросит его у Spring Container
	3. Подходит для stateless объектов
```
	<bean id="myPet"
		class="ioc.Dog"
		scope="singleton">
		</bean>
```
	*короче создает только один объект и все переменные от этого бина ссылаются на один объект*

---
##### Prototype 
	1. Такой бин создается только после обращения к Spring Container с помощью метода getBean
	2. Для каждого такого обращения создается новый бин в Spring Container
	3. Подходит для stateful объектов
```
	<bean id="myPet"
		class="ioc.Dog"
		scope="prototype">
		</bean>
```