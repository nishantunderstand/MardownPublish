### **Advanced Spring MCQs**

**Q1.** Which annotation is used to define a **Spring Boot main application class**?
A) @SpringBootApplication
B) @EnableAutoConfiguration
C) @ComponentScan
D) All of the above

A

**Q2.** What does the **@Primary** annotation do in Spring?
A) Marks a bean as the default candidate when multiple beans of the same type exist
B) Makes a bean singleton
C) Injects primitive values into beans
D) Defines a bean lifecycle method

A

**Q3.** How does **@Qualifier** help in dependency injection?
A) Allows injecting multiple beans into one field
B) Resolves ambiguity when multiple beans of the same type exist
C) Marks a bean as lazy
D) Replaces @Autowired

B

**Q4.** Which is a **valid lifecycle method in Spring beans**?
A) @PostConstruct
B) @PreDestroy
C) init-method in XML config
D) All of the above

D

**Q5.** What is the difference between **Java-based config and XML-based config** in Spring?
A) Java config uses @Configuration classes; XML uses .xml files
B) Java config is type-safe and refactoring-friendly; XML is not
C) Both achieve the same functionality
D) All of the above

D

**Q6.** Which annotation marks a class as a **Spring-managed component**?
A) @Service
B) @Repository
C) @Controller
D) All of the above

D

**Q7.** What does **@ComponentScan** do in Spring Boot?
A) Scans packages to detect @Component, @Service, @Repository, @Controller classes
B) Defines bean lifecycle methods
C) Enables AOP proxy creation
D) Configures database connections

A

**Q8.** Which of the following is **true about Spring AOP**?
A) AOP stands for Aspect-Oriented Programming
B) AOP allows cross-cutting concerns like logging and transactions
C) AOP can be applied using @Aspect and @Before/@After annotations
D) All of the above

D

**Q9.** Which **Spring Boot annotation** automatically enables **component scanning, auto-configuration, and configuration**?
A) @EnableAutoConfiguration
B) @SpringBootApplication
C) @Configuration
D) @Component

B

**Q10.** Which **scope is required for stateful beans in Spring MVC**?
A) Singleton
B) Prototype
C) Request
D) Session

D

**Q11.** What does the **@PostConstruct** annotation do?
A) Marks a method to run after bean initialization
B) Marks a method to run before bean destruction
C) Marks a bean as primary
D) Replaces @Autowired

A

**Q12.** Which annotation in Spring Boot is used to **inject a property value from application.properties or application.yml**?
A) @Autowired
B) @Value
C) @PropertySource
D) @Bean

B

**Q13.** Which is the **correct way to define multiple beans of the same type and select one**?
A) Use @Primary on the default bean
B) Use @Qualifier with the bean name
C) Both A and B
D) Cannot define multiple beans of same type

C

**Q14.** Which annotation is used to **create an aspect in Spring AOP**?
A) @Aspect
B) @Before
C) @After
D) @Component

A

**Q15.** Which advice type **runs before a method execution** in Spring AOP?
A) @Before
B) @After
C) @Around
D) @AfterReturning

A

**Q16.** What is **the difference between @Controller and @RestController**?
A) @Controller returns view templates; @RestController returns JSON/XML response
B) @RestController is a combination of @Controller + @ResponseBody
C) Both are detected by component scanning
D) All of the above

D

**Q17.** Which annotation marks a **repository layer class** for persistence exceptions translation?
A) @Repository
B) @Service
C) @Component
D) @Controller

A

**Q18.** Which is **true about @Configuration classes** in Spring?
A) They are used to define beans using @Bean methods
B) They support Java-based type-safe configuration
C) Can replace XML configuration entirely
D) All of the above

D