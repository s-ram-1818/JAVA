
# JSP & Servlets Complete Notes for Spring Boot Mastery

# Table of Contents
1. Introduction
2. Client Server Architecture
3. Static vs Dynamic Response
4. What is a Web Server
5. What is an Application Server
6. HTTP Protocol Basics
7. Request Response Cycle
8. What is Servlet
9. Servlet Lifecycle
10. Servlet API
11. Types of Servlet
12. Creating First Servlet
13. Deployment Descriptor (web.xml)
14. Annotations in Servlet
15. GenericServlet
16. HttpServlet
17. GET vs POST
18. RequestDispatcher
19. SendRedirect
20. ServletConfig
21. ServletContext
22. Session Management
23. Cookies
24. URL Rewriting
25. HttpSession
26. Hidden Form Fields
27. Filters
28. Listeners
29. Exception Handling
30. What is JSP
31. JSP Lifecycle
32. JSP Architecture
33. JSP Tags
34. JSP Directives
35. JSP Scripting Elements
36. JSP Implicit Objects
37. Expression Language (EL)
38. JSTL
39. MVC Architecture
40. Servlet + JSP Flow
41. WAR File
42. Apache Tomcat
43. JSP vs Servlet
44. Why Learn JSP & Servlets for Spring Boot
45. How Spring Boot Internally Uses Servlet
46. Interview Questions
47. Important Summary

---

# 1. Introduction

Before Spring Boot existed, Java web applications were mainly built using:
- Servlets
- JSP
- JDBC

Spring Boot is built on top of:
- Servlet API
- Embedded Tomcat
- DispatcherServlet

So understanding Servlets gives deep understanding of Spring Boot internals.

---

# 2. Client Server Architecture

## What is Client?

A client is a system that requests services.

Examples:
- Browser
- Mobile App
- Postman

## What is Server?

A server processes client requests and sends responses.

Examples:
- Tomcat
- Apache Server
- Node.js Server

---

# Architecture Flow

```text
Client (Browser)
       |
       | HTTP Request
       v
Web Server / Application Server
       |
       v
Servlet/JSP/Application Logic
       |
       v
Database
       |
       v
HTTP Response
       |
       v
Client (Browser)
````

---

# Real Example

```text
1. User enters:
   http://localhost:8080/login

2. Browser sends HTTP request

3. Tomcat receives request

4. Servlet processes request

5. Servlet fetches data from DB

6. Response sent back to browser
```

---

# 3. Static vs Dynamic Response

# Static Response

Fixed content.

Same response for every user.

Examples:

* HTML
* CSS
* Images

---

## Static Response Flow

```text
Browser -> Server -> HTML File -> Browser
```

---

## Example

```html
<h1>Welcome</h1>
```

Every user sees same output.

---

# Dynamic Response

Generated at runtime.

Different users may get different data.

Examples:

* Login page
* Dashboard
* Banking apps

---

## Dynamic Response Flow

```text
Browser -> Servlet/JSP -> Database -> Dynamic Output
```

---

## Example

```jsp
<%
String name = "Ram";
out.println(name);
%>
```

Output:

```text
Ram
```

---

# Difference Between Static and Dynamic Response

| Feature         | Static    | Dynamic              |
| --------------- | --------- | -------------------- |
| Data            | Fixed     | Generated at runtime |
| Speed           | Faster    | Slightly slower      |
| DB Usage        | No        | Yes                  |
| Personalization | No        | Yes                  |
| Example         | HTML page | Dashboard            |

---

# 4. What is a Web Server

A web server handles:

* Static content
* HTTP requests

Examples:

* Apache HTTP Server
* Nginx

---

# 5. What is an Application Server

Handles:

* Business logic
* Dynamic content
* Servlet execution

Examples:

* Tomcat
* JBoss
* GlassFish

---

# 6. HTTP Protocol Basics

HTTP = HyperText Transfer Protocol

Used for communication between:

* Client
* Server

---

# HTTP Methods

| Method | Use         |
| ------ | ----------- |
| GET    | Fetch data  |
| POST   | Send data   |
| PUT    | Update data |
| DELETE | Delete data |

---

# HTTP Status Codes

| Code | Meaning      |
| ---- | ------------ |
| 200  | Success      |
| 404  | Not Found    |
| 500  | Server Error |
| 403  | Forbidden    |

---

# 7. Request Response Cycle

```text
1. Browser sends request
2. Server receives request
3. Servlet processes request
4. Response generated
5. Browser displays output
```

---

# 8. What is Servlet

Servlet is a Java program that runs on server side and handles HTTP requests.

Package:

```java
jakarta.servlet
```

Old package:

```java
javax.servlet
```

---

# Features of Servlet

* Platform independent
* Server side
* Dynamic response generation
* Better than CGI

---

# 9. Servlet Lifecycle

Lifecycle controlled by container (Tomcat).

## Methods

### 1) init()

Called once when servlet loads.

```java
public void init()
```

---

### 2) service()

Handles requests.

```java
public void service()
```

---

### 3) destroy()

Called before servlet removal.

```java
public void destroy()
```

---

# Lifecycle Diagram

```text
Load Servlet
     |
     v
init()
     |
     v
service()
     |
     v
destroy()
```

---

# 10. Servlet API

Main Interfaces and Classes:

| Component           | Purpose              |
| ------------------- | -------------------- |
| Servlet             | Base interface       |
| GenericServlet      | Protocol independent |
| HttpServlet         | HTTP specific        |
| HttpServletRequest  | Client request       |
| HttpServletResponse | Server response      |

---

# 11. Types of Servlet

## 1) GenericServlet

* Protocol independent

## 2) HttpServlet

* HTTP based
* Most commonly used

---

# 12. Creating First Servlet

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class HelloServlet extends HttpServlet {

    protected void doGet(HttpServletRequest req,
                         HttpServletResponse res)
            throws ServletException, IOException {

        PrintWriter out = res.getWriter();

        out.println("<h1>Hello Servlet</h1>");
    }
}
```

---

# 13. Deployment Descriptor (web.xml)

Used for servlet configuration.

```xml
<web-app>

    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>HelloServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

</web-app>
```

---

# 14. Annotations in Servlet

Modern way.

```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {

}
```

---

# 15. GenericServlet

Abstract class implementing Servlet interface.

Protocol independent.

```java
public class Demo extends GenericServlet {

    public void service(ServletRequest req,
                        ServletResponse res) {

    }
}
```

---

# 16. HttpServlet

Most important servlet class.

Supports:

* GET
* POST
* PUT
* DELETE

Methods:

* doGet()
* doPost()
* doPut()
* doDelete()

---

# 17. GET vs POST

| Feature      | GET      | POST    |
| ------------ | -------- | ------- |
| Data visible | Yes      | No      |
| Security     | Less     | More    |
| Data size    | Limited  | Large   |
| Used for     | Fetching | Sending |

---

# Example GET

```java
protected void doGet(HttpServletRequest req,
                     HttpServletResponse res)
```

---

# Example POST

```java
protected void doPost(HttpServletRequest req,
                      HttpServletResponse res)
```

---

# 18. RequestDispatcher

Used to forward request.

```java
RequestDispatcher rd =
request.getRequestDispatcher("home.jsp");

rd.forward(request, response);
```

---

# 19. SendRedirect

Redirects client to another resource.

```java
response.sendRedirect("home.jsp");
```

---

# Forward vs Redirect

| Feature     | Forward | Redirect |
| ----------- | ------- | -------- |
| Server side | Yes     | No       |
| New request | No      | Yes      |
| URL changes | No      | Yes      |

---

# 20. ServletConfig

Used for servlet-specific configuration.

```java
ServletConfig config = getServletConfig();
```

---

# 21. ServletContext

Shared across application.

```java
ServletContext context =
getServletContext();
```

---

# 22. Session Management

HTTP is stateless.

Session tracking needed for:

* Login
* Shopping cart

---

# Session Tracking Techniques

1. Cookies
2. URL Rewriting
3. Hidden Fields
4. HttpSession

---

# 23. Cookies

Stored in browser.

```java
Cookie c = new Cookie("name", "Ram");

response.addCookie(c);
```

---

# Read Cookie

```java
Cookie[] cookies = request.getCookies();
```

---

# 24. URL Rewriting

```text
/profile?user=ram
```

---

# 25. HttpSession

Most used session technique.

```java
HttpSession session =
request.getSession();

session.setAttribute("name", "Ram");
```

---

# Get Session Data

```java
String name =
(String) session.getAttribute("name");
```

---

# 26. Hidden Form Fields

```html
<input type="hidden"
       name="id"
       value="101">
```

---

# 27. Filters

Used before and after request processing.

Examples:

* Authentication
* Logging
* Validation

---

# Filter Flow

```text
Request -> Filter -> Servlet -> Response
```

---

# Example Filter

```java
@WebFilter("/*")
public class MyFilter implements Filter {

    public void doFilter(ServletRequest req,
                         ServletResponse res,
                         FilterChain chain) {

        chain.doFilter(req, res);
    }
}
```

---

# 28. Listeners

Used for event handling.

Examples:

* Session creation
* Context initialization

---

# Example

```java
@WebListener
public class MyListener
implements ServletContextListener {

}
```

---

# 29. Exception Handling

```java
try {

} catch(Exception e) {

}
```

---

# 30. What is JSP

JSP = Java Server Pages

Used to create dynamic web pages.

Extension:

```text
.jsp
```

---

# JSP Internally

JSP gets converted into Servlet by Tomcat.

```text
JSP -> Servlet -> Bytecode
```

---

# 31. JSP Lifecycle

```text
1. Translation
2. Compilation
3. Class Loading
4. Instantiation
5. jspInit()
6. _jspService()
7. jspDestroy()
```

---

# 32. JSP Architecture

```text
Browser
   |
   v
JSP Page
   |
   v
Converted to Servlet
   |
   v
Response
```

---

# 33. JSP Tags

# 1) Declaration Tag

```jsp
<%! int a = 10; %>
```

---

# 2) Scriptlet Tag

```jsp
<%
out.println("Hello");
%>
```

---

# 3) Expression Tag

```jsp
<%= 10 + 20 %>
```

---

# 34. JSP Directives

## page directive

```jsp
<%@ page language="java" %>
```

---

## include directive

```jsp
<%@ include file="header.jsp" %>
```

---

## taglib directive

Used for JSTL.

---

# 35. JSP Scripting Elements

| Element     | Syntax   |
| ----------- | -------- |
| Declaration | `<%! %>` |
| Scriptlet   | `<% %>`  |
| Expression  | `<%= %>` |

---

# 36. JSP Implicit Objects

| Object      | Purpose         |
| ----------- | --------------- |
| request     | Client request  |
| response    | Server response |
| session     | Session object  |
| application | ServletContext  |
| out         | PrintWriter     |

---

# 37. Expression Language (EL)

Simplifies JSP code.

```jsp
${user.name}
```

Instead of:

```jsp
<%= user.getName() %>
```

---

# 38. JSTL

JSP Standard Tag Library

Used instead of Java code inside JSP.

---

# Core JSTL Tags

## if

```jsp
<c:if test="${a > b}">
</c:if>
```

---

## forEach

```jsp
<c:forEach var="i" items="${list}">
</c:forEach>
```

---

# 39. MVC Architecture

MVC = Model View Controller

| Component  | Role           |
| ---------- | -------------- |
| Model      | Business logic |
| View       | JSP            |
| Controller | Servlet        |

---

# MVC Flow

```text
Browser
   |
   v
Servlet (Controller)
   |
   v
Business Logic
   |
   v
JSP (View)
```

---

# 40. Servlet + JSP Flow

```text
1. Request from browser
2. Servlet receives request
3. Process logic
4. Store data in request/session
5. Forward to JSP
6. JSP displays output
```

---

# Example

## Servlet

```java
request.setAttribute("name", "Ram");

RequestDispatcher rd =
request.getRequestDispatcher("home.jsp");

rd.forward(request, response);
```

---

## JSP

```jsp
${name}
```

---

# 41. WAR File

WAR = Web Application Archive

Contains:

* JSP
* Servlet classes
* web.xml
* Libraries

Generated using:

* Maven
* Gradle

---

# 42. Apache Tomcat

Tomcat is:

* Web server
* Servlet container

Responsibilities:

* Runs servlets
* Converts JSP into servlet
* Handles lifecycle

---

# Tomcat Directory

| Folder  | Purpose       |
| ------- | ------------- |
| bin     | Startup files |
| webapps | Deploy apps   |
| conf    | Config files  |
| lib     | Libraries     |

---

# 43. JSP vs Servlet

| Feature      | JSP             | Servlet |
| ------------ | --------------- | ------- |
| UI           | Easier          | Harder  |
| Logic        | Difficult       | Better  |
| HTML writing | Easy            | Hard    |
| Performance  | Slightly slower | Faster  |

---

# Best Practice

Use:

* Servlet for logic
* JSP for UI

---

# 44. Why Learn JSP & Servlets for Spring Boot

Spring Boot internally uses:

* DispatcherServlet
* Embedded Tomcat
* Servlet container

If you understand Servlets:

* Spring MVC becomes easier
* Request lifecycle becomes easy
* Filters/interceptors easier
* Security concepts easier

---

# 45. How Spring Boot Internally Uses Servlet

## Flow

```text
Browser
   |
   v
DispatcherServlet
   |
   v
Controller
   |
   v
Service
   |
   v
Repository
   |
   v
Database
```

---

# DispatcherServlet

Heart of Spring MVC.

Acts as Front Controller.

---

# Spring Boot Mapping Example

```java
@GetMapping("/hello")
public String hello() {
    return "Hello";
}
```

Internally handled using Servlet concepts.

---

# 46. Important Interview Questions

# Servlet Questions

1. What is Servlet?
2. Difference between GenericServlet and HttpServlet?
3. Servlet lifecycle?
4. GET vs POST?
5. Forward vs Redirect?
6. What is session management?
7. Difference between ServletConfig and ServletContext?
8. What is Filter?
9. What is Listener?

---

# JSP Questions

1. What is JSP?
2. JSP lifecycle?
3. JSP implicit objects?
4. Difference between JSP and Servlet?
5. What is EL?
6. What is JSTL?

---

# Spring Boot Related Questions

1. What is DispatcherServlet?
2. How Spring Boot uses embedded Tomcat?
3. What is Front Controller pattern?
4. Difference between JSP MVC and Spring MVC?

---

# 47. Important Summary

# Must Know for Spring Boot

## Very Important Servlet Topics

* Servlet lifecycle
* HttpServlet
* Request/Response
* Session management
* Filters
* MVC architecture
* RequestDispatcher
* Redirect vs Forward

---

# Very Important JSP Topics

* JSP lifecycle
* EL
* JSTL
* Implicit objects

---

# Most Important Concept

```text
Spring Boot is built on top of Servlet architecture.
```

If Servlet basics are strong:

* Spring MVC becomes easy
* Security becomes easy
* REST APIs easier
* Request lifecycle easier

---

# Recommended Next Learning After This

1. Maven
2. JDBC
3. Hibernate
4. Spring Core
5. Spring MVC
6. Spring Boot
7. Spring Security
8. JPA/Hibernate
9. REST APIs
10. Microservices

---

# Final Architecture Understanding

```text
Client
   |
HTTP Request
   |
Tomcat
   |
Servlet Container
   |
DispatcherServlet
   |
Controller
   |
Service
   |
Repository
   |
Database
   |
HTTP Response
   |
Client
```

```
```
