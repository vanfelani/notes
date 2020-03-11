## Salah satu Annotation dalam Spring Boot ('@')

### @ControllerAdvice

**Definisi :**

@ControllerAdvice salah satu Annotation dalam SpringBoot yang berguna untuk menangani Exception di seluruh aplikasi dalam satu komponen penanganan global yang menjadi salah satu pendukung dalam menerapkan konsep MVC.

**Contoh pendeklarasian :**

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Autowired
    private MessageSource messageSource;

    @ExceptionHandler(ApplicationException.class)
    public ResponseEntity<ResponseMessage> handleApplicationException(ApplicationException e, Locale locale) {
        String message = messageSource.getMessage(e.getMessage(), null, LocaleContextHolder.getLocale());
        ResponseMessage body = ResponseMessage.error(e.getCode(), message);
        return ResponseEntity.ok(body);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ResponseMessage> handleUnknowException(Exception e) {
        ResponseMessage body = ResponseMessage.error(-1, e.getMessage());
        return ResponseEntity.ok(body);
    }

}
```

```java
@ControllerAdvice
public class ControllerAdvisor extends ResponseEntityExceptionHandler {

    @ExceptionHandler(CityNotFoundException.class)
    public ResponseEntity<Object> handleCityNotFoundException(
        CityNotFoundException ex, WebRequest request) {

        Map<String, Object> body = new LinkedHashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("message", "City not found");

        return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(NoDataFoundException.class)
    public ResponseEntity<Object> handleNodataFoundException(
        NoDataFoundException ex, WebRequest request) {

        Map<String, Object> body = new LinkedHashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("message", "No cities found");

        return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
    }@ControllerAdvice
public class ControllerAdvisor extends ResponseEntityExceptionHandler {

    @ExceptionHandler(CityNotFoundException.class)
    public ResponseEntity<Object> handleCityNotFoundException(
        CityNotFoundException ex, WebRequest request) {

        Map<String, Object> body = new LinkedHashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("message", "City not found");

        return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(NoDataFoundException.class)
    public ResponseEntity<Object> handleNodataFoundException(
        NoDataFoundException ex, WebRequest request) {

        Map<String, Object> body = new LinkedHashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("message", "No cities found");

        return new ResponseEntity<>(body, HttpStatus.NOT_FOUND);
    }
}
```

## Internasionalisasi Message in Spring Boot

**Definisi :**

Internasionalisasi Message ditujukan untuk memberikan pesan kepada client dengan bahasa yang disesuaikan dengan lokasi komputer client berada.

**Contoh pendeklarasian :**

controller
```java
@RequestMapping("/hello")
@RestController
public class HelloController {

    @Autowired
    private MessageSource messageSource;

    @GetMapping
    public String sayHello() {
        String message = messageSource.getMessage("hello", new String[] { "Jhon" }, LocaleContextHolder.getLocale());
        return message;
    }

}
}
```

properties (message_id)
```properties
excetion.entity.not.found = Entitas tidak ditemukan
```

properties (message)
```properties
exception.entity.not.found = Entity not found
```

**sumber :**

1. [@ControllerAdvice](http://zetcode.com/springboot/controlleradvice/)

2. [Internasionalisasi](https://medium.com/@satya.syahputra/internasionalisasi-pesan-di-spring-boot-menggunakan-message-source-8e17ace6bbaa)