# VIPGuestList

## About the Project

This is a simple project, based on **_Alura's Spring Boot course_**, used to practice creating a Spring boot application!
The **purpose** of this project is to add guests to a "Vip" list and inform them via email that they have been invited.
### Technologies/Database used
* Spring Boot;
* Spring MVC;
* Spring DevTools &amp; LiveRealod;
* Spring Initializer;
*  Thymeleaf;
* JPA;
* Java Commom Email; 
* AJAX;
* MySQL;

## Summary
1. [Starting the project - Spring Boot](#boot)
	* [Why to use Spring boot?](#why)
	* [How to use?](#howto)
	* [How to Configure/Run the Server](#configureserver)
	* [How to Configure the JPA + MySQL](#configurejpa)
2. [Creating the Entity](#entity)
 

## <a name="boot"></a>Starting the project - Spring Boot
###  <a name="why"></a>Why to use Spring boot? 
The main utility of **Spring Boot** is at:
* Simplify application development.
* Configure Spring through Java classes, not XML

###  <a name="howto"></a>How to use? 
1. Create a maven project;
2. Add the dependency below into the pom.xml
```xml
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.2.2.RELEASE</version>
	<relativePath />
</parent>

<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>
```

### <a name="configureserver"></a>How to Configure/Run the Server

1. Create a package _(com.vipguestlist.configurations)_ into the _src/main/java_;
2. Create a class with the **@SpringBootApplication** annotation and with a 'main method';
3. Run the server using the _run_ method;
4. Test, acessing `localhost:8080` and look if the "Whitelabel Error Page" appears;

_by default, the port used is 8080 and the container server is tomcat_
```java
package com.vipguestlist.configuration;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Configuration {

	public static void main(String[] args) {
		SpringApplication.run(Configuration.class, args);
	}
}
```
### <a name="configurejpa"></a>How to Configure the JPA + MySQL
1. Add into the pom.xml the dependencies;
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
</dependency>
```
2. Create a file into the folder **_src/main/resources_**, with the name **_application.properties_** and with the code below:
```
# Database
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost/viplist?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=
spring.jpa.hibernate.ddl-auto = update
spring.jpa.show-sql = true
```
* **Another option**, it will be adding the code below, into the Configuration Class:
```java
@SpringBootApplication
public class Configuration {

	public static void main(String[] args) {
		SpringApplication.run(Configuration.class, args);
	}
	
	/** JPA ConfigurationS
	 *  @bean it's necessary for Spring to "manage" the class
	 *  DriverManagerDataSource returns DataSource
	 */
	@Bean
	public DataSource dataSource() {
		DriverManagerDataSource driver = new DriverManagerDataSource();
		driver.setDriverClassName("com.mysql.cj.jdbc.Driver");
		driver.setUrl("jdbc:mysql://localhost/viplist?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC");
		driver.setUsername("root");
		driver.setPassword("");
		return driver;
	}
}
```
## <a name="entity"></a>Creating the Entity
