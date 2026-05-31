# ResponseEntity in Spring Boot - Complete Notes

## What is ResponseEntity?

`ResponseEntity<T>` is a Spring Framework class that represents the **entire HTTP response**.

It provides control over:

1. Response Body
2. HTTP Status Code
3. HTTP Headers

Package:

```java
import org.springframework.http.ResponseEntity;
```

---

# Why Use ResponseEntity?

Without ResponseEntity:

```java
@GetMapping("/hello")
public String hello() {
    return "Hello World";
}
```

Response:

```http
200 OK
```

```json
"Hello World"
```

You cannot easily control:

* Status Code
* Headers

With ResponseEntity:

```java
@GetMapping("/hello")
public ResponseEntity<String> hello() {
    return ResponseEntity.ok("Hello World");
}
```

Now you can control body, headers, and status.

---

# HTTP Response Structure

Every HTTP Response contains:

```text
Status Line
Headers
Body
```

Example:

```http
HTTP/1.1 200 OK

Content-Type: application/json

{
   "name":"Laptop"
}
```

ResponseEntity controls all of them.

---

# Syntax

```java
ResponseEntity<T>
```

Where `T` is the body type.

Examples:

```java
ResponseEntity<String>

ResponseEntity<Product>

ResponseEntity<List<Product>>

ResponseEntity<Map<String,Object>>

ResponseEntity<Void>

ResponseEntity<?>

ResponseEntity<Object>
```

---

# Generic Types

## String Response

```java
ResponseEntity<String>
```

```java
return ResponseEntity.ok("Success");
```

---

## Object Response

```java
ResponseEntity<Product>
```

```java
return ResponseEntity.ok(product);
```

---

## List Response

```java
ResponseEntity<List<Product>>
```

```java
return ResponseEntity.ok(products);
```

---

## Map Response

```java
ResponseEntity<Map<String,Object>>
```

```java
Map<String,Object> response = new HashMap<>();

response.put("success",true);
response.put("message","Added");

return ResponseEntity.ok(response);
```

---

## No Body

```java
ResponseEntity<Void>
```

```java
return ResponseEntity.noContent().build();
```

---

# ResponseEntity<?> (Unknown Response Type)

Used when success and error responses are different.

Example:

```java
@GetMapping("/product/{id}")
public ResponseEntity<?> getProduct(
        @PathVariable Integer id) {

    Product product =
            productRepo.findById(id)
                       .orElse(null);

    if(product == null) {
        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body("Product Not Found");
    }

    return ResponseEntity.ok(product);
}
```

Possible Responses:

```java
Product
String
List<Product>
Map<String,Object>
```

The wildcard `?` means:

```text
Any Type
```

---

# ResponseEntity<Object>

```java
@GetMapping("/test")
public ResponseEntity<Object> test() {

    if(true)
        return ResponseEntity.ok(new Product());

    return ResponseEntity.badRequest()
                         .body("Error");
}
```

Useful when multiple object types can be returned.

---

# Difference Between ? and Object

### ResponseEntity<?>

```java
ResponseEntity<?>
```

Means:

```text
Unknown Type
```

Preferred for mixed responses.

---

### ResponseEntity<Object>

```java
ResponseEntity<Object>
```

Means:

```text
Body is Object
```

Also works but less expressive.

---

# Common Methods

## 1. ok()

Returns:

```http
200 OK
```

```java
return ResponseEntity.ok(product);
```

Equivalent:

```java
return ResponseEntity
       .status(HttpStatus.OK)
       .body(product);
```

---

## 2. status()

Used for custom status.

```java
return ResponseEntity
       .status(HttpStatus.CREATED)
       .body(product);
```

Response:

```http
201 Created
```

---

## 3. created()

Used after resource creation.

```java
URI location =
        URI.create("/products/1");

return ResponseEntity
        .created(location)
        .body(product);
```

Response:

```http
201 Created
Location: /products/1
```

---

## 4. accepted()

Returns:

```http
202 Accepted
```

```java
return ResponseEntity
       .accepted()
       .body("Processing");
```

---

## 5. badRequest()

Returns:

```http
400 Bad Request
```

```java
return ResponseEntity
       .badRequest()
       .body("Invalid Input");
```

---

## 6. notFound()

Returns:

```http
404 Not Found
```

```java
return ResponseEntity
       .notFound()
       .build();
```

---

## 7. noContent()

Returns:

```http
204 No Content
```

```java
return ResponseEntity
       .noContent()
       .build();
```

---

## 8. internalServerError()

Returns:

```http
500 Internal Server Error
```

```java
return ResponseEntity
       .internalServerError()
       .body("Server Error");
```

---

# CRUD Examples

## GET All

```java
@GetMapping("/products")
public ResponseEntity<List<Product>> getProducts() {

    return ResponseEntity.ok(
            productService.getAllProducts()
    );
}
```

---

## GET By ID

```java
@GetMapping("/products/{id}")
public ResponseEntity<Product> getProduct(
        @PathVariable Integer id) {

    Product product =
            productRepo.findById(id)
                       .orElse(null);

    if(product == null)
        return ResponseEntity.notFound().build();

    return ResponseEntity.ok(product);
}
```

---

## POST

```java
@PostMapping("/products")
public ResponseEntity<Product> addProduct(
        @RequestBody Product product) {

    Product saved =
            productRepo.save(product);

    return ResponseEntity
            .status(HttpStatus.CREATED)
            .body(saved);
}
```

---

## PUT

```java
@PutMapping("/products/{id}")
public ResponseEntity<Product> updateProduct(
        @PathVariable Integer id,
        @RequestBody Product product) {

    if(!productRepo.existsById(id))
        return ResponseEntity.notFound().build();

    product.setId(id);

    return ResponseEntity.ok(
            productRepo.save(product)
    );
}
```

---

## DELETE

```java
@DeleteMapping("/products/{id}")
public ResponseEntity<Void> deleteProduct(
        @PathVariable Integer id) {

    if(!productRepo.existsById(id))
        return ResponseEntity.notFound().build();

    productRepo.deleteById(id);

    return ResponseEntity.noContent().build();
}
```

---

# Custom Headers

```java
@GetMapping("/version")
public ResponseEntity<String> version() {

    return ResponseEntity
            .ok()
            .header("App-Version","1.0")
            .header("Company","ABC")
            .body("Running");
}
```

Response:

```http
200 OK

App-Version: 1.0
Company: ABC
```

---

# Builder Pattern

ResponseEntity uses Builder Pattern.

```java
return ResponseEntity
        .status(HttpStatus.CREATED)
        .header("Version","1.0")
        .body(product);
```

Flow:

```java
ResponseEntity
      .status(...)
      .header(...)
      .body(...)
```

---

# HTTP Status Codes

## Success

| Code | Meaning    |
| ---- | ---------- |
| 200  | OK         |
| 201  | Created    |
| 202  | Accepted   |
| 204  | No Content |

---

## Client Errors

| Code | Meaning            |
| ---- | ------------------ |
| 400  | Bad Request        |
| 401  | Unauthorized       |
| 403  | Forbidden          |
| 404  | Not Found          |
| 405  | Method Not Allowed |

---

## Server Errors

| Code | Meaning               |
| ---- | --------------------- |
| 500  | Internal Server Error |
| 502  | Bad Gateway           |
| 503  | Service Unavailable   |

---

# ResponseEntity vs @ResponseBody

## @ResponseBody

```java
@ResponseBody
public Product getProduct() {
    return product;
}
```

Controls:

* Body Only

---

## ResponseEntity

```java
public ResponseEntity<Product> getProduct() {
    return ResponseEntity.ok(product);
}
```

Controls:

* Body
* Status Code
* Headers

---

# ResponseEntity vs @ResponseStatus

## @ResponseStatus

```java
@ResponseStatus(HttpStatus.CREATED)
@PostMapping
public Product addProduct() {
    return product;
}
```

Always returns:

```http
201 Created
```

Static response.

---

## ResponseEntity

```java
if(success)
    return ResponseEntity.ok(product);

return ResponseEntity.notFound().build();
```

Dynamic response.

---

# Exception Handling

```java
@ExceptionHandler(Exception.class)
public ResponseEntity<String> handleException(
        Exception ex) {

    return ResponseEntity
            .internalServerError()
            .body(ex.getMessage());
}
```

---

# Best Practices

### Use ResponseEntity in REST APIs

```java
ResponseEntity<Product>
```

instead of

```java
Product
```

---

### Return Proper Status Codes

Create:

```http
201 Created
```

Delete:

```http
204 No Content
```

Not Found:

```http
404 Not Found
```

---

### Use Structured Error Responses

```java
Map<String,Object> error =
        new HashMap<>();

error.put("error","Invalid Input");
error.put("status",400);

return ResponseEntity
        .badRequest()
        .body(error);
```

Response:

```json
{
  "error":"Invalid Input",
  "status":400
}
```

---

# Quick Revision Sheet

```java
ResponseEntity.ok(body);

ResponseEntity.status(HttpStatus.CREATED)
              .body(body);

ResponseEntity.created(uri)
              .body(body);

ResponseEntity.accepted()
              .body(body);

ResponseEntity.badRequest()
              .body(body);

ResponseEntity.notFound()
              .build();

ResponseEntity.noContent()
              .build();

ResponseEntity.internalServerError()
              .body(body);
```

---

# Interview Answers

### What is ResponseEntity?

ResponseEntity is a Spring Framework class that represents the complete HTTP response including body, status code, and headers.

---

### Why use ResponseEntity?

To gain complete control over REST API responses.

---

### What does ResponseEntity control?

1. Body
2. Status Code
3. Headers

---

### When to use ResponseEntity<?>?

When the method can return different response body types.

---

### When to use ResponseEntity<Void>?

When no response body is required.

---

### Formula to Remember

```text
ResponseEntity
=
Body
+
Status Code
+
Headers
```
