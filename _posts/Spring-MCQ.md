## **Spring MCQ Master Sheet (50 Questions)**

### **A. Spring Core & DI (1–15)**

**Q1.** Which of the following is true about Dependency Injection (DI) in Spring?
A) DI is manual object creation
B) Spring manages object creation and dependencies
C) DI works only for primitives
D) DI is unrelated to IoC

**Q2.** Which is **NOT a type of DI** in Spring?
A) Constructor Injection
B) Setter Injection
C) Field Injection
D) Method Overloading Injection

**Q3.** BeanFactory vs ApplicationContext – which **loads beans lazily** by default?
A) ApplicationContext
B) BeanFactory
C) WebApplicationContext
D) SpringBootApplication

**Q4.** Which annotation is used to **inject a bean by type**?
A) @Bean
B) @Autowired
C) @Component
D) @Qualifier

**Q5.** Default scope of a Spring bean?
A) Singleton
B) Prototype
C) Request
D) Session

**Q6.** Spring can inject which collection types?
A) List
B) Set
C) Map
D) All of the above

**Q7.** Which annotation injects values from properties files?
A) @Autowired
B) @Value
C) @PropertySource
D) @Bean

**Q8.** Purpose of @Qualifier?
A) Resolve ambiguity when multiple beans exist
B) Create primary bean
C) Inject primitive values
D) Mark lazy beans

**Q9.** Purpose of @Primary?
A) Marks default bean among multiple candidates
B) Makes bean singleton
C) Marks lazy bean
D) Injects collections

**Q10.** Which annotation marks a class as Spring-managed component?
A) @Service
B) @Repository
C) @Controller
D) All of the above

**Q11.** Which lifecycle annotations exist in Spring?
A) @PostConstruct
B) @PreDestroy
C) init-method in XML
D) All of the above

**Q12.** Which is true about Java config vs XML config?
A) Java config uses @Configuration; XML uses .xml files
B) Java config is type-safe
C) Both achieve same functionality
D) All of the above

**Q13.** What does @ComponentScan do?
A) Detects @Component, @Service, @Repository, @Controller
B) Defines bean lifecycle methods
C) Configures database connections
D) Enables AOP proxies

**Q14.** Which scope is required for stateful Spring MVC beans?
A) Singleton
B) Prototype
C) Request
D) Session

**Q15.** Which annotation defines a Spring Boot main class?
A) @SpringBootApplication
B) @EnableAutoConfiguration
C) @ComponentScan
D) @Configuration

---

### **B. Spring AOP & Advanced DI (16–25)**

**Q16.** What does AOP stand for?
A) Application-Oriented Programming
B) Aspect-Oriented Programming
C) Automatic Object Processing
D) Advanced OOP

**Q17.** Which annotation marks a class as an aspect?
A) @Aspect
B) @Before
C) @After
D) @Component

**Q18.** Advice that runs **before method execution**?
A) @Before
B) @After
C) @Around
D) @AfterReturning

**Q19.** Which advice runs after a method completes successfully?
A) @Before
B) @After
C) @AfterReturning
D) @AfterThrowing

**Q20.** What is a cross-cutting concern in Spring AOP?
A) Logging
B) Transactions
C) Security
D) All of the above

**Q21.** Multiple beans of same type exist. How to select one?
A) @Primary
B) @Qualifier
C) Both A and B
D) Cannot define multiple beans

**Q22.** Which bean scope creates **a new bean instance every request**?
A) Singleton
B) Prototype
C) Request
D) Session

**Q23.** Which bean scope creates **one instance per HTTP session**?
A) Singleton
B) Prototype
C) Request
D) Session

**Q24.** Which annotation defines **a repository layer** with exception translation?
A) @Repository
B) @Service
C) @Component
D) @Controller

**Q25.** Which annotation defines **service layer class**?
A) @Repository
B) @Service
C) @Component
D) @Controller

---

### **C. Spring Boot & Annotations (26–35)**

**Q26.** Which annotation enables **auto-configuration, component scan, and configuration**?
A) @EnableAutoConfiguration
B) @SpringBootApplication
C) @Configuration
D) @Component

**Q27.** Inject property value from application.properties?
A) @Autowired
B) @Value
C) @PropertySource
D) @Bean

**Q28.** Which annotation defines **a REST controller**?
A) @Controller
B) @RestController
C) @Service
D) @Repository

**Q29.** Difference between @Controller and @RestController?
A) @Controller returns views
B) @RestController returns JSON/XML
C) @RestController = @Controller + @ResponseBody
D) All of the above

**Q30.** Which annotation imports **external configuration classes**?
A) @Import
B) @Configuration
C) @ComponentScan
D) @SpringBootApplication

**Q31.** Which annotation is used to **define a bean method** inside a @Configuration class?
A) @Bean
B) @Autowired
C) @Primary
D) @Qualifier

**Q32.** Purpose of @EnableAspectJAutoProxy?
A) Enable AOP proxy creation
B) Define beans
C) Configure MVC
D) Scan packages

**Q33.** Which annotation marks a **controller method to handle HTTP GET**?
A) @GetMapping
B) @PostMapping
C) @RequestMapping(method=GET)
D) Both A and C

**Q34.** Which annotation handles **HTTP POST requests** in Spring MVC?
A) @GetMapping
B) @PostMapping
C) @RequestMapping(method=GET)
D) @RequestBody

**Q35.** Which annotation binds **method parameter to request parameter**?
A) @PathVariable
B) @RequestParam
C) @RequestBody
D) @Autowired

---

### **D. Spring MVC & Real-World Scenarios (36–50)**

**Q36.** Which annotation maps a **path variable** in Spring MVC?
A) @PathVariable
B) @RequestParam
C) @RequestBody
D) @ModelAttribute

**Q37.** Purpose of @ModelAttribute?
A) Bind form data to model object
B) Inject beans
C) Map URL
D) Enable AOP

**Q38.** Which annotation marks **exception handler methods**?
A) @ExceptionHandler
B) @ControllerAdvice
C) Both A and B
D) @ResponseBody

**Q39.** Which annotation globally handles exceptions across controllers?
A) @ExceptionHandler
B) @ControllerAdvice
C) @ResponseBody
D) @Service

**Q40.** Which annotation handles **transactions** in Spring?
A) @Transactional
B) @EnableTransactionManagement
C) Both A and B
D) @Service

**Q41.** Which annotation indicates **lazy bean initialization**?
A) @Lazy
B) @Primary
C) @Qualifier
D) @Autowired

**Q42.** Which annotation enables **JPA repositories**?
A) @EnableJpaRepositories
B) @Repository
C) @Entity
D) @Service

**Q43.** Which annotation marks **entity classes** for JPA?
A) @Entity
B) @Table
C) @Repository
D) @Component

**Q44.** Which annotation is used for **configuration properties binding**?
A) @ConfigurationProperties
B) @Value
C) @PropertySource
D) @Bean

**Q45.** Which annotation marks **controller advice for REST APIs**?
A) @RestControllerAdvice
B) @ControllerAdvice
C) @ExceptionHandler
D) @ResponseBody

**Q46.** Which annotation indicates **bean initialization after dependencies are set**?
A) @PostConstruct
B) @PreDestroy
C) init-method
D) @Autowired

**Q47.** Which annotation indicates **bean destruction callback**?
A) @PostConstruct
B) @PreDestroy
C) @Bean
D) @Lazy

**Q48.** Which annotation marks a **component for caching** in Spring?
A) @Cacheable
B) @EnableCaching
C) Both A and B
D) @Bean

**Q49.** Which annotation enables **Spring MVC support in configuration class**?
A) @EnableWebMvc
B) @SpringBootApplication
C) @Configuration
D) @Controller

**Q50.** Which annotation is used to define **custom bean initialization logic**?
A) @PostConstruct
B) @Bean(initMethod="methodName")
C) @PreDestroy
D) @Configuration
