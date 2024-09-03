```
@Component  
@Scope("singleton")
```
---
## Init, Destroy
## @PostConstruct, @PreDestroy

```
@PostConstruct  
public void init(){  
    System.out.println("init");  
}  
@PreDestroy  
public void destroy(){  
    System.out.println("destroy");  
}
```