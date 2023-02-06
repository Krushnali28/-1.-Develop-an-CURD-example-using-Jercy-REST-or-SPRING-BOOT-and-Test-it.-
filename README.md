# -1.-Develop-an-CURD-example-using-Jercy-REST-or-SPRING-BOOT-and-Test-it.-
import org.springframework.boot.SpringApplication;

import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootCrudRestApplication {

 public static void main(String[] args) {
  SpringApplication.run(SpringBootCrudRestApplication.class, args);
 }
}

##Configuring MySQL Database
spring.datasource.url = jdbc:mysql://localhost:3306/users_database?useSSL=false
spring.datasource.username = root
spring.datasource.password = root


## Hibernate Properties
# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect

# Hibernate ddl auto (create, create-drop, 


## Create Jersey Resource - UserResource.java

Java JavaEE Library REST JUnit Spring Boot Microservices Full Stack  YouTubeUI  InterviewQuiz Hibernate DB Go Me 

Spring Boot 2 + Jersey REST + JPA + Hibernate 5 CRUD REST APIs Example
author: Ramesh Fadatare
spring boot

<< Back to Spring Boot Tutorial

In this article, we will learn step by step how to develop CRUD REST APIs using integration of Jersey 2.26 with Spring boot 2.0.5 RELEASE, JPA/Hibernate 5 and MySQL as a database.
Jersey RESTful Web Services framework is open source, production quality, a framework for developing RESTful Web Services in Java that provides support for JAX-RS APIs and serves as a JAX-RS (JSR 311 & JSR 339) Reference Implementation.
Spring boot provides support for integration of Jersey with spring boot application using spring-boot-starter-jersey starter dependency:
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jersey</artifactId>
</dependency>
Let's create a step by step Spring Boot Jersey CRUD RESTful APIs project.
Table of contents
What we’ll build?
Tools and Technologies Used
Creating and Importing a Project
Packaging Structure
Configuring MySQL Database
Create Jersey Resource - UserResource.java
Creating a JerseyConfiguration Class
Create a JPA Entity called User.java
Create Spring Data JPA Repository - UserRepository.java
Create ResourceNotFoundException.java Class
Running the Application
Testing via Postman Client
1. What we’ll build?
We are developing a CRUD REST APIs using integration of Jersey 2.26 with Spring boot 2.0.5 RELEASE, JPA/Hibernate 5 and MySQL as a database.

2. Tools and Technologies Used
Spring Boot - 2.0.4.RELEASE
JDK - 1.8 or later
Spring Framework - 5.0.8 RELEASE
Hibernate - 5.2.17.Final
Maven - 3.2+
Spring Data JPA - 2.0.10 RELEASE
IDE - Eclipse or Spring Tool Suite (STS)
MYSQL - 5.1.47
Jersey - 2.26
3. Creating and Importing a Project
There are many ways to create a Spring Boot application. The simplest way is to use Spring Initializr at http://start.spring.io/, which is an online Spring Boot application generator.

Look at the above diagram, we have specified following details:
Generate: Maven Project
Java Version: 1.8 (Default)
Spring Boot:2.0.6
Group: net.guides.springboot2
Artifact: springboot-jersey-rest-crud-jpa
Name: springboot-jersey-rest-crud-jpa
Description: Rest API for a Simple User Management Application
Package Name : net.guides.springboot2
Packaging: jar (This is the default value)
Dependencies: Jersey, JPA, MySQL
Once, all the details are entered, click on Generate Project button will generate a spring boot project and downloads it. Next, Unzip the downloaded zip file and import it into your favorite IDE.
4. Packaging Structure
Following is the packing structure for your reference -

The pom.xml File
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
 <modelVersion>4.0.0</modelVersion>

 <groupId>net.guides.springboot2</groupId>
 <artifactId>springboot-jersey-rest-crud-jpa</artifactId>
 <version>0.0.1-SNAPSHOT</version>
 <packaging>jar</packaging>

 <name>springboot-jersey-rest-crud-jpa</name>
 <description>Demo project for Spring Boot</description>

 <parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.0.5.RELEASE</version>
  <relativePath /> <!-- lookup parent from repository -->
 </parent>

 <properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
  <java.version>1.8</java.version>
 </properties>

 <dependencies>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-jpa</artifactId>
  </dependency>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jersey</artifactId>
  </dependency>

  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
  </dependency>

  <dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <scope>runtime</scope>
  </dependency>
 </dependencies>

 <build>
  <plugins>
   <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
   </plugin>
  </plugins>
 </build>
</project>
SpringBootCrudRestApplication.java
This spring boot application has an entry point Java class called SpringBootCrudRestApplication.java with the public static void main(String[] args) method, which you can run to start the application.
import org.springframework.boot.SpringApplication;

import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootCrudRestApplication {

 public static void main(String[] args) {
  SpringApplication.run(SpringBootCrudRestApplication.class, args);
 }
}
@SpringBootApplication is a convenience annotation that adds all of the following:
@Configuration tags the class as a source of bean definitions for the application context.
@EnableAutoConfiguration tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
Normally you would add @EnableWebMvc for a Spring MVC app, but Spring Boot adds it automatically when it sees spring-webmvc on the classpath. This flags the application as a web application and activates key behaviors such as setting up a DispatcherServlet.
@ComponentScan tells Spring to look for other components, configurations, and services in the hello package, allowing it to find the controllers.
The main() method uses Spring Boot’s SpringApplication.run() method to launch an application.
5. Configuring MySQL Database
Configure application.properties to connect to your MySQL database. Let's open an application.properties file and add following database configuration to it.
spring.datasource.url = jdbc:mysql://localhost:3306/users_database?useSSL=false
spring.datasource.username = root
spring.datasource.password = root


## Hibernate Properties
# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect

# Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto = update
Change the above configuration such as JDBC URL, username and password as per your environment.
6. Create Jersey Resource - UserResource.java
package net.guides.springboot2.springbootjerseyrestcrudjpa.controller;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.validation.Valid;
import javax.ws.rs.Consumes;
import javax.ws.rs.DELETE;
import javax.ws.rs.GET;
import javax.ws.rs.POST;
import javax.ws.rs.PUT;
import javax.ws.rs.Path;
import javax.ws.rs.PathParam;
import javax.ws.rs.Produces;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Component;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;

import net.guides.springboot2.springbootjerseyrestcrudjpa.exception.ResourceNotFoundException;
import net.guides.springboot2.springbootjerseyrestcrudjpa.model.User;
import net.guides.springboot2.springbootjerseyrestcrudjpa.repository.UserRepository;

@Component
@Path("/api/v1")
public class UserResource {

 @Autowired
 private UserRepository userRepository;

 @GET
 @Produces("application/json")
 @Path("/users")
 public List<User> getAllUsers() {
  return userRepository.findAll();
 }

 @GET
 @Produces("application/json")
 @Path("/users/{id}")
 public ResponseEntity<User> getUserById(@PathParam(value = "id") Long userId) throws ResourceNotFoundException {
  User user = userRepository.findById(userId)
    .orElseThrow(() -> new ResourceNotFoundException("User not found :: " + userId));
  return ResponseEntity.ok().body(user);
 }

 @POST
 @Produces("application/json")
 @Consumes("application/json")
 @Path("/users")
 @PostMapping("/users")
 public User createUser(User user) {
  return userRepository.save(user);
 }

 @PUT
 @Consumes("application/json")
 @Path("/users/{id}}")
 public ResponseEntity<User> updateUser(@PathParam(value = "id") Long userId,
   @Valid @RequestBody User userDetails) throws ResourceNotFoundException {
  User user = userRepository.findById(userId)
    .orElseThrow(() -> new ResourceNotFoundException("User not found :: " + userId));

  user.setEmailId(userDetails.getEmailId());
  user.setLastName(userDetails.getLastName());
  user.setFirstName(userDetails.getFirstName());
  final User updatedUser = userRepository.save(user);
  return ResponseEntity.ok(updatedUser);
 }

 @DELETE
 @Path("/users/{id}")
 public Map<String, Boolean> deleteUser(@PathParam(value = "id") Long userId) throws ResourceNotFoundException {
  User user = userRepository.findById(userId)
    .orElseThrow(() -> new ResourceNotFoundException("User not found :: " + userId));

  userRepository.delete(user);
  Map<String, Boolean> response = new HashMap<>();
  response.put("deleted", Boolean.TRUE);
  return response;
 }
}
