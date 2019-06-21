#Spring Hello World

This code is an example of deploying a Spring Boot application to Java application servers such as Tomcat and Docker 
container

##Deploying to Java application servers
- Create a subclass that extends the _SpringBootServletInitializer_ class and implements _configure()_ method
- Change the ```<packaging>``` element to war
- If we are using an embedded servlet container, ensure that that servlet container doesn't interfere with the servlet 
container to which the WAR file will be deployed.
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```
- Execute the _package_ goal: $ mvnw package
- Code the WAR file in /target directory to /webapps folder of the Tomcat server

##Deploying to Docker container
- Define a file named 'Dockerfile' that identifies the structure of a Docker image
- Build a Docker Image with Maven using Dockerfile Maven Plugin
```
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>dockerfile-maven-plugin</artifactId>
    <version>1.4.3</version>
    <configuration>
        <repository>${docker.image.prefix}/${project.artifactId}</repository>
        <buildArgs>
            <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
        </buildArgs>
    </configuration>
</plugin>
```
- Execute the _package_ and _dockerfile:build_ goal: $ mvnw package dockerfile:build
- Check whether the image is ready to run or not: $ docker images
- Run the Docker container: $ docker run -p <port_in_hostpc>:<port_in_container> <image_name>

###Reference: 
1. https://spring.io/blog/2014/03/07/deploying-spring-boot-applications
2. https://spring.io/guides/gs/spring-boot-Docker/
3. Spring in Action, Fifth Edition, Manning https://www.manning.com/books/spring-in-action-fifth-edition



