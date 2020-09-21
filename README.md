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
