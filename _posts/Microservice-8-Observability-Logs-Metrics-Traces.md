Architectural Style 
1. Monolithic
2. Microservice

Why ?


---
Learn this by an example :  

What happened?
Payment failed for order 123

How much / how often?
Payment API latency = 2.5 sec
Error rate = 5%
  
Where did the request go and where did it spend time?
Gateway
   ↓ 100ms
Order
   ↓ 200ms
Payment
   ↓ 2.2 sec ← bottleneck
Inventory
   ↓ 100ms
  
---



---

Logging , Monitoring , Distributed Tracing 
  
Three Pillars of Observability
1. Logs  
2. Metrics   
3. Traces

Logs    → What happened?
Metrics → How much/how often?
Traces  → Where did the request go?

Logging  vs Metrics vs Tracing 
Distributed Tracing vs Logging

---


Trace vs Span
Trace ID
Span ID
  
Trace = Whole Journey
Span  = Individual Step

  
Can Tracing work asynchronously?
Sync or Async ?


----

W3C Trace Context : World Wide Web Consortium Trace Context
  
W3C Headers
1. traceparent
2. tracestate 👈👈👈👈👈 Does it related to  traceflag
  
traceparent 4 Parts
3. TraceID
4. ParentID
5. Version
6. Trace Flag
  
Trace Flag 👈👈👈👈👈
00 → not sampled
01 → sampled
  
Trace flags are not HTTP status codes.


---
SpringBoot
Zipkin
Promethus
OpenTelementary
Grafana

👈👈👈👈👈
How do they fit together in an ecosystem ?


---
![[Spring-Security-Logs-Metrics-Traces.png]]

---


https://www.linkedin.com/feed/update/urn:li:activity:7469248420961017856/