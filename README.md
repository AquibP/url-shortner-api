# URL Shortner API

## How to use

git clone https://github.com/AquibP/url-shortner-api.git

Make sure to have MySQL server locally.

Open the project in IDE of your choice and make necessary changes to application.properties to map with SQL Database.

Build spring project

Open localhost:8080/swagger-ui.html

## Example:
Using Swagger make a post request by providing long URL as input and execute to get a short URL.

long URL: "https://github.com/AquibP/url-shortner-api.git"

Short URL: "l"

Append the short URL to "localhost:<port number>//. The URL should look like,

"http://localhost:8080/u.rl/l"

Paste the URL in browser to get redirected to original URL

## Working: 

### Introduction:
The URL shortner api is used to create short URL by consuming long URL. The short URL will redirects automatically to the long URL.

### URL Conversation:
The short URL is generated by converting numbers from base 10 to base 62. The base 10 digits are [0-9] and base 62 digits are[a-z][A-Z][0-9]. The base 62 provides significant number(depends on length of characters allowed in short URL) of characters for the generation of short URL.

### Implementation:
The API is implemented using spring boot and MySQL. 
Spring  Initializer: start.spring.io
Initialized the Mavan project with required dependencies, here we used Web and MySql.
The code is logically divided into different folders, config, controller, dto, entity, repository, service. The connection details are in application.property

### Swagger
Swagger Specification, is a specification for machine-readable interface files for describing, producing, consuming, and visualizing RESTful web services.
Swagger and some other tools can generate code, documentation and test cases given an interface file.
Setup:
    1. Add Maven dependency
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

    2. Java Configuration:
The select() method returns an instance of ApiSelectorBuilder, which provides a way to control the endpoints exposed by Swagger
@Bean
public Docket apiDocket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(metadata())
            .select()
            .apis(RequestHandlerSelectors.basePackage("com.aquib"))
            .build();
}

    3. Synchronization with code base/Request mapping with controller methods(endpoints):
Tell Swagger to route the requests to your controller and expose the API endpoints
@RequestMapping("/u.rl")
public class UrlController {

That’s it. Now the API endpoints will be visible through Swagger UI.

### Docker
Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. 
To dockerize our application we have used Docker's own build-file format: a Dockerfile. The file contains following commands :

FROM openjdk:13jdk-alpine

RUN addgroup -S spring && adduser -S spring -G spring

USER spring:spring

ARG JAR_FILE=target/*.jar

COPY ${JAR_FILE} app.jar

ENTRYPOINT ["java","-jar","/app.jar"]

FROM: The keyword FROM, tells Docker to use a given image with its tag as build-base. If this image is not in the local library, an online-search on DockerHub, or on any other configured remote-registry, is performed
RUN: With the RUN command, we're executing a shell command-line within the target system.
USER: to specify a non-root user for containers to run as.
ARG: defines a variable that can be passed at build time.
COPY: The last command tells Docker to COPY a few files from the local file-system, specifically a subfolder to the build directory, into the image in a given path
ENTRYPOINT: allows you to configure a container that will run as an executable.

### Architecture Diagram
![](images/Architecture%20Diagram.png)

