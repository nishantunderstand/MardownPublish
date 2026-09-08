

20 NEW Database Failure Scenarios — Spring Boot Interviews  
  
These are the questions interviewers ask when they want to know whether you can handle real production database problems.  
  
1. Database suddenly becomes unreachable. How should your Spring Boot service behave?  
2. HikariCP connection timeouts appear, but the database itself is healthy. What would you investigate?  
3. Database connections keep increasing until the pool is exhausted. How would you find the connection leak?  
4. A query that normally takes 50 ms suddenly takes 10 seconds. How would you identify the root cause?  
5. Database CPU reaches 100% after a new application release. How would you determine whether the application caused it?  
6. Deadlocks suddenly increase during peak traffic. How would you identify and fix the conflicting transactions?  
7. Two requests update the same record simultaneously. How would you prevent lost updates?  
8. A transaction holds a database lock for several seconds. What application code could be responsible?  
9. The application starts throwing “Too many connections.” What would you check before increasing the database connection limit?  
10. Read queries are slow, but write queries are normal. What database-level issues would you investigate?  
11. Write operations suddenly become slow after adding several indexes. Why can indexes cause this?  
12. A JPA batch process crashes with OutOfMemoryError while processing millions of records. How would you redesign it?  
13. Database replication lag increases, causing users to see old data after an update. How would you handle read-after-write consistency?  
14. Primary database fails while replicas are healthy. How should the application recover without losing requests?  
15. A schema migration succeeds on some pods but fails on others during deployment. What could cause this?  
16. A production migration locks a large table and suddenly APIs start timing out. How would you prevent this?  
17. Database storage reaches 100%. What happens to the application, and what should your recovery plan look like?  
18. Connection pool is configured with 100 connections, but the database supports only 50. What problems can this create?  
19. A transaction succeeds in the database, but the API returns an error because the response failed afterward. What happens when the client retries?  
20. Database looks healthy, but application performance is poor. How would you determine whether the bottleneck is connection acquisition, query execution, locking, network latency, or application code?  
  
A strong database answer should cover:  
  
Detection → Root Cause → Immediate Mitigation → Permanent Fix → Prevention  
  
That’s the difference between knowing SQL and being able to run production systems reliably.