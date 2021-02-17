---
layout: post
title:  "Building a Simple Spring Boot application with Java"
description: In this blog we talk about creating basic RESTful methods for our application
date:   2021-02-14 09:03:36 +0530
categories: Java SpringBoot RESFTful
---

Today I want to talk about craeting a super simple application with Spring boot and latest version of Java.
We will learn how to create a basic application with a GET, POST, PUT & DELETE methods in it.
If you are new to the Spring Framework, this might be a good start for you

### How Can We Set up a Spring Boot Application with Maven?
First, we have to add the spring-boot-starter-parent project or package in a maven project and declare dependencies that are needed for run Spring Boot application. There are steps need to do for setup the spring boot project in maven application
Add spring-boot-starter-parent project to the parent element in pom.xml:
``` <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.1.RELEASE</version>
</parent>
```


In the Dependency section, we have to add the following dependency also in pom.xml
```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-
   .er-web</artifactId>
</dependency>
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <scope>runtime</scope>
   <optional>true</optional>
</dependency>
```
Then add the Following plugins dependency to the plugins section of pom.xml file
```
<build>
   <plugins>
      <plugin>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
   </plugins>
</build>
```
Then add the following code to the main class of the project
import org.springframework.boot.SpringApplication;
```
@SpringBootApplication
public class Application {
   public static void main(String[] args) {
      SpringApplication.run(StarterApplication.class, args);
   }
}
```
Then go to IDE, re-import all the project dependency. clean and build the maven project as a spring boot project.

<br>
Alternatively these steps can be done on the spring boot website as well, go to [Start Spring Boot](https://start.spring.io/).
- Then initialize and setup your project
- Download your project as a zip file
- Unzip the file
- Open the file as a Maven project in your IDE 
### Setting up the project online
- Setting up the project is quite easy from Spring Boot website
- Your setup should look something like this
![A test imagdce](/assets/dependancies.JPG)
![A test imaewwefge](/assets/project.JPG)

### Making a User.java file
This file will contain the information about our user and its attributes
``` 
/src/main/java/com/SpringProject/rest/webservices/restfulwebservices/user/User.java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import javax.validation.constraints.Past;
import javax.validation.constraints.Size;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;

@ApiModel(value="User Details", description="Contains all details of a user")
public class User {

	private Integer id;

	@Size(min=2, message="Name should have atleast 2 characters")
	@ApiModelProperty(notes = "Name should have atleast 2 characters")
	private String name;

	

	protected User() {

	}

	public User(Integer id, String name) {
		super();
		this.id = id;
		this.name = name;
	}

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	

	@Override
	public String toString() {
		return String.format("User [id=%s, name=%s]", id, name, );
	}

}
```
### Creating the functional methods to control our User
```
package com.Springproject.rest.webservices.restfulwebservices.user;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

import org.springframework.stereotype.Component;

@Component
public class UserDaoService {
	
	private static List<User> users = new ArrayList<>();

	private static int usersCount = 3;

	static {
		users.add(new User(1, "Adam", new Date()));
		users.add(new User(2, "Eve", new Date()));
		users.add(new User(3, "Jack", new Date()));
	}

	public List<User> findAll() {
		return users;
	}

	public User save(User user) {
		if (user.getId() == null) {
			user.setId(++usersCount);
		}
		users.add(user);
		return user;
	}
	public User savebyid(User user) {
		if (user.getId() == null) {
			user.setId(++usersCount);
		}
		users.add(user.getId(),user);
		return user;
	}
		

	public User findOne(int id) {
		for (User user : users) {
			if (user.getId() == id) {
				return user;
			}
		}
		return null;
	}

	public User deleteById(int id) {
		Iterator<User> iterator = users.iterator();
		while (iterator.hasNext()) {
			User user = iterator.next();
			if (user.getId() == id) {
				iterator.remove();
				return user;
			}
		}
		return null;
	}

}
```

### Creating a UserNotFoundException
```
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;

@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {
	public UserNotFoundException(String message) {
		super(message);
	}
}
```

### Creating all the imports required to make operations on our Users
```
import static org.springframework.hateoas.mvc.ControllerLinkBuilder.linkTo;
import static org.springframework.hateoas.mvc.ControllerLinkBuilder.methodOn;

import java.net.URI;
import java.util.List;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.hateoas.Resource;
import org.springframework.hateoas.mvc.ControllerLinkBuilder;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;
```

### Returning all the Users using mapping
```

@RestController
public class UserResource {

	@Autowired
	private UserDaoService service;

	@GetMapping("/users")
	public List<User> retrieveAllUsers() {
		return service.findAll();
	}

	}
```

### Returning user by a specific Id
```

	@GetMapping("/users/{id}")
	public Resource<User> retrieveUser(@PathVariable int id) {
		User user = service.findOne(id);
		
		if(user==null)
			throw new UserNotFoundException("id-"+ id);
		
		
			}
```

### Executing a POST operation 

Here we call the constructors and create a new User object to be posted
```
@PostMapping("/users")
	public ResponseEntity<Object> createUser(@Valid @RequestBody User user) {
		User savedUser = service.save(user);
		// CREATED
		
		
	}
```

#### Note - To test your POST executions you should download the POSTMAN tool and try executing queries 
### Executing a PUT request

```
@PutMapping("/users/{id}")
	public ResponseEntity<Object> createUser(@Valid @RequestBody User user) {
		User savedUser = service.savebyid(user);
		// CREATED
		
	}
```

### Executing a DELETE request
```
@DeleteMapping("/users/{id}")
	public void deleteUser(@PathVariable int id) {
		User user = service.deleteById(id);
		
		if(user==null)
			throw new UserNotFoundException("id-"+ id);		
	}
```

## Example Requests
### GET http://localhost:8080/users
```
[
    {
        "id": 1,
        "name": "Adam",
    },
    {
        "id": 2,
        "name": "Eve",
    },
    {
        "id": 3,
        "name": "Jack",
    }
]
```
### GET http://localhost:8080/users/1
```
{
    "id": 1,
    "name": "Adam",
}
```
### GET http://localhost:8080/users/1000
Get request to a non existing resource. <br>
The response shows default error message structure auto configured by Spring Boot.
``` 
{
    "timestamp": "2017-07-19T05:28:37.534+0000",
    "status": 404,
    "error": "Not Found",
    "message": "id-500",
    "path": "/users/500"
}
```

### Generating a Swagger file
```
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2WebMvc;

@Configuration
@EnableSwagger2WebMvc
public class SwaggerConfig {

	public static final Contact DEFAULT_CONTACT = new Contact(
			"Kartik Kumar", "www.404kartik.me");
	
	public static final ApiInfo DEFAULT_API_INFO = new ApiInfo(
			"Awesome API Title", "Awesome API Description", "1.0",
			"urn:tos", DEFAULT_CONTACT, 
			"Apache 2.0", "http://www.apache.org/licenses/LICENSE-2.0", Arrays.asList());

	private static final Set<String> DEFAULT_PRODUCES_AND_CONSUMES = 
			new HashSet<String>(Arrays.asList("application/json",
					"application/xml"));

	@Bean
	public Docket api() {
		return new Docket(DocumentationType.SWAGGER_2)
				.apiInfo(DEFAULT_API_INFO)
				.produces(DEFAULT_PRODUCES_AND_CONSUMES)
				.consumes(DEFAULT_PRODUCES_AND_CONSUMES);
	}
}
```

Thank you for joining in for this blog
