# SPRING BOOT


Kenapa SpringBoot? bisa buat apa aja!.

Spring Boot adalah salah satu framework dari Spring Framework. Dengan Spring Boot, developer tidak terlalu banyak menambahkan dependensi sehingga pembuatan aplikasi dapat lebih cepat. Selain itu, Spring Boot juga menyediakan banyak dependensi yang dibutuhkan oleh developer seperti  Spring Web, Spring Reactive We, Spring Web Services, WebSocket, Jersey,  Template Thymeleaf, Apache Freemarker, Groovy Templates, Spring Security, OAuth2 Client, Okta, JDBC API, Liquibase Migration, JOOQ Access Layer, HyperSQL Database, Oracle Driver, Spring Boot Actuator, dan lainnya.

Di Spring Boot kita bisa membuat:
1. Microservices
   Microservice adalah kumpulan proses independen dan kecil yang berkomunikasi antara satu dengan lainnya untuk membentuk aplikasi kompleks yang agnostik terhadap bahasa API apa pun.

   ![MICROSERVICES](https://miro.medium.com/max/640/1*LWc55_UCWZAZr7Vke6fweg.png)

   Jadi intinya microservice yaitu membagi service ke bagian yang lebih kecil dimana service — service tersebut saling berhungan satu sama lain.Selain itu, dalam setiap services yang dibuat bisa menggunakan teknologi yang berbebeda.


   Sedangkan untuk implementasi ke web, android, iOS dll tidak bisa secara langsung. Dimana kita harus membuat terlebih dahulu yang namanya API Gateway. API Gateway memiliki tugas seperti load balancing, caching, access controll , API metering, dan monitoring.

2. Reactive
    Reactive programming mengelola aliran data asynchronous antara produsen data dan konsumen yang perlu bereaksi terhadap data tersebut dengan cara non-blocking.
3. Cloud 
4. Web Apss
5. Serverless
6. Event 
7. Driven
8. Batch.

#### Anotasi atau '@' dalam SpringBoot

+ **@SpringBootApplication** ini berguna untuk memberi tahu (sama seperti metadata) kepada compiler bahwa kita akan menggunakan SpringBootApplication.
  
  '
+ **@RestController** Sebagai penanda class sebagai controller.
  '
+ **@RequestMapping** digunakan untuk membuat maps permintaan web ke metode Spring Controller
  '  
+ **@RequestParam** Untuk mendapatkan parameter dari URL
  '
+ **@PathVariabel** untuk mendapatkan tempat penampung dari URL (Spring menyebutnya sebagai Templat URL)
  '
+ **@PostMapping** Menangani Permintaan POST HTTP
'
+ **@GetMapping** Menangani Permintaan GET HTTP
  '
+ **@PutMapping** Menangani Permintaan Put HTTP
  '
+ **@DeleteMapping** Menangani Permintaan Delete HTTP

didalam POST Dan GET mapping kita bisa memberikan tipe nya dengan parameter Produce
  

GET (Method) ga ada data ga ada bodynya. get pakai parameter ?name=didit  PATH (test?name=didit)

+ **@PostConstract** method ini dipanggil setelah constructor
  '

#### Request dan Response

*HttpServletRequest* Request yang dikirim dari client (diterima server)

*HttpServletResponse* Isi Requestnya. Request yang dikirim dari server dan diterima oleh Client.



### Test Controller diSpringBoot

oh ya, di dalam spring boot ini kita tidak perlu menjalankan server web di lokal kita, tapi spring boot sudah menyatukan semua ini pada saat kita menjalankan program kita. untuk defaultnya alamat dari java yang telah kita buat adalah http://localhost:8080/ 

Contoh Source Code untuk Test Controller ke HTTP.
```java
package com.codeid.restservice.controller; //Package Repository

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RequestMapping("/test")
// @Controller //non rest controller
@RestController
public class TestController {

    @GetMapping
    public String test (){
        return "halo.";
    }
}

```

>References: spring.io                                