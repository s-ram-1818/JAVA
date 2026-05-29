# Spring Framework Notes

## What is Spring Framework?

Spring is a lightweight Java framework used to build enterprise applications.

Main goals:
- Reduce boilerplate code
- Support Loose Coupling
- Manage object creation automatically
- Simplify Java EE development

---

# Why Spring?

Before Spring, developers used:

```java
Engine engine = new DieselEngine();
Car car = new Car(engine);
```

Developers manually created every object.

Problems:
- Tight coupling
- Difficult testing
- Difficult maintenance
- Code changes required when implementation changes

Spring solves this using:
- IoC (Inversion of Control)
- Dependency Injection (DI)

---

# Problem with Manual Object Creation

## Example

### Engine

```java
public class DieselEngine {
    public void start() {
        System.out.println("Diesel Engine Started");
    }
}
```

### Car

```java
public class Car {
    private DieselEngine engine =
            new DieselEngine();
}
```

Problems:

### 1. Tight Coupling

Car directly depends on DieselEngine.

If tomorrow:

```java
PetrolEngine
```

comes,

we must modify Car class.

### 2. Hard to Test

Cannot easily replace dependency with mock object.

### 3. Maintenance Issues

Changes spread throughout the project.

---

# Loose Coupling

Loose coupling means:

Classes should depend on abstractions (interfaces), not concrete implementations.

## Example

### Interface

```java
public interface Engine {
    void start();
}
```

### Implementation 1

```java
public class DieselEngine implements Engine {
    public void start() {
        System.out.println("Diesel Started");
    }
}
```

### Implementation 2

```java
public class PetrolEngine implements Engine {
    public void start() {
        System.out.println("Petrol Started");
    }
}
```

### Car

```java
public class Car {

    private Engine engine;

    public Car(Engine engine){
        this.engine = engine;
    }
}
```

Now Car doesn't care which engine is used.

Benefits:
- Easy maintenance
- Easy testing
- Flexible code
- Reusable components

---

# IoC (Inversion of Control)

## Definition

Inversion of Control means:

The control of object creation is transferred from the programmer to Spring Container.

### Without Spring

```java
Engine e = new DieselEngine();
```

Developer creates objects.

### With Spring

```java
@Autowired
Engine engine;
```

Spring creates and injects objects.

So control moves from developer → Spring.

Hence:

Inversion of Control (IoC)

---

# Dependency Injection (DI)

## Definition

Dependency Injection means:

Spring provides required objects (dependencies) automatically.

Instead of:

```java
Engine engine =
        new DieselEngine();
```

Spring injects dependency.

---

# Types of Dependency Injection

1. Constructor Injection
2. Setter Injection

---

# Constructor Injection

Recommended approach.

## Example

```java
@Component
public class Car {

    private Engine engine;

    public Car(Engine engine){
        this.engine = engine;
    }
}
```

Spring automatically injects Engine.

### Advantages

- Mandatory dependencies
- Immutable objects
- Better testing
- Recommended by Spring Team

---

# Setter Injection

Dependencies are injected using setter methods.

## Example

```java
@Component
public class Car {

    private Engine engine;

    @Autowired
    public void setEngine(Engine engine){
        this.engine = engine;
    }
}
```

### Advantages

- Optional dependencies
- Easy configuration

### Disadvantages

- Object can be incomplete
- Dependency can be changed later

---

# Spring Bean

## Definition

Any object managed by Spring Container is called a Bean.

Example:

```java
@Component
public class Car {
}
```

Car becomes a Bean.

Spring creates:

```java
Car car = new Car();
```

internally.

---

# Bean Lifecycle

1. Spring Container Starts
2. Bean Created
3. Dependencies Injected
4. Bean Ready for Use
5. Bean Destroyed

---

# Spring Container

Spring container manages:

- Bean creation
- Dependency injection
- Bean lifecycle
- Configuration

Two popular containers:

1. BeanFactory
2. ApplicationContext

---

# ApplicationContext

Advanced version of BeanFactory.

Provides:

- Bean management
- Event handling
- Internationalization
- Resource loading

Most commonly used container.

---

# ClassPathXmlApplicationContext

Used when configuration is written in XML.

Example:

```java
ApplicationContext context =
 new ClassPathXmlApplicationContext(
 "beans.xml");
```

Spring loads beans from:

```xml
beans.xml
```

---

# XML Bean Configuration

## beans.xml

```xml
<bean id="engine"
      class="com.demo.DieselEngine"/>

<bean id="car"
      class="com.demo.Car">
    <constructor-arg ref="engine"/>
</bean>
```

Access Bean:

```java
ApplicationContext context =
new ClassPathXmlApplicationContext(
"beans.xml");

Car car =
context.getBean("car",Car.class);
```

---

# Autowiring

## Definition

Spring automatically finds and injects dependencies.

### Example

```java
@Autowired
private Engine engine;
```

Spring searches for Engine Bean and injects it.

No need:

```java
new DieselEngine();
```

---

# Types of Autowiring

1. By Type
2. By Name
3. Constructor
4. Setter

Most common:

```java
@Autowired
```

---

# Ambiguity Problem

Suppose:

```java
public interface Engine
```

Implemented by:

```java
DieselEngine
```

and

```java
PetrolEngine
```

---

## Problem

```java
@Autowired
private Engine engine;
```

Spring becomes confused.

Because:

```java
DieselEngine
PetrolEngine
```

Both are Engine beans.

Error:

```
NoUniqueBeanDefinitionException
```

---

# @Primary

Used to define default bean.

## Example

```java
@Component
@Primary
public class DieselEngine
implements Engine {
}
```

Now Spring injects DieselEngine by default.

```java
@Autowired
Engine engine;
```

Result:

```java
DieselEngine
```

is injected.

---

# @Qualifier

Used when multiple beans exist and we want a specific bean.

## Example

```java
@Component("diesel")
class DieselEngine
implements Engine{
}
```

```java
@Component("petrol")
class PetrolEngine
implements Engine{
}
```

Injection:

```java
@Autowired
@Qualifier("petrol")
private Engine engine;
```

Result:

```java
PetrolEngine
```

gets injected.

---

# @Primary vs @Qualifier

| Feature | @Primary | @Qualifier |
|----------|----------|------------|
| Purpose | Default Bean | Specific Bean |
| Priority | Lower | Higher |
| Use Case | Common default implementation | Exact implementation required |

Example:

```java
@Primary
DieselEngine
```

and

```java
@Qualifier("petrol")
```

Spring chooses:

```java
PetrolEngine
```

because Qualifier has higher priority.

---

# Important Annotations

## @Component

Creates Bean.

```java
@Component
class Car{
}
```

---

## @Autowired

Inject Dependency.

```java
@Autowired
Engine engine;
```

---

## @Primary

Default Bean.

```java
@Primary
```

---

## @Qualifier

Choose specific Bean.

```java
@Qualifier("petrol")
```

---

# Spring Framework Architecture

User Class
↓
Spring Container
↓
Bean Creation
↓
Dependency Injection
↓
Application Ready

---

# Spring vs Spring Boot

| Feature | Spring Framework | Spring Boot |
|-----------|----------------|-------------|
| Setup | Complex | Easy |
| Configuration | More | Minimal |
| XML Usage | Often Required | Rare |
| Server Setup | Manual | Embedded |
| Starter Dependencies | No | Yes |
| Production Ready | Requires setup | Built-in |
| Development Speed | Slower | Faster |

---

# Advantages of Spring Framework

1. Loose Coupling
2. Dependency Injection
3. Easy Testing
4. Modular Architecture
5. Reusable Components
6. Large Ecosystem

---

# Disadvantages of Spring Framework

1. Lots of Configuration
2. XML Configuration (older projects)
3. Steeper Learning Curve
4. More Setup Time

---

# Advantages of Spring Boot

1. Rapid Development
2. Auto Configuration
3. Embedded Tomcat
4. Starter Dependencies
5. Production Ready Features
6. Less Boilerplate
7. Microservices Friendly

---

# Disadvantages of Spring Boot

1. Less Control over Auto Configuration
2. Higher Memory Consumption
3. Can hide internal configurations
4. Larger executable JAR

---

# Interview Questions

### What is IoC?

Control of object creation is transferred to Spring Container.

---

### What is DI?

Spring injects dependencies automatically.

---

### What is a Bean?

An object managed by Spring Container.

---

### Why Constructor Injection?

- Recommended
- Immutable
- Better testing

---

### Difference between @Primary and @Qualifier?

@Primary:
- Default bean

@Qualifier:
- Specific bean

Qualifier has higher priority.

---

### Why Spring Boot over Spring?

- Less configuration
- Faster development
- Embedded server
- Auto configuration

---

# Quick Revision

Spring
    |
    ├── IoC
    ├── DI
    ├── Bean
    ├── Container
    │      └── ApplicationContext
    |
    ├── Autowiring
    │      ├── @Autowired
    │      ├── @Primary
    │      └── @Qualifier
    |
    ├── Constructor Injection
    └── Setter Injection

Spring Boot
    |
    ├── Auto Configuration
    ├── Starter Dependencies
    ├── Embedded Tomcat
    └── Faster Development
