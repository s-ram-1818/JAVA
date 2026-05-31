# ResponseEntity in Spring Boot

## What is ResponseEntity?

`ResponseEntity<T>` is a Spring class used to represent the **entire HTTP response**.

It allows you to control:

1. Response Body
2. HTTP Status Code
3. HTTP Headers

Unlike returning a plain object, `ResponseEntity` gives full control over the response sent to the client.

---

# Why Use ResponseEntity?

Without `ResponseEntity`, Spring automatically returns:

* Status Code: 200 OK
* Response Body: Returned Object

Example:

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

You cannot easily customize the status code.

---

# ResponseEntity Syntax

```java
ResponseEntity<T>
```

Where:

* T = Type of Response Body

Examples:

```java
ResponseEntity<String>
ResponseEntity<Product>
ResponseEntity<List<Product>>
ResponseEntity<Void>
```

---

# Basic Example

```java
@GetMapping("/hello")
public ResponseEntity<String> hello() {

    return ResponseEntity.ok("Hello World");
}
```

Response:

```http
200 OK
```

```json
"Hello World"
```

---

# ResponseEntity Methods

## 1. ok()

Returns:

```http
200 OK
```

Example:

```java
return ResponseEntity.ok(product);
```

Equivalent:

```java
return ResponseEntity.status(HttpStatus.OK)
                     .body(product);
```

---

## 2. status()

Used for custom status codes.

Example:

```java
return ResponseEntity
       .status(HttpStatus.CREATED)
       .body("Product Added");
```

Response:

```http
201 Created
```

---

## 3. badRequest()

Returns:

```http
400 Bad Request
```

Example:

```java
return ResponseEntity
       .badRequest()
       .body("Invalid Input");
```

---

## 4. notFound()

Returns:

```http
404 Not Found
```

Example:

```java
return ResponseEntity
       .notFound()
       .build();
```

---

## 5. noContent()

Returns:

```http
204 No Content
```

Example:

```java
return ResponseEntity
       .noContent()
       .build();
```

---

## 6. internalServerError()

Returns:

```http
500 Internal Server Error
```

Example:

```java
return ResponseEntity
       .internalServerError()
       .body("Something went wrong");
```

---

# CRUD Examples

## GET All Products

```java
@GetMapping("/products")
public ResponseEntity<List<Product>> getProducts() {

    List<Product> products =
            productService.getAllProducts();

    return ResponseEntity.ok(products);
}
```

Response:

```http
200 OK
```

---

## GET Product By ID

```java
@GetMapping("/products/{id}")
public ResponseEntity<Product> getProduct(
        @PathVariable Integer id) {

    Product product =
            productRepo.findById(id)
                       .orElse(null);

    if(product == null) {
        return ResponseEntity.notFound().build();
    }

    return ResponseEntity.ok(product);
}
```

Possible Responses:

```http
200 OK
```

or

```http
404 Not Found
```

---

## POST Product

```java
@PostMapping("/products")
public ResponseEntity<String> addProduct(
        @RequestBody Product product) {

    productRepo.save(product);

    return ResponseEntity
            .status(HttpStatus.CREATED)
            .body("Product Added Successfully");
}
```

Response:

```http
201 Created
```

---

## UPDATE Product

```java
@PutMapping("/products/{id}")
public ResponseEntity<String> updateProduct(
        @PathVariable Integer id,
        @RequestBody Product product) {

    if(!productRepo.existsById(id)) {
        return ResponseEntity.notFound().build();
    }

    product.setId(id);
    productRepo.save(product);

    return ResponseEntity.ok("Updated Successfully");
}
```

---

## DELETE Product

```java
@DeleteMapping("/products/{id}")
public ResponseEntity<Void> deleteProduct(
        @PathVariable Integer id) {

    if(!productRepo.existsById(id)) {
        return ResponseEntity.notFound().build();
    }

    productRepo.deleteById(id);

    return ResponseEntity.noContent().build();
}
```

Response:

```http
204 No Content
```

---

# Returning Custom Headers

Example:

```java
@GetMapping("/version")
public ResponseEntity<String> getVersion() {

    return ResponseEntity
            .ok()
            .header("App-Version", "1.0")
            .body("Spring Boot App");
}
```

Response:

```http
200 OK

App-Version: 1.0
```

---

# Common HTTP Status Codes

| Status Code | Meaning               |
| ----------- | --------------------- |
| 200         | OK                    |
| 201         | Created               |
| 204         | No Content            |
| 400         | Bad Request           |
| 401         | Unauthorized          |
| 403         | Forbidden             |
| 404         | Not Found             |
| 500         | Internal Server Error |

---

# ResponseEntity<Void>

Used when no body is required.

Example:

```java
return ResponseEntity.noContent().build();
```

Type:

```java
ResponseEntity<Void>
```

---

# ResponseEntity vs Returning Object Directly

## Direct Return

```java
@GetMapping
public Product getProduct() {
    return product;
}
```

Pros:

* Simple

Cons:

* Cannot control status code
* Cannot add headers

---

## ResponseEntity

```java
@GetMapping
public ResponseEntity<Product> getProduct() {
    return ResponseEntity.ok(product);
}
```

Pros:

* Control Status Code
* Control Headers
* Better Error Handling
* Production Ready

---

# Interview Questions

## What is ResponseEntity?

ResponseEntity is a Spring class that represents the complete HTTP response including body, headers, and status code.

---

## Why use ResponseEntity?

To return custom status codes, headers, and responses from REST APIs.

---

## Difference Between @ResponseBody and ResponseEntity?

### @ResponseBody

Returns only body.

```java
@ResponseBody
public Product getProduct()
```

### ResponseEntity

Returns:

* Body
* Status Code
* Headers

```java
public ResponseEntity<Product> getProduct()
```

---

# Best Practice

For production REST APIs:

* Use `ResponseEntity`
* Return proper status codes
* Handle errors properly
* Avoid returning plain Strings unless necessary

Example:

```java
return ResponseEntity.ok(data);

return ResponseEntity.notFound().build();

return ResponseEntity.status(HttpStatus.CREATED)
                     .body(data);
```
