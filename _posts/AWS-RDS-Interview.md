# Amazon RDS — Interview Questions
### Core RDS Questions
1. What is Amazon RDS?
2. What does RDS stand for?
3. Is RDS a database or a managed database service?
4. Which database engines does Amazon RDS support?  🤔🤔🤔
5. What is the difference between RDS and a traditional database installed on an EC2 instance?
6. What is the difference between RDS and EC2?
7. What is the difference between RDS and DynamoDB?
8. Does RDS support NoSQL databases?  🤔🤔🤔
9. What is an RDS DB instance?
10. What is an RDS endpoint?
11. What is a DB subnet group?
12. What is a parameter group in RDS?
13. What is an option group in RDS?
### High Availability & Disaster Recovery
14. What is Multi-AZ in RDS?
15. How does RDS Multi-AZ work?
16. What is the difference between Multi-AZ and Read Replica?
17. Does Multi-AZ improve read performance?
18. What happens when the primary RDS instance fails?
19. How does RDS perform automatic failover?
20. What is an RDS Read Replica?
21. Can Read Replicas be used for write operations?
22. Can a Read Replica be promoted to a standalone database?
23. Can RDS Read Replicas exist in another AWS Region?
24. What is the difference between Multi-AZ, Read Replica, and backup?
25. How would you design RDS for disaster recovery?
### Backup & Recovery
26. What is automated backup in RDS?
27. What is an RDS snapshot?
28. Difference between automated backups and manual snapshots?
29. How do you restore an RDS database?
30. What is Point-in-Time Recovery in RDS?
31. How long can RDS automated backups be retained?
32. What happens to automated backups when an RDS instance is deleted?
33. Can you copy an RDS snapshot to another Region?
34. Can you encrypt an RDS snapshot?
35. How would you recover a production database after accidental data deletion?
### Scaling & Performance
36. How do you scale an RDS database?
37. Difference between vertical scaling and horizontal scaling in RDS?
38. How do Read Replicas help with scaling?
39. Can RDS automatically scale storage?
40. What is Provisioned IOPS?
41. What is the difference between General Purpose SSD and Provisioned IOPS storage?
42. How would you troubleshoot a slow RDS database?
43. What CloudWatch metrics would you monitor for RDS?
44. What happens when RDS runs out of storage?
45. How would you handle a sudden increase in database traffic?
### Security
46. How do you secure an RDS database?
47. What is encryption at rest in RDS?
48. How do you enable encryption for an RDS database?
49. What is encryption in transit?
50. How do you enforce SSL/TLS connections to RDS?
51. How does IAM integrate with RDS?
52. What is the role of Security Groups in RDS?
53. Should an RDS database be publicly accessible?
54. How would you allow only your Spring Boot application to access RDS?
55. How do you store RDS database credentials securely?
56. What is AWS Secrets Manager and how can it be used with RDS?
### Networking
57. What is an RDS VPC?
58. Why is RDS commonly deployed inside a private subnet?
59. What is an RDS DB subnet group?
60. Can an EC2 instance in a different subnet access RDS?
61. How does a Security Group control access to RDS?
62. What is the difference between public and private RDS access?
63. How would your Spring Boot application connect to a private RDS instance?
### RDS vs Other AWS Services
64. RDS vs EC2 — when would you choose each?
65. RDS vs DynamoDB?
66. RDS vs Aurora?
67. RDS vs Redshift?
68. RDS vs ElastiCache?
69. RDS vs running MySQL/PostgreSQL manually on EC2?
### Scenario-Based Questions ⭐
70. Your production RDS instance goes down. What happens?
71. Your application has heavy read traffic but relatively few writes. How would you scale RDS?
72. Your RDS database is running out of storage. What would you do?
73. Your Spring Boot application cannot connect to RDS. How would you troubleshoot it?
74. Your RDS database is publicly accessible. What security changes would you make?
75. You accidentally deleted important data from RDS. How would you recover it?
76. You need high availability for a production PostgreSQL database. How would you configure RDS?
77. You need to reduce the load on your primary database caused by reporting queries. What would you do?
78. You need to replicate your database to another AWS Region for disaster recovery. How would you approach it?
79. Your application suddenly gets 10× more traffic. How would you handle the database load?
80. You need to migrate an on-premise MySQL/PostgreSQL database to AWS RDS. How would you approach the migration?
### ⭐ Must-Know for Interviews
If you have limited time, prioritize these:
1. **What is RDS?**
2. **RDS vs EC2**
3. **RDS vs DynamoDB**
4. **Multi-AZ**
5. **Read Replica**
6. **Multi-AZ vs Read Replica**
7. **Automated Backup vs Snapshot**
8. **Point-in-Time Recovery**
9. **RDS Security**
10. **RDS Security Groups**
11. **RDS Encryption**
12. **RDS Scaling**
13. **RDS Endpoint**
14. **DB Subnet Group**
15. **RDS vs Aurora**