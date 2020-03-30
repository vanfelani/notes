## Swagger 
___

Sebuah tools untuk :
1. Develop API 
2. Interact With APIs
3. Document APIs
> Membantu pengembang merancang, membangun, mendokumentasikan isi dari aplikasi 

Menurut sumber : [https://swagger.io/about/](https://swagger.io/about/)
> Keunggulan Swagger :

* Design ,
Design and model APIs according to specification-based standards

* Build ,
Build stable ,reusable code for your API in almost any language

* Document ,
Improve developer experience with interactive API documentation

* Test ,
Perform simple functional tests on your APIs without overhead

> Cara menjalankan Swagger


Langkah pertama, masukkan dependency Swagger di pom.xml dan install , versi yang di gunakan adalah **swagger 2** 

```java
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

kedua , buatlah file . java di package configs

```java
@EnableSwagger2
@Configuration
public class SwaggerApplication {

    @Bean
    public Docket api(){
        return new Docket(DocumentationType.SWAGGER_2)
        .select()
        .apis(RequestHandlerSelectors.basePackage("com.enigma.restservice"))
        .paths(PathSelectors.any())
        .build().apiInfo(apiInfo());
    }
    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
        .title("Spring Boot Rest API")
        .description("Example")
        .contact(new Contact("Christin","christin.com","christin@gmail.com"))
        .version("1.2.3")
        .build();
    }
}
```

**notes**  : basepackage untuk menetapkan controller

Buka browser dan ketik :
1. Tampilan swagger biasa -> [http://localhost:8080/v2/api-docs](http://localhost:8080/v2/api-docs) 

2. Tampilan swagger dengan ui -> [http://localhost:8080/swagger-ui.html] , memudahkan pengguna dalam melihat & membaca isi dari sebuah program 


```java
@RequestMapping("/items")
@RestController
@Api(value ="Item",description = "Item Controller",tags = {"item"})
public class ItemController {
}
```
**@Api(value ="Item",description = "Item Controller",tags = {"item"})** fungsinya untuk memberikan nilai , dan menampilkan deskripsi dan tagsnya 

```java
@ApiOperation(value = "Find All Item",tags = {"item"})
    @ApiResponses({
        @ApiResponse(code=200,message = "This is response")
    })
    @GetMapping
    public ResponseMessage<PageableList<ItemModel>> findAll(
        @RequestParam(required = false)@ApiParam(required = true)String name,
        @RequestParam(defaultValue = "asc")String sort,
        @RequestParam(defaultValue = "0")int page,
        @RequestParam(defaultValue = "10") int size
        ) {
            if(size >100){
                size=100;
            }
```
**@ApiOperation(value = "Find All Item",tags = {"item"})**
* @ApiOperation dapat di tambahkan dalam sebuah method 

**@ApiResponses({
        @ApiResponse(code=200,message = "This is response")**
* @ApiResponses(banyak) /@ApiResponse(untuk 1 response) : bisa di letakkan dalam method , untuk memberikan informasi mengenai responnya  

**@ApiParam(required = true)**
* @ApiParam di letakkan dalam parameter 

## Docker : Containerization
____

Docker menggunakan konsep Container Manager

> perbedaan Virtual Machine (VM) dan Docker :

 * **VM** : Install VM manager , contoh : virtual box atau vm . ketika ingin deploy maka , operating system , application dan depedency harus di install lagi , bayangkan apabila kita memiliki banyak aplikasi , maka setiap aplikasi harus menginstal kembali masing-masing os , app dan depedency nya 

* **Docker** : mengandung konsep container dimana ketika kita deploy sebuah program , maka hanya folder aplikasi saja yang di masukkan , di docker tidak perlu lagi untuk menginstall os , app dan depedency nya , cukup di instal di applikasi . Docker tidak memiliki operating system, ketika membuat container, kita menggunakan os bawaan dari container manager menggunakan os induk docker

> Penggunaan Docker (Contoh menggunakan OS Linux )
 1. Install Docker  
 2. Pilih folder aplikasi 
 3. Buat Dockerfile ( penulisan harus tepat ) dan simpan file,lokasi file di dalam folder 'rest-service' sejajar dengan pom.xml 

 ```java 
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```
4. Buka file application.yml 
```java
 datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://127.0.0.1:3306/bootcamp
    username: root
    password: root123
```
4. Save dan buka terminal , start docker ,ketik
    * **sudo service docker start**
    * build aplikasi 
    * **docker build -t com.enigma/rest-service .**
    * cek images -> **docker images** , cek container -> **docker ps -a**
     * Penamaan _com.enigma/rest-service_ di dapat dari file  group pom.xml 

    ```java
    <groupId>com.enigma</groupId>
	<artifactId>rest-service</artifactId>
    ```

    * dan run  **docker run --name application -p 8080:8090 --network="host" com.enigma/rest-service -t**  
    Penamaan _com.enigma/rest-service_ di dapat dari file  group pom.xml 

    ```java
    <groupId>com.enigma</groupId>
	<artifactId>rest-service</artifactId>
    ```

> NOTES : (Apabila ada Error)
* Buat User baru (localhost di ganti % , agar bisa di akses dimanapun)
* GRANT ALL PRIVILEGES ON *.* TO 'USERNAME'@'%' IDENTIFIED BY 'PASSWORD' WITH GRANT OPTION;

* atau ubah user yang sudah ada
* update mysql.user set Host='%' WHERE Host='localhost' and User='root';


