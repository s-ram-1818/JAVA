# Spring Boot Logging - Complete Industry-Level Notes

# Table of Contents

1. Introduction to Logging
2. Why Logging is Important
3. Logging Architecture in Spring Boot
4. SLF4J
5. Logback
6. Logging Levels
7. Creating Logger
8. Lombok @Slf4j
9. Logging Best Practices
10. Log Message Formatting
11. Exception Logging
12. Logging Configuration
13. Package-Level Logging
14. Logging to File
15. Custom Log Patterns
16. Logback Configuration
17. Rolling Log Files
18. Asynchronous Logging
19. MDC (Mapped Diagnostic Context)
20. Correlation IDs
21. Request & Response Logging
22. Logging in Controllers
23. Logging in Services
24. Logging in Repositories
25. Logging in Exception Handlers
26. Logging in Microservices
27. Logging Security Considerations
28. Log Aggregation Tools
29. Monitoring and Observability
30. Industry Best Practices
31. Common Interview Questions

---

# 1. Introduction to Logging

Logging is the process of recording application events, errors, warnings, debugging information, and business activities.

Instead of:

```java
System.out.println("User Created");
```

Industry uses:

```java
log.info("User Created");
```

Logs help developers:

- Debug issues
- Monitor applications
- Audit user actions
- Investigate production failures
- Analyze system behavior

---

# 2. Why Logging is Important

## Debugging

```java
log.debug("User object: {}", user);
```

---

## Error Tracking

```java
log.error("Database connection failed", e);
```

---

## Monitoring

```java
log.info("Application Started");
```

---

## Security Auditing

```java
log.info("User {} logged in", username);
```

---

## Production Support

Without logging:

```java
500 Internal Server Error
```

No clue what happened.

With logging:

```java
Database Timeout
Connection Refused
Invalid JWT Token
```

Easy to identify issue.

---

# 3. Logging Architecture in Spring Boot

Spring Boot Logging Stack:

```text
Application
     ↓
SLF4J
     ↓
Logback
     ↓
Console/File
```

Default dependency:

```xml
spring-boot-starter-logging
```

Contains:

- SLF4J
- Logback

---

# 4. SLF4J

## Simple Logging Facade for Java

SLF4J is not a logging framework.

It is an abstraction layer.

```text
Application
     ↓
SLF4J
     ↓
Logback / Log4j2 / JUL
```

Benefits:

- Loose coupling
- Easy framework switching
- Industry standard

Example:

```java
Logger logger =
LoggerFactory.getLogger(UserService.class);
```

---

# 5. Logback

Default logging framework in Spring Boot.

Features:

- High performance
- Rolling files
- Async logging
- File rotation
- Log filtering

Configuration file:

```text
logback-spring.xml
```

---

# 6. Logging Levels

## TRACE

Very detailed information.

```java
log.trace("Method Entered");
```

Used rarely.

---

## DEBUG

Developer debugging information.

```java
log.debug("User Object: {}", user);
```

---

## INFO

Business events.

```java
log.info("Order Created");
```

Most used level.

---

## WARN

Potential problem.

```java
log.warn("Cache Miss");
```

---

## ERROR

Application failure.

```java
log.error("Payment Failed");
```

---

# Priority

```text
TRACE
DEBUG
INFO
WARN
ERROR
```

If level = INFO

Shown:

```text
INFO
WARN
ERROR
```

Hidden:

```text
TRACE
DEBUG
```

---

# 7. Creating Logger

## Traditional Way

```java
private static final Logger log =
LoggerFactory.getLogger(UserService.class);
```

---

# 8. Lombok @Slf4j

Most common in industry.

```java
@Slf4j
@Service
public class UserService {
}
```

Use directly:

```java
log.info("User Created");
```

Dependency:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

---

# 9. Logging Best Practices

## Avoid System.out.println

Bad:

```java
System.out.println("Hello");
```

Good:

```java
log.info("Hello");
```

---

## Use Correct Level

Debugging:

```java
log.debug("Payload {}", request);
```

Business Event:

```java
log.info("Order Created");
```

Error:

```java
log.error("Database Error");
```

---

# 10. Log Message Formatting

Bad:

```java
log.info("User " + user.getName());
```

String is always created.

Good:

```java
log.info("User {}", user.getName());
```

---

Multiple Values:

```java
log.info(
    "User {} logged in from {}",
    username,
    ipAddress
);
```

---

# 11. Exception Logging

Bad:

```java
log.error(e.getMessage());
```

Only message printed.

Good:

```java
log.error("Unexpected Error", e);
```

Produces full stack trace.

---

# 12. Logging Configuration

application.properties

```properties
logging.level.root=INFO
```

---

Enable Debug:

```properties
logging.level.root=DEBUG
```

---

Enable Trace:

```properties
logging.level.root=TRACE
```

---

# 13. Package-Level Logging

```properties
logging.level.com.company=DEBUG
```

Example:

```properties
logging.level.com.ecom.service=DEBUG
logging.level.org.springframework=WARN
```

Result:

```text
Application → DEBUG
Spring → WARN
```

---

# 14. Logging to File

```properties
logging.file.name=logs/app.log
```

Creates:

```text
logs/app.log
```

---

Using Folder:

```properties
logging.file.path=logs
```

---

# 15. Custom Log Patterns

```properties
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
```

Output:

```text
2026-06-02 10:30:12
[main]
INFO
UserService
- User Created
```

---

# 16. Logback Configuration

Create:

```text
src/main/resources/logback-spring.xml
```

Example:

```xml
<configuration>

    <root level="INFO">
        <appender-ref ref="CONSOLE"/>
    </root>

</configuration>
```

---

# 17. Rolling Log Files

Prevent huge log files.

```xml
<rollingPolicy
class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">

    <fileNamePattern>
        logs/app-%d{yyyy-MM-dd}.log
    </fileNamePattern>

</rollingPolicy>
```

Generated:

```text
app-2026-06-01.log
app-2026-06-02.log
app-2026-06-03.log
```

---

# 18. Asynchronous Logging

Improves performance.

Instead of:

```text
Application
    ↓
Write Log
    ↓
Continue
```

Use:

```text
Application
    ↓
Queue
    ↓
Background Thread
```

Example:

```xml
<appender name="ASYNC"
class="ch.qos.logback.classic.AsyncAppender">

    <appender-ref ref="FILE"/>

</appender>

<root level="INFO">
    <appender-ref ref="ASYNC"/>
</root>
```

Used in high-traffic systems.

---

# 19. MDC (Mapped Diagnostic Context)

Adds extra data to every log.

Example:

```java
MDC.put("requestId",
UUID.randomUUID().toString());
```

```java
log.info("Request Started");
```

Output:

```text
[requestId=12345]
Request Started
```

Useful for:

- Microservices
- Distributed systems
- Request tracing

---

# 20. Correlation ID

Industry Standard.

Request:

```text
Gateway
    ↓
User Service
    ↓
Order Service
    ↓
Payment Service
```

Same Correlation ID:

```text
REQ-12345
```

appears in every log.

Helps trace complete flow.

---

# 21. Request & Response Logging

Request:

```java
log.info("Incoming Request");
```

Response:

```java
log.info("Response Sent");
```

---

Example:

```java
@PostMapping("/save")
public ResponseEntity<?> save() {

    log.info("Save API Called");

    return ResponseEntity.ok("Success");
}
```

---

# 22. Logging in Controllers

```java
@RestController
@Slf4j
public class UserController {

    @PostMapping("/users")
    public User saveUser() {

        log.info("Create User API Called");

        return service.save();
    }
}
```

---

# 23. Logging in Services

```java
@Service
@Slf4j
public class UserService {

    public User save(User user){

        log.info("Saving User");

        User saved =
        repository.save(user);

        log.info(
            "User Saved With ID {}",
            saved.getId()
        );

        return saved;
    }
}
```

---

# 24. Logging in Repositories

Generally avoided.

Hibernate already logs SQL.

Enable SQL Logging:

```properties
spring.jpa.show-sql=true
```

Better:

```properties
logging.level.org.hibernate.SQL=DEBUG
```

---

# 25. Logging in Exception Handlers

```java
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<?> handle(
        Exception ex
    ){

        log.error(
            "Unexpected Error",
            ex
        );

        return ResponseEntity
                .internalServerError()
                .build();
    }
}
```

---

# 26. Logging in Microservices

Common fields:

```text
timestamp
service-name
request-id
user-id
thread
log-level
message
```

Example:

```text
2026-06-02
ORDER-SERVICE
REQ-12345
INFO
Order Created
```

---

# 27. Logging Security Considerations

Never log:

```text
Passwords
OTP
JWT Tokens
Credit Card Numbers
CVV
API Keys
Access Tokens
```

Bad:

```java
log.info("Password {}", password);
```

Good:

```java
log.info("User Login Successful");
```

---

# 28. Log Aggregation Tools

Large systems store logs centrally.

Popular Tools:

### ELK Stack

```text
Elasticsearch
Logstash
Kibana
```

---

### EFK Stack

```text
Elasticsearch
Fluentd
Kibana
```

---

### Splunk

Enterprise logging platform.

---

### Datadog

Cloud monitoring.

---

### Grafana Loki

Popular with Kubernetes.

---

# 29. Monitoring and Observability

Logs + Metrics + Traces

```text
Observability
     |
     +---- Logs
     +---- Metrics
     +---- Traces
```

Common Tools:

- Grafana
- Prometheus
- Kibana
- Datadog
- New Relic

---

# 30. Industry Best Practices

### Use INFO for business events

```java
log.info("Order Created");
```

### Use DEBUG for debugging

```java
log.debug("Payload {}", payload);
```

### Use ERROR with Exception

```java
log.error("Database Error", e);
```

### Use Placeholders

```java
log.info("User {}", userId);
```

### Never Log Sensitive Data

```java
password
otp
jwt
card details
```

### Add Correlation IDs

```java
REQ-12345
```

### Use Rolling Logs

Avoid huge files.

### Centralize Logs

Use ELK/Splunk.

### Use Structured Logging

Preferred:

```json
{
  "userId": 101,
  "action": "LOGIN",
  "status": "SUCCESS"
}
```

instead of plain text.

---

# 31. Common Interview Questions

### Why use logging?

To monitor, debug, audit, and troubleshoot applications.

---

### Why not System.out.println?

- No log levels
- No file support
- No filtering
- No production monitoring

---

### What is SLF4J?

Logging abstraction layer.

---

### What is Logback?

Default Spring Boot logging framework.

---

### Difference between INFO and DEBUG?

INFO:
Business events.

DEBUG:
Developer troubleshooting information.

---

### What is MDC?

Mechanism to attach contextual data to logs.

---

### What is Correlation ID?

Unique identifier used to trace a request across multiple services.

---

### Why use Async Logging?

Improves application performance by writing logs in background threads.

---

### What is Structured Logging?

Logging in JSON format for easy searching and analysis.

---

# Industry Logging Flow

Client
↓
API Gateway
↓
Microservice
↓
Business Logic
↓
Database

At each stage:

INFO  → Business Events
DEBUG → Troubleshooting
WARN  → Suspicious Activity
ERROR → Failures

Logs → ELK/Splunk/Grafana → Monitoring Dashboard → Alerts

This is the complete Spring Boot Logging roadmap from beginner to production-grade enterprise applications.
