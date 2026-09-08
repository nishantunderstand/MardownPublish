# Spring Exception Handling & Transaction Rollback — Complete Guide

Many developers confuse **Spring Exception Handling** with **Transaction Rollback** because both involve exceptions. However, they belong to **different Spring modules** and solve different problems.

---

# Big Picture

```text
Spring
│
├── Spring MVC (Web Layer)
│   ├── Exception Handling
│   │   ├── @ExceptionHandler
│   │   ├── @ControllerAdvice
│   │   ├── @RestControllerAdvice
│   │   ├── @ResponseStatus
│   │   └── ResponseStatusException
│   │
│   └── Validation
│       ├── @Valid
│       ├── BindingResult
│       └── MethodArgumentNotValidException
│
├── Spring Transaction
│   ├── @Transactional
│   ├── Rollback
│   ├── rollbackFor
│   ├── noRollbackFor
│   └── Transaction Propagation
│
├── Spring AOP
│   ├── @Aspect
│   ├── @Before
│   ├── @After
│   ├── @Around
│   ├── @AfterReturning 👈👈👈👈]
│   └── @AfterThrowing
│
└── Spring Security
    ├── AuthenticationException
    ├── AccessDeniedException
    └── ExceptionTranslationFilter
```

These are **different topics** even though they all use exceptions.

---

# 1. Spring MVC Exception Handling

Suppose a request comes to your application.

```text
Client
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
```

If everything works:

```text
200 OK
```

If an exception occurs:

```text
ArithmeticException

NullPointerException

UserNotFoundException
```

Without Spring Exception Handling:

```text
HTTP 500
Stack Trace
```

Not user-friendly.

Spring provides mechanisms to convert exceptions into meaningful HTTP responses.

---

# @ExceptionHandler

Handles a particular exception.

Example

```java
@RestController
public class UserController {

    @GetMapping("/divide")
    public int divide() {
        return 10 / 0;
    }

    @ExceptionHandler(ArithmeticException.class)
    public ResponseEntity<String> handleArithmeticException(
            ArithmeticException ex) {

        return ResponseEntity
                .badRequest()
                .body("Division by Zero");
    }
}
```

Request

```text
GET /divide
```

Response

```text
400 Bad Request

Division by Zero
```

### Scope

Only this controller.

---

# @ControllerAdvice

Global exception handler.

Instead of writing

```java
@ExceptionHandler
```

inside every controller,

create one class.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handle(Exception ex) {

        return ResponseEntity
                .internalServerError()
                .body(ex.getMessage());
    }
}
```

Now every controller automatically uses it.

---

# @RestControllerAdvice

Equivalent to

```java
@ControllerAdvice
@ResponseBody
```

Always returns JSON.

This is preferred for REST APIs.

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handle(
            UserNotFoundException ex) {

        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(ex.getMessage());
    }
}
```

---

# @ResponseStatus

Instead of writing

```java
throw new UserNotFoundException();
```

Define

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException
        extends RuntimeException {
}
```

Whenever thrown

↓

HTTP 404

---

# ResponseStatusException

Instead of creating custom exception.

```java
throw new ResponseStatusException(
        HttpStatus.NOT_FOUND,
        "User Not Found");
```

Useful for small applications.

---

# Is @Advice Specific to Exception?

**No.**

This is one of the most common interview questions.

`@ControllerAdvice` is **not an exception annotation**.

It is a **cross-cutting component for Spring MVC controllers**.

It can contain

* `@ExceptionHandler`
* `@InitBinder`
* `@ModelAttribute`

Example

```java
@ControllerAdvice
public class GlobalConfig {

    @ModelAttribute
    public void addCommonData(Model model) {

        model.addAttribute("company","ABC");
    }

    @InitBinder
    public void init(WebDataBinder binder){

    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handle(Exception ex){

        return ResponseEntity.internalServerError()
                .body(ex.getMessage());
    }
}
```

So `@ControllerAdvice` is **not specific to exceptions**.

---

# @ExceptionHandler

Specific to exceptions.

```java
@ExceptionHandler(IOException.class)
```

Only handles exceptions.

---

# Validation Exceptions

```java
@PostMapping
public User save(@Valid @RequestBody User user)
```

Invalid input

↓

Spring throws

```text
MethodArgumentNotValidException
```

Usually handled inside

```java
@RestControllerAdvice
```

---

# Spring AOP Advice

This is another place where "Advice" appears.

Many developers confuse it with `@ControllerAdvice`.

They are unrelated.

---

## AOP Advice Types

```text
@Before

@After

@AfterReturning

@AfterThrowing

@Around
```

Example

```java
@Before("execution(* com.example.service.*.*(..))")
public void log(){

}
```

Here

Advice means

> Code executed before or after another method.

Not exception handling.

---

# Transaction Management

Entirely different module.

Example

```java
@Transactional
public void transfer(){

    withdraw();

    deposit();
}
```

If

```text
withdraw()

Success
```

Then

```text
deposit()

Fails
```

Should database keep withdrawal?

No.

Rollback.

---

# Default Rollback Rule

Spring rolls back

Only

```text
RuntimeException

Error
```

Example

```java
@Transactional
public void save(){

    repository.save(user);

    throw new RuntimeException();
}
```

Database

↓

Rollback

---

Checked Exception

```java
@Transactional
public void save()
throws IOException{

    repository.save(user);

    throw new IOException();
}
```

Default

↓

No Rollback

Because checked exceptions do **not** trigger rollback by default.

---

# rollbackFor

Force rollback.

```java
@Transactional(
    rollbackFor = IOException.class
)
```

Now

```text
IOException
```

also rolls back.

---

# noRollbackFor

Prevent rollback.

```java
@Transactional(
    noRollbackFor = RuntimeException.class
)
```

Even if

```text
RuntimeException
```

occurs

↓

Commit.

---

# rollbackFor vs noRollbackFor

```text
rollbackFor

↓

Force rollback
```

```text
noRollbackFor

↓

Prevent rollback
```

These belong to

```text
Transaction Management
```

NOT

```text
Spring MVC Exception Handling
```

---

# Relationship Between Exceptions and Rollback

People think rollback is part of exception handling.

Actually

```text
Exception

↓

Transaction Manager

↓

Rollback Decision
```

The exception **triggers** the transaction manager to decide whether to commit or roll back based on the rollback rules.

Exception handling and transaction management are different responsibilities.

---

# Typical Flow

```text
HTTP Request
      │
      ▼
Controller
      │
      ▼
Service (@Transactional)
      │
      ▼
Repository
      │
      ▼
Database
```

Suppose

```text
Repository

↓

SQLException
```

Spring converts it

↓

```text
DataAccessException
```

Transaction Manager

↓

Rollback

Controller

↓

Exception

↓

@RestControllerAdvice

↓

JSON Response

```text
{
   "message":"User Not Found"
}
```

Notice how the **same exception** is involved in two different concerns:

1. **Transaction Manager** decides whether to roll back the database.
2. **Spring MVC** decides what HTTP response to send.

---

# Interview Questions

1. What is the difference between `@ExceptionHandler` and `@ControllerAdvice`?
2. What is the difference between `@ControllerAdvice` and `@RestControllerAdvice`?
3. Is `@ControllerAdvice` only for exception handling?
4. When would you use `ResponseStatusException` instead of a custom exception?
5. How does Spring decide whether to roll back a transaction?
6. Why does Spring roll back only for unchecked exceptions by default?
7. What is the difference between `rollbackFor` and `noRollbackFor`?
8. What happens if a checked exception is thrown inside a `@Transactional` method?
9. How are validation exceptions handled globally?
10. What is the difference between Spring MVC Advice and Spring AOP Advice?

---

# Summary

| Topic                                | Module             | Purpose                                                                      |
| ------------------------------------ | ------------------ | ---------------------------------------------------------------------------- |
| `@ExceptionHandler`                  | Spring MVC         | Handle specific exceptions                                                   |
| `@ControllerAdvice`                  | Spring MVC         | Global controller configuration (exceptions, model attributes, data binding) |
| `@RestControllerAdvice`              | Spring MVC         | Global REST exception handling (JSON responses)                              |
| `@ResponseStatus`                    | Spring MVC         | Associate an HTTP status with an exception                                   |
| `ResponseStatusException`            | Spring MVC         | Throw an exception with an HTTP status without creating a custom exception   |
| `@Valid`                             | Spring Validation  | Validate request data                                                        |
| `MethodArgumentNotValidException`    | Spring Validation  | Raised when validation fails                                                 |
| `@Transactional`                     | Spring Transaction | Define transactional boundaries                                              |
| `rollbackFor`                        | Spring Transaction | Force rollback for specified exceptions                                      |
| `noRollbackFor`                      | Spring Transaction | Prevent rollback for specified exceptions                                    |
| `@Before`, `@After`, `@Around`, etc. | Spring AOP         | Execute cross-cutting logic around method execution                          |
