

🤔 If Filters and Interceptors can both intercept requests... why does Spring Security build its entire authentication architecture on Filters instead of Interceptors?  
  
The answer lies in where they execute in the request lifecycle.  
  
✅ Filters run before the request enters the Spring Context, making them ideal for authentication, CORS, security headers, and other cross-cutting concerns.  
  
✅ Interceptors execute inside Spring MVC, where they can access Spring beans and are better suited for business logic, monitoring, and request processing.  
  
Understanding this distinction helps you choose the right tool for the right responsibility—leading to cleaner, more secure, and more maintainable application.


![[Spring-Security-Filter-Interceptors.png]]