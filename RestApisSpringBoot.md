# Spring Boot REST API Complete Notes

---

# Table of Contents

1. What is REST?
2. What is an API?
3. What is HTTP?
4. HTTP Request & Response
5. HTTP Methods
6. Request Mapping
7. Controller vs RestController vs ResponseBody
8. Front Controller (DispatcherServlet)
9. CRUD Operations
10. Path Variable
11. Request Parameters
12. Request Body
13. Response Entity
14. HTTP Status Codes
15. Headers
16. Content-Type
17. Accept Header
18. Payload
19. Jackson Library
20. Lombok
21. Serialization & Deserialization
22. REST API Flow in Spring Boot
23. Interview Quick Revision

---

# 1. What is REST?

REST stands for:

```text
Representational State Transfer
```

REST is an architectural style used for building web services.

REST APIs use:

```text
HTTP Protocol
```

for communication between client and server.

Example:

```text
Mobile App
      |
      V
Spring Boot API
      |
      V
Database
```

---

# 2. What is an API?

API stands for:

```text
Application Programming Interface
```

An API allows two applications to communicate.

Example:

```text
Swiggy App
     |
     V
Restaurant API
```

The app requests data and the API sends data.

---

# 3. What is HTTP?

HTTP stands for:

```text
HyperText Transfer Protocol
```

Used for communication between:

```text
Client <----> Server
```

Examples:

```http
GET /products

POST /products

DELETE /products/1
```

---

# 4. HTTP Request & Response

## HTTP Request

Contains:

* URL
* Method
* Headers
* Body

Example:

```http
POST /products

Content-Type: application/json

{
   "name":"Pen",
   "price":10
}
```

---

## HTTP Response

Contains:

* Status Code
* Headers
* Body

Example:

```http
HTTP/1.1 201 Created

Content-Type: application/json

{
   "id":1,
   "name":"Pen"
}
```

---

# 5. HTTP Methods

HTTP Methods define the action to perform.

---

## GET

Used to fetch data.

Example:

```http
GET /products
```

Controller:

```java
@GetMapping("/products")
public List<Product> getProducts() {
    return products;
}
```

Use Cases:

* Get products
* Get users
* Get attendance

Properties:

* Safe
* Idempotent

---

## POST

Used to create data.

Example:

```http
POST /products
```

Request Body:

```json
{
  "name":"Pen",
  "price":10
}
```

Controller:

```java
@PostMapping("/products")
public Product create(
        @RequestBody Product product
) {
    return service.save(product);
}
```

Properties:

* Not Idempotent

---

## PUT

Used to completely replace an existing resource.

Example:

```http
PUT /products/1
```

Body:

```json
{
  "name":"Blue Pen",
  "price":20
}
```

Entire object replaced.

Properties:

* Idempotent

---

## PATCH

Used for partial updates.

Example:

```http
PATCH /products/1
```

Body:

```json
{
  "price":20
}
```

Only specified fields updated.

Properties:

* Usually Idempotent

Difference:

| PUT           | PATCH           |
| ------------- | --------------- |
| Full Update   | Partial Update  |
| Entire Object | Specific Fields |
| More Data     | Less Data       |

---

## DELETE

Used to remove data.

Example:

```http
DELETE /products/1
```

Controller:

```java
@DeleteMapping("/products/{id}")
public String delete(
        @PathVariable int id
){
    service.delete(id);
    return "Deleted";
}
```

Properties:

* Idempotent

---

## HEAD

Same as GET but returns only headers.

Example:

```http
HEAD /products
```

Used to check:

* File existence
* Content length

---

## OPTIONS

Returns allowed HTTP methods.

Example:

```http
OPTIONS /products
```

Response:

```http
Allow:
GET,POST,PUT,PATCH,DELETE
```

Used in:

```text
CORS
```

---

# 6. Request Mapping

Maps URLs to methods.

## Class Level

```java
@RestController
@RequestMapping("/products")
public class ProductController {
}
```

Base URL:

```text
/products
```

---

## Method Level

```java
@RequestMapping(
        method = RequestMethod.GET
)
```

Shortcut annotations:

```java
@GetMapping
@PostMapping
@PutMapping
@PatchMapping
@DeleteMapping
```

---

# 7. Controller vs RestController vs ResponseBody

## @Controller

Used for MVC applications.

Returns View.

```java
@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "home";
    }
}
```

Spring searches:

```text
home.jsp
home.html
```

---

## @ResponseBody

Converts returned object into JSON.

```java
@Controller
public class ProductController {

    @GetMapping("/product")
    @ResponseBody
    public Product getProduct() {
        return new Product("Pen",10);
    }
}
```

---

## @RestController

Combination of:

```java
@Controller
+
@ResponseBody
```

Example:

```java
@RestController
public class ProductController {

    @GetMapping("/product")
    public Product getProduct() {
        return new Product("Pen",10);
    }
}
```

Most REST APIs use:

```java
@RestController
```

---

# 8. Front Controller

Spring's Front Controller is:

```java
DispatcherServlet
```

Flow:

```text
Client
  |
  V
DispatcherServlet
  |
  V
Controller
  |
  V
Service
  |
  V
Repository
  |
  V
Database
```

Responsibilities:

* Receives request
* Finds controller
* Executes method
* Returns response

---

# 9. CRUD Operations

CRUD means:

```text
Create
Read
Update
Delete
```

| Operation      | HTTP Method |
| -------------- | ----------- |
| Create         | POST        |
| Read           | GET         |
| Update         | PUT         |
| Partial Update | PATCH       |
| Delete         | DELETE      |

---

# 10. Path Variable

Used to read values from URL.

URL:

```http
/products/10
```

Controller:

```java
@GetMapping("/products/{id}")
public Product get(
        @PathVariable int id
){
    return service.get(id);
}
```

Value:

```java
id = 10
```

---

## Multiple Path Variables

```java
@GetMapping(
"/users/{uid}/orders/{oid}"
)
```

```java
public String get(
    @PathVariable int uid,
    @PathVariable int oid
)
```

---

# 11. Request Parameters

Used for filtering/searching.

URL:

```http
/products?name=pen
```

Controller:

```java
@GetMapping("/products")
public Product search(
        @RequestParam String name
){
    return service.search(name);
}
```

---

# 12. Request Body

Reads incoming JSON.

Example:

```json
{
  "name":"Pen",
  "price":10
}
```

Controller:

```java
@PostMapping("/products")
public Product save(
        @RequestBody Product product
){
    return product;
}
```

---

# 13. ResponseEntity

Used to customize response.

Example:

```java
return ResponseEntity.ok(product);
```

---

## Custom Status

```java
return ResponseEntity
        .status(HttpStatus.CREATED)
        .body(product);
```

---

# 14. HTTP Status Codes

## 2xx Success

| Code | Meaning    |
| ---- | ---------- |
| 200  | OK         |
| 201  | Created    |
| 204  | No Content |

---

## 3xx Redirection

| Code | Meaning           |
| ---- | ----------------- |
| 301  | Moved Permanently |
| 302  | Found             |

---

## 4xx Client Error

| Code | Meaning      |
| ---- | ------------ |
| 400  | Bad Request  |
| 401  | Unauthorized |
| 403  | Forbidden    |
| 404  | Not Found    |

---

## 5xx Server Error

| Code | Meaning               |
| ---- | --------------------- |
| 500  | Internal Server Error |
| 503  | Service Unavailable   |

---

# 15. Headers

Headers provide metadata.

Examples:

```http
Authorization: Bearer Token
Content-Type: application/json
Accept: application/json
```

---

# 16. Content-Type

Tells server what type of data is sent.

JSON:

```http
Content-Type: application/json
```

XML:

```http
Content-Type: application/xml
```

Multipart:

```http
Content-Type: multipart/form-data
```

---

# 17. Accept Header

Tells server what format client expects.

Example:

```http
Accept: application/json
```

or

```http
Accept: application/xml
```

---

# 18. Payload

Payload = Actual data inside request body.

Example:

```json
{
  "name":"Pen",
  "price":10
}
```

This JSON is called payload.

---

# 19. Jackson Library

Jackson converts:

```text
Java Object <-> JSON
```

Spring Boot automatically includes Jackson through:

```xml
spring-boot-starter-web
```

---

## Java Object → JSON

```java
new Product("Pen",10)
```

becomes:

```json
{
  "name":"Pen",
  "price":10
}
```

Called:

```text
Serialization
```

---

## JSON → Java Object

```json
{
  "name":"Pen",
  "price":10
}
```

becomes:

```java
Product p
```

Called:

```text
Deserialization
```

---

## Useful Annotations

### @JsonIgnore

```java
@JsonIgnore
private String password;
```

---

### @JsonProperty

```java
@JsonProperty("product_name")
private String name;
```

Output:

```json
{
  "product_name":"Pen"
}
```

---

### @JsonInclude

```java
@JsonInclude(
Include.NON_NULL
)
```

Ignores null values.

---

# 20. Lombok

Lombok reduces boilerplate code.

Dependency:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

---

## @Getter

Creates getters.

```java
@Getter
private String name;
```

---

## @Setter

Creates setters.

```java
@Setter
private String name;
```

---

## @NoArgsConstructor

Creates:

```java
public Product(){}
```

---

## @AllArgsConstructor

Creates:

```java
public Product(
 String name,
 int price
){}
```

---

## @Data

Combination of:

```java
@Getter
@Setter
ToString
EqualsAndHashCode
RequiredArgsConstructor
```

---

# 21. Serialization & Deserialization

## Serialization

Java Object → JSON

```java
Product
```

↓

```json
{
  "name":"Pen"
}
```

---

## Deserialization

JSON → Java Object

```json
{
  "name":"Pen"
}
```

↓

```java
Product
```

---

# 22. REST API Flow in Spring Boot

```text
Client
   |
   V
HTTP Request
   |
   V
DispatcherServlet
   |
   V
Controller
   |
   V
Service
   |
   V
Repository
   |
   V
Database
   |
   V
Repository
   |
   V
Service
   |
   V
Controller
   |
   V
JSON Response
   |
   V
Client
```

---

# 23. Interview Quick Revision

1. REST = Representational State Transfer
2. API = Application Programming Interface
3. HTTP = HyperText Transfer Protocol
4. DispatcherServlet is Front Controller.
5. @RestController = @Controller + @ResponseBody
6. GET = Read Data
7. POST = Create Data
8. PUT = Full Update
9. PATCH = Partial Update
10. DELETE = Remove Data
11. @PathVariable reads value from URL.
12. @RequestParam reads query parameters.
13. @RequestBody reads JSON request body.
14. ResponseEntity customizes response.
15. Jackson converts Java Objects ↔ JSON.
16. Serialization = Object → JSON.
17. Deserialization = JSON → Object.
18. Content-Type tells format of request body.
19. Accept tells desired response format.
20. Payload = Actual data sent in body.
21. Lombok reduces boilerplate code.
22. 200 = OK
23. 201 = Created
24. 404 = Not Found
25. 500 = Internal Server Error
26. PUT replaces whole object.
27. PATCH updates selected fields.
28. POST is not idempotent.
29. GET, PUT, DELETE are idempotent.
30. Spring Boot REST APIs mostly use JSON.
