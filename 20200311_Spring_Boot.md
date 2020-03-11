## Disable Error items.

Agar dapat memanipulasi tampilan ketika error pada interface sesuai dengan apa yang kita inginkan maka kita dapat melakukannya dengan 3 cara yaitu dengan menggunakan hibernate, annotation atau dengan cara membuat method baru.

Menggunakan hibernate:
   Tambahkan code berikut pada settingan hibernate server.error.whitelabel.enabled: false.

Menggunakan Annotation.
   Tambahka annotation @EnableAutoConfiguration(exclude = {ErrorMvcAutoConfiguration.class}) pada application

Membuat method baru di package com.enigma.restservice.controller (CustomeErrorController) berikut merupakan codenya.
   
   ``` java
    
        @Controller
        public class CustomErrorController implements ErrorController {

            @RequestMapping("/error")
            public void handleError() {
                throw new PathNotFoundException();
            }

            @Override
            public String getErrorPath() {
                return "/error";
    }
}
```

## Upload File Image

Untuk dapat mengupload file image pada aplikasi maka kita harus membuat class baru pada package com.enigma.restservice.controller, package com.enigma.restservice.services dan package com.enigma.restservice.services.impl.

Langkah pertam kita membuat class baru pada package com.enigma.restservice.controller, berikut merupakan contoh codingnya. Kita buat class dengan nama ItemImageController.java

``` java
@RequestMapping("/items/{id}/images")
@RestController
public class ItemImageController {

    @Autowired
    private ItemImageService service;

    @PostMapping
    public ResponseMessage<ItemImageModel> upload(@PathVariable Integer id, @RequestParam MultipartFile file) throws IOException {
        Path path = service.save(id, file);

        String name = path.getFileName().toString();
        String uri = ServletUriComponentsBuilder.fromCurrentContextPath()
                .path("/items/" + id + "/images/")
                .path(path.getFileName()
                        .toString())
                .toUriString();
        
        ItemImageModel model = new ItemImageModel();
        model.setName(name);
        model.setUrl(uri);
        model.setType(Files.probeContentType(path));
        model.setSize(Files.size(path));

        return ResponseMessage.success(model);
    }

```

# Membuat interface pada package com.enigma.restservice.services
 Langkah kedua kita akan membuat interface pada package com.enigma.restservice.services, disini kita akan membuat interface dengan nama ItemImageService.java. Berikut merupakan contoh coding pada interface ItemImageService.java.

``` java

    public interface ItemImageService {

    public Path save(Integer id, MultipartFile file) throws IOException;
}

```

# Membuat class pada package com.enigma.restservice.services.impl.

Langkah selanjutnya kita akan membuat class baru pada package com.enigma.restservice.services.impl., disini kita akan membuat class dengan nama ItemImageServiceImpl.java. Berikut merupakan contoh kodingan dari class ItemImageServiceImpl.java pada package com.enigma.restservice.services.impl.

``` java

@Service
public class ItemImageServiceImpl implements ItemImageService {


    @Autowired
    private ApplicationProperties properties;

    private Path parentDir;

    @Autowired
    @PostConstruct
    public void init() throws IOException {
        parentDir = Paths.get(properties.getDataDir(), "item")
                .toAbsolutePath().normalize();

    }

    @Override
    public Path save(Integer id, MultipartFile file) throws IOException {
        Path dir = parentDir.resolve(id.toString());
        Files.createDirectories(dir);

        Path target = dir.resolve(file.getOriginalFilename());
        Files.copy(file.getInputStream(), target, StandardCopyOption.REPLACE_EXISTING);

        return target;
    }
}

```

## Membuat setting untuk unit test.
Agar hasil tidak monoton maka kita dapat membuat class baru pada package com.enigma.restservice.models. Disini kita akan memberi nama class nya dengan nama ItemImageModel.java. Berikut merupakan coding dari ItemImageModel.java.

``` java

public class ItemImageModel {

    private String Filename;
    private String url;
    private  String type;
    private  Long size;

    public String getName() {
        return Filename;
    }

    public void setName(String fileName) {
        this.Filename = fileName;
    }

    public String getUrl() {
        return url;
    }

    public void setUrl(String url) {
        this.url = url;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public Long getSize() {
        return size;
    }

    public void setSize(Long size) {
        this.size = size;
    }

```

## Berikut merupakan hasil keluaran dari API TESTER

``` json

{
"code": 0,
"message": null,
"data":{
"url": "http://localhost:8080/items/3/images/get%20staff.PNG",
"type": "image/png",
"size": 17261,
"name": "get staff.PNG"
},
"timestamp": "2020-03-11 13:25:16.185"
}

```
Dan file imgae pun berhasil di upload di browser.

## Download File Image

Untuk dapat mendownload file image pada aplikasi maka kita akan menambahkan code pada packge com.enigma.restservice.services.impl

Langkah pertam kita akan menambahkan code pada package com.enigma.restservice.services.impl. Berikut merupakan penambahan syntak codingnya.

ItemServiceImpl.java

``` java

@Override
    public Resource load(Integer id, String filename) throws IOException {
        Path target = parentDir.resolve(id.toString()).resolve(filename);
        Resource resource = new UrlResource(target.toUri());
        return resource;
    }

```

Lalu kita tambahkan syntak pada package com.enigma.restservice.controller pada class ItemImageController.java. Berikut merupakan penambahan syntak untuk download file image.

``` java

     @GetMapping("/{filename}")
    public ResponseEntity<Resource> download(@PathVariable Integer id, @PathVariable String filename) throws IOException {
        Item entity = itemService.findById(id);
        Resource resource = service.load(entity, filename);

        String mediaType = URLConnection.guessContentTypeFromName(resource.getFilename());
        return ResponseEntity.ok()
                        .contentType(MediaType.parseMediaType(mediaType))
                .header(HttpHeaders.CONTENT_DISPOSITION)
                        .body(resource);
    }

```

Berikut merupakan output dari program application download

``` json

{
  "code": 0,
  "message": null,
  "data": [
    {
      "url": "http://localhost:8080/items/1/images/Insert%20Attendance.PNG",
      "type": "image/png",
      "size": 14318,
      "filename": "Insert Attendance.PNG"
    }
  ],
  "timestamp": "2020-03-11 15:44:40.684"
}

```
Pada url http://localhost:8080/items/1/images/Insert%20Attendance.PNG
jika di klik maka file gambar akan terdownload otomatis di browser.

## Delete File Image
Sama seperti download kita akan menambahkan code pada packge om.enigma.restservice.services.impl.
Langkah pertam kita akan menambahkan code pada packge impl, berikut merupakan penambahan syntak codingnya.

ItemServiceImpl.java

``` java

    @Override
    public void delete(Item entity, String filename) throws IOException {
        Path target = parentDir.resolve(entity.getId().toString()).resolve(filename);
        Files.delete(target);
    }

```
Lalu kita tambahkan syntak pada package com.enigma.restservice.controller pada class ItemImageController.java. Berikut merupakan penambahan syntak untuk delete file image.

``` java 

    @DeleteMapping("/{filename}")
    public ResponseMessage<Boolean> delete(@PathVariable Integer id, @PathVariable String filename) throws IOException {
        Item entity = itemService.findById(id);
        service.delete(entity, filename);
        return ResponseMessage.success(Boolean.TRUE);
    }

```

Berikut merupakan output dari delete file image

``` json

{
"code": 0,
"message": null,
"data": true,
"timestamp": "2020-03-11 17:01:42.734"
}

```

## Unit Test

Untuk melakukan unit test sendiri pertama-tama kita harus setting pom.xml terlebihdahulu. Tambahkan code berikut.

``` json

    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <scope>test</scope>
    </dependency>

```
Setelah selesai setting pom.xml maka kita terlebihdahulu harus setting pada hibernate. Berikut code pada setting hibernate.

``` json

application:
    data-dir: /home/heikal/VSCodeProject/rest-service
spring:
    datasource:
        driverClassName: org.h2.Driver
        url: jdbc:h2:mem:bootcamp
    jpa:
        hibernate:
            ddl-auto: create-drop
        generate-ddl: true
        show-sql: true
        properties:
            hibernate: 
                dialect: org.hibernate.dialect.H2Dialect
    messages:   
        basename: i18n/messages
    servlet:
        multipart:
            enabled: true
            max-file-size: 2MB
            max-request-size: 2MB

```
Setelah keduanya selesai langkah selanjutnya kita membuat file test pada package com.enigma.restservice.controller;
Disini kita buat file dengan nama ItemControllerTest.java.
Berikut code dari ItemControllerTest.java.

``` java

@AutoConfigureMockMvc
@SpringBootTest
public class ItemControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void shouldHaveItemNameBeras() throws Exception {

        mvc.perform(get("/items/1"))
                .andExpect(status().isOk())
                .andExpect(content().contentTypeCompatibleWith(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$.data.name", is("Beras")));
    }

}

```
Unit test untuk file ItemController pun selesai dibuat.
