Spring Exception

Spring MVC
@ExceptionHandler
@ControllerAdvice
@RestControllerAdvice


Is Advice Specific to Exception ?

I need to write Code to understand it better ?

What else topic comes under this category


---
rollback 
rollback NoFar : Is this part of Exception or Transaction



---

Spring MVC Exception Handling Hierarchy

Spring MVC Exception Handling
│
├── Local Exception Handling
│      └── @ExceptionHandler
  Can one handler manage multiple exceptions?
│
├── Global Exception Handling
│      ├── @ControllerAdvice
│      └── @RestControllerAdvice
│
├── Exception → HTTP Status
│      ├── @ResponseStatus
│      └── ResponseStatusException
│
└── Validation Exceptions
       ├── @Valid
       ├── BindingResult
       └── MethodArgumentNotValidException







----

@ResponseStatus	Simple exception
@ExceptionHandler	Custom response body banana ho
@RestControllerAdvice	Global handling
Who will get more priority ?

