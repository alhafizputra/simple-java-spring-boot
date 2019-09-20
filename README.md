# simple-java-spring-boot

Building Simple Java Application with Spring Boot
<br/><br/>
IDE used: Netbeans
<br/><br/>
Langkah-langkahnya:
1.	File -> New Project -> Maven -> Web Application
2.	Isi nama project: Simple-Spring-Boot. Isi groupId: belajar, package:belajar.latihan
3.	Server pilih <No Server Selected>, lalu Finish.
4.	Pom.xml
```
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.1.RELEASE</version>
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
    </dependencies>
```
5.	Di project files tambah nbactions.xml untuk running menggunakan server tomcat embed nya springboot
```
<?xml version="1.0" encoding="UTF-8"?>
<actions>
        <action>
            <actionName>run</actionName>
            <packagings>
                <packaging>war</packaging>
                <packaging>ear</packaging>
                <packaging>ejb</packaging>
            </packagings>
            <goals>
                <goal>org.springframework.boot:spring-boot-maven-plugin:1.5.4.RELEASE:run</goal>
            </goals>
            <properties>
                <exec.args>-classpath %classpath prosia.app.Application</exec.args>
                <exec.executable>java</exec.executable>
            </properties>
        </action>
    </actions>
```   
6.	Buat Application.java di package belajar.latihan
```
package belajar.latihan;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;

@SpringBootApplication(
        scanBasePackages = {
            "belajar.latihan", "belajar.latihan.controller"
        })
public class Application extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(Application.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```
7.	Buat HelloController.java dengan package belajar.latihan.controller
```
package belajar.latihan.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {
    
    @GetMapping({"/", "/index"})
    public String hello(Model model, @RequestParam(value="name", required=false, defaultValue="World") String name) {
        model.addAttribute("name", name);
        return "index.html";
    }
}
```
8.	Di Other Sources tambah application.properties
```
## Embedded Server Configuration
server.port = 8091
```
9.	Klik kanan project, klik run
10. Buka localhost:8091/ di browser
 

