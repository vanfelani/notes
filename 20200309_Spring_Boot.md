 #Hibernate Validator
 ***
 ### Membuat Annotation NotBlank
 
 > @NotBlank harus memiliki minimal 1 character tidak boleh white space, sedangkan @NotEmpty boleh kosong/ boleh white space.
 
 ```java
    private Integer id;

    @NotBlank
    private String name;
```
harus menambahkan anotation @Valid pada target
example
```java
 @PutMapping("/{id}")
    public ResponseMessage<ItemModel> edit(@PathVariable Integer id, @RequestBody @Valid ItemModel model) {
        ModelMapper modelMapper = new ModelMapper();
        model.setId(id);
        Item entity = modelMapper.map(model, Item.class);


        entity = itemService.edit(entity);
        ItemModel data = modelMapper.map(entity, ItemModel.class);

        return ResponseMessage.succses(data);
    }
```
lalu taruh exeption di class GlobalExeptionHandler dengan menambahkan implements @Override handleMethodArgumentNotValue
example
```java
 
    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException e, HttpHeaders headers, HttpStatus status, WebRequest request) {
        Map<String, String> errors = new HashMap<>();
        e.getBindingResult().getFieldErrors().forEach(fieldError -> {
            String field = fieldError.getField();
            String message = fieldError.getDefaultMessage();

            errors.put(field, message);
        });

        ResponseMessage<Map<String, String>> body = ResponseMessage.error(-1, e.getMessage(),errors);
        return ResponseEntity.ok(body);
    }
```
Setela itu buat method error responMessage baru untuk menampilkan data error
```java
 public static  <T> ResponseMessage<T> error(int code, String message, T data) {
        return new ResponseMessage(code, message, data);
    }
```
hanya bisa menampilkan validasi satu error pertama, jika kita mau menampikan validasi erorr lenbih dari satu maka kita bisa membuatnya seperti ini
di class GlobalExeptionHandler.java
example
```java
  @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException e, HttpHeaders headers, HttpStatus status, WebRequest request) {
        Map<String, List<String>> errors = new HashMap<>();

        e.getBindingResult().getFieldErrors().forEach(fieldError -> {
            String field = fieldError.getField();
            String message = fieldError.getDefaultMessage();

            List<String> messages = errors.get(field);
            if (messages == null) {
                messages = new ArrayList<>();
                errors.put(field, messages);
            }
            messages.add(message);
        });
        ResponseMessage body = ResponseMessage.error(-1, e.getMessage(), errors);
        return ResponseEntity.ok(body);
    }
```
jika kita ingin mengcostum message di @NotBlank maka bisa juga dengn menambhkan
```java
@NotBlank(message = "Data Not Blank")
    private String name;
```
jika kita mengcustom dengan Internationalsasion maka dengan cara seperti ini
example
1.ItemModel,java
```java
  @NotBlank(message = "{name.notblank}")
    private String name;
```
2.di messages.properties
```java
name.notBlank = Name cannot empty
```
di messages_in_ID.properties
```java
name.notBlank = Nama tidak boleh kosong
```
3.di ApplicationConfig,java
```java
@Bean
    public LocalValidatorFactoryBean validatorFactory(MessageSource messageSource){
        LocalValidatorFactoryBean bean = new LocalValidatorFactoryBean();
        bean.setValidationMessageSource(messageSource);
        return bean;
    }
```


### Membuat custom annotations  MinLength

[1].buat class MinLength.java di  package com.enigma.restservice.validations.annotations;

 ```java
package com.enigma.restservice.validations.annotations;

import com.enigma.restservice.validations.MinLengthValidator;

import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.*;

@Target({ElementType.FIELD, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = MinLengthValidator.class)
@Documented
public @interface MinLength {
    String message() default "{com.enigma.restservice.validations.annotations.MinLength.message}";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};

    int value();

    @Target({ElementType.FIELD, ElementType.METHOD})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @interface List {
        MinLength[] value();
    }

}
```
[2]. lalu buat class MintLengtValidator.java di package com.enigma.restservice.validations;

```java
package com.enigma.restservice.validations;

import com.enigma.restservice.validations.annotations.MinLength;

import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

public class MinLengthValidator implements ConstraintValidator<MinLength, String> {

    private MinLength constraint;

    @Override
    public void initialize(MinLength constraintAnnotation) {
        constraint = constraintAnnotation;
    }

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        int length = value != null ? value.length() : 0;
        return  length >= constraint.value();
    }
}

```

[3]. lalu buat message di massages.properties

```java
com.enigma.restservice.validations.annotations.MinLength.message = Minimum length is {value} character
```

[4]. Taruh @MinLength di target nya

```java
    @MinLength(3)
    @NotBlank(message = "{name.notblank}")
    private String name;
```
### Bean Validation constraints
Terdapat banyak anotasi validasi yang ada di hibernate, yaitu :
```java
@AssertFalse
Pastikan elemen beranotasi salah

@AssertTrue
Pastikan elemen beranotasi benar

@Email
Cek apakah urutan karakter yang ditentukan adalah alamat email yang valid. Parameter opsional regexpdan flagsmemungkinkan untuk menentukan ekspresi reguler tambahan (termasuk bendera ekspresi reguler) yang harus cocok dengan email.
Jenis data yang didukung : CharSequence

@NotNull
Periksa bahwa nilai yang dianotasi tidak null
@Null
Memeriksa apakah nilai penjelasannya adalah null

```
>Selain annotasi diatas masih ada lagi anotasi yang lain, 
>selengkapnya baca di : [dokumentasi hibernate validator](https://docs.jboss.org/hibernate/validator/6.0/reference/en-US/html_single/#section-declaring-method-constraints)

##Menghubungkan Spring dengan database (mySql)

tambahkan depedency di pom.xml
```java
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
```

lalu buat setting di resources/application.yml

```java
spring:
  datasource:
    driverClassName: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/bootcamp?useTimezone=true&serverTimezone=UTC
    username: root
    password: adam003
  jpa:
    hibernate:
      ddl-auto: update
    generate-ddl: true
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect
  messages:
    basename: i18n/messages
```
di spring sudah ada terdapat method bawaan dibawah ini :
```java

@NoRepositoryBean
public interface JpaRepository<T, ID> extends PagingAndSortingRepository<T, ID>, QueryByExampleExecutor<T> {
    List<T> findAll();

    List<T> findAll(Sort var1);

    List<T> findAllById(Iterable<ID> var1);

    <S extends T> List<S> saveAll(Iterable<S> var1);

    void flush();

    <S extends T> S saveAndFlush(S var1);

    void deleteInBatch(Iterable<T> var1);

    void deleteAllInBatch();

    T getOne(ID var1);

    <S extends T> List<S> findAll(Example<S> var1);

    <S extends T> List<S> findAll(Example<S> var1, Sort var2);
}
```
jadi jika kita ingin membuat menggunakan method yang sama maka hanya memanggilnya saja
dengan membuat class yang extends JpaRepository

```java
package com.enigma.restservice.repositories;

import com.enigma.restservice.entity.Item;
import org.springframework.data.jpa.repository.JpaRepository;

public interface ItemRepository extends JpaRepository<Item, Integer> {
   
}
```

jika tidak mau mengikuti method bawaan di jpa atau mau membuat method custom, maka bisa dibuat dengan referensi
sebagai berikut
 [Query creation](https://docs.spring.io/spring-data/data-jpa/docs/current/reference/html/#jpa.query-methods.query-creation)
 
 >Noted by : [Adam Nasrudin](https://www.instagram.com/adamnasrudin/?hl=id)