# IDEA LIVE TEMPLATES 
These are the [IntelliJ IDEA Live Templates](https://www.jetbrains.com/help/idea/using-live-templates.html) that I’ve used in Spring Boot applications.

Copy springboot.xml content (right click and select copy, or ctrl+c), and paste it into your "Template Group". Right click one of the groups and select Paste. This is easiest way. 

[Click here](https://www.youtube.com/watch?v=pNZAr2xwdTo&t=7m47) if you want to watch how it's done -Turkish- 

## Spring BOOT TEMPLATES

### jpaentitylom

Create JPA entity classes using Lombok

**Source :**
```
@lombok.Data
@lombok.AllArgsConstructor
@lombok.NoArgsConstructor
@javax.persistence.Entity
public class $NAME$ {
    
    @javax.persistence.Id
    @javax.persistence.GeneratedValue(strategy = javax.persistence.GenerationType.IDENTITY)
    private java.lang.Long id;

    private java.lang.String name;
    
}
```

### jparepo

Create JPA repository class with defined entity

**Source :**
```
@org.springframework.stereotype.Repository
public interface $ENTITY$Repository extends org.springframework.data.repository.CrudRepository<$ENTITY$, Long> {

    org.springframework.data.domain.Page<$ENTITY$> findAll(org.springframework.data.domain.Pageable pageable);

}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY | - | "User" | -

### spservice

Create spring service with autowired repository and add first empty method

**Source :** 
```
@org.springframework.stereotype.Service
public class $ENTITY$Service {

    private $ENTITY$Repository $ENTITY_VARIABLE$Repository;

    @org.springframework.beans.factory.annotation.Autowired
    public $ENTITY$Service($ENTITY$Repository $ENTITY_VARIABLE$Repository) {
        this.$ENTITY_VARIABLE$Repository = $ENTITY_VARIABLE$Repository;
    }

    public java.util.List<$ENTITY$> findAll(int page){
        List<$ENTITY$> $ENTITY_VARIABLE$List = new java.util.ArrayList<>();

        return $ENTITY_VARIABLE$List;
    }
}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY_VARIABLE | camelCase(ENTITY) | - | -

### spfindall

Create to derive a Pageable instance from the request parameters and get all item list

**Source :**

```
org.springframework.data.domain.PageRequest pageRequest = org.springframework.data.domain.PageRequest.of($PAGE$ - 1, $SIZE$);
java.util.List<$ENTITY$> $ENTITY_VARIABLE$List = $ENTITY_VARIABLE$Repository.findAll(pageRequest).getContent();
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY_VARIABLE | camelCase(ENTITY) | - | -
PAGE | - | "page" | -
SIZE | - | "10" | -

### spcontroller

Create spring controller with autowired service and add findAll get method

**Source :**

```
@org.springframework.web.bind.annotation.RestController
@org.springframework.web.bind.annotation.RequestMapping("/$ENDPOINT$")
public class $ENTITY$Controller {

    private $ENTITY$Service $ENTITY_VARIABLE$Service;

    @org.springframework.beans.factory.annotation.Autowired
    public $ENTITY$Controller($ENTITY$Service $ENTITY_VARIABLE$Service) {
        this.$ENTITY_VARIABLE$Service = $ENTITY_VARIABLE$Service;
    }

    @RequestMapping(value = "/{page}")
    public org.springframework.http.ResponseEntity<java.util.List<$ENTITY$>> findById(@org.springframework.web.bind.annotation.PathVariable("page") int page) {
        return new ResponseEntity<>($ENTITY_VARIABLE$Service.findAll(page), org.springframework.http.HttpStatus.OK);
    }

}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY_VARIABLE | camelCase(ENTITY) | - | -
ENDPOINT | - | ENTITY_VARIABLE | -

### @reqget

Get mapping method

**Source :**

```
@org.springframework.web.bind.annotation.GetMapping(value = "/get$ENTITY$/{$PARAMETER$Id}")
public ResponseEntity<$ENTITY$> get$ENTITY$(@PathVariable("$PARAMETER$Id") Long $PARAMETER$Id) {
    return new ResponseEntity<>(userService.get$ENTITY$($PARAMETER$Id), HttpStatus.OK);
}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY_VARIABLE | camelCase(ENTITY) | - | -

### @reqpost

Post mapping method

**Source :**

```
@org.springframework.web.bind.annotation.PostMapping(value = "/$METHOD_PREFIX$$ENTITY$")
public ResponseEntity<$ENTITY$> $METHOD_PREFIX$$ENTITY$(@RequestBody $ENTITY$ $ENTITY_VARIABLE$) {
    return new ResponseEntity<>($ENTITY_VARIABLE$Service.$METHOD_PREFIX$$ENTITY$($ENTITY_VARIABLE$), HttpStatus.OK);
}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ENTITY_VARIABLE | camelCase(ENTITY) | - | -




### h2conf

Configure h2 database

**Source :**
```
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:file:~/$FILE_NAME$
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.show-sql=true
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=update
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
FILE_NAME | - | "application" | -

### valclass

Check all request for requested items

**Source :**
```
public class Validator {

    public static void validateUser($ENTITY$ $ENTITY_VARIABLE$) {
        org.springframework.util.Assert.isTrue($ENTITY_VARIABLE$ != null, "$ENTITY_VARIABLE$ $ERROR_MESSAGE$");
    }
}
```

Name | Expression | Default value | Skip if defined
--- | --- | --- | ---
ERROR_MESSAGE | - | "cannot be null" | -