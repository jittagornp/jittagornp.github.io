# การเขียน Spring-boot Reactive + Nuxt.js 

### 1. ทำการ spring-boot project    
add dependencies ดังต่อไปนี้ 
```xml
...
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-webflux</artifactId>
  </dependency>

  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-thymeleaf</artifactId>
  </dependency>
...
```

### 2. config main class 
สำหรับ start/run spring-boot 
```java
...
@SpringBootApplication
@ComponentScan(basePackages = "com.pamarin")
public class AppStarter {
    public static void main(String[] args) {
        SpringApplication.run(AppStarter.class, args);
    }
}
```

### 3. เขียน controller 
เนื่องจากเราจะใช้ Nuxt.js ใน mode SPA (Single Page Application) เราจะต้องเขียน router ให้รอรับกับ nuxt (vue) route ดังนี้
```java
@Controller
public class IndexController {

    @GetMapping({"", "/"})
    public Mono<String> index(final Model model) {
        return Mono.just("index");
    }

    @GetMapping({
        "/{path:[^\\.]*}", 
        "/{path1:^(?!oauth).*}/{path2:[^\\.]*}",
        "/{path1:[^\\.]*}/{path2:[^\\.]*}/{path3:[^\\.]*}",
        "/{path1:[^\\.]*}/{path2:[^\\.]*}/{path3:[^\\.]*}/{path4:[^\\.]*}",
        "/{path1:[^\\.]*}/{path2:[^\\.]*}/{path3:[^\\.]*}/{path4:[^\\.]*}/{path5:[^\\.]*}",
        "/{path1:[^\\.]*}/{path2:[^\\.]*}/{path3:[^\\.]*}/{path4:[^\\.]*}/{path5:[^\\.]*}/{path6:[^\\.]*}"
    })
    public Mono<String> forward(final Model model) {
        return index(model);
    }
}

```
### 4. สร้าง Nuxt project ที่ root maven project
run คำสั่งดังต่อไปนี้
```shell
$ npx create-nuxt-app nuxt
```
- nuxt คือ ชื่อ folder  



