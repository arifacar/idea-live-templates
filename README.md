# Spring BOOT TEMPLATES

**spring-jpa-entity-lombok** 

Create JPA entity with lombok
```
@lombok.Data
@lombok.AllArgsConstructor
@lombok.NoArgsConstructor
@javax.persistence.Entity
public class $name$ {
    
    @javax.persistence.Id
    @javax.persistence.GeneratedValue(strategy = javax.persistence.GenerationType.IDENTITY)
    private java.lang.Long id;

    private java.lang.String name;
    
}
```

**spring-jpa-repository**

Create JPA repository with defined entity
```
@org.springframework.stereotype.Repository
public interface $entity$Repository extends org.springframework.data.repository.CrudRepository<$entity$, Long

    org.springframework.data.domain.Page<$entity$> findAll(org.springframework.data.domain.Pageable pageable);

}
```

**spring-jpa-sevice**

Create spring service with autowired repository and add first empty method
```
@org.springframework.stereotype.Service
class $entity$Service {

    private final $entity$Repository $entityVariable$Repository;

    @org.springframework.beans.factory.annotation.Autowired
    public $entity$Service($entity$Repository $entityVariable$Repository) {
        this.$entityVariable$Repository = $entityVariable$Repository;
    }

    public java.util.List<$entity$> findAll(int page){
        List<$entity$> $entityVariable$List = new java.util.ArrayList<>();

        return $entityVariable$List;
    }
}
```

**spring-jpa-findall**

Create to derive a Pageable instance from the request parameters and get all item list
```
org.springframework.data.domain.PageRequest pageRequest = PageRequest.of($page$ - 1, $size$);
java.util.List<$entity$> $entityVariable$List = $entityVariable$Repository.findAll(pageRequest).getContent();
```

**spring-jpa-controller**

Create spring controller with autowired service and add findAll get method
```
@org.springframework.web.bind.annotation.RestController
@org.springframework.web.bind.annotation.RequestMapping("/$endpoint$")
public class $entity$Controller {

    private final $entity$Service $entityVariable$Service;

    @org.springframework.beans.factory.annotation.Autowired
    public $entity$Controller($entity$Service $entityVariable$Service) {
        this.$entityVariable$Service = $entityVariable$Service;
    }

    @RequestMapping(value = "/{page}")
    public org.springframework.http.ResponseEntity<java.util.List<$entitiy$>> findById(@org.springframework.web.bind.annotation.PathVariable("page") int page) {
        return new ResponseEntity<>($entityVariable$Service.findAll(page), org.springframework.http.HttpStatus.OK);
    }
}
```

**jpa-h2-config**

Configure h2 database
```
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:tcp://localhost:$port$/~/$dbname$;
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.show-sql=true
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=update
```

**spring-get-mapping**

Get mapping method
```
@GetMapping(value = "/get$entity$/{$parameter$}")
public ResponseEntity<$entity$> get$entity$(@PathVariable("$parameter$") Long $parameter$) {
    return new ResponseEntity<>(userService.get$entity$($parameter$), HttpStatus.OK);
}
```

**spring-post-mapping**

Post mapping method
```
@PostMapping(value = "/$method$")
public ResponseEntity<$entity$> $method$(@RequestBody $entity$ $entityVariable$) {
    return new ResponseEntity<>($serviceName$.$method$($entityVariable$), HttpStatus.OK);
}
```

**java-validator-class**

Check all request for requested items
```
public class Validator {
    public static void validateUser(javax.servlet.http.HttpServletRequest request, $entity$ $entityVariable$) {
        org.springframework.util.Assert.isTrue($entityVariable$ != null, "$entityVariable$ bilgisi boş olamaz");
        Assert.isTrue("$headerAttributeValue$".equalsIgnoreCase(request.getHeader("$headerAttributeKey$")), "$errorMessage$");
    }
}
```

**spring-assert-true**

```
Assert.isTrue($express$, "$exceptionMessage$");
```
