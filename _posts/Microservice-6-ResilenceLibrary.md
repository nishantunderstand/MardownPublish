
Architectural Style 
1. Monolithic
2. Microservice


https://app.xmind.com/gZ0ZdIEQ?sheet-id=2e13d090-7f96-48c9-a2ac-59dd554a0644

---

Due to Evolution of Technology 
Hystrix  → Resilience4j | Successor of Hystrix :  Resilience4j
Ribbon   → Spring Cloud LoadBalancer
Zuul     → Spring Cloud Gateway

---

Hystrix 
Fault Tolerance Library
Cascading Failure
Fault-Tolerance / Resilience Mechanisms

Why Deprecated 
Due to rise of Technology.
https://resilience4j.readme.io/docs/getting-started


---

Supports : 
1. Circuit Breaker
2. Retry
3. Timeout / Time Limiter
4. Bulkhead / Isolation
5. Rate Limiter
6. Fallback
  

  
Bucket4j (Specially Design For Rate Limiter )

---

Retry = "Try again."
Circuit Breaker = "Stop trying."


Circuit Breaker Vs Retry vs Bulkhead  
Retry vs Circuit Breaker
Can Retry Make the System Worse?
Is Circuit Breaker Same as Timeout?

CircuitBreaker with Exponential TimeOfff
Rate Limiter Vs Bloom Filter ?



Why Use Bulkhead?
Bulkhead vs Circuit Breaker


Rate Limiter vs Load Balancer
Where to Apply Rate Limiter?

---

Which Pattern for Temporary Network Glitch?
Which Pattern for Slow External API?
Which Pattern for Too Many Requests?
Which Pattern for Thread Exhaustion?
