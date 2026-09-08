Architectural Style 
1. Monolithic : Rollback 
2. Microservice : 
  
SAGA Design Patten
SAGA : Sequential Approach to General Availability

A SAGA breaks one large transaction into multiple smaller local transactions.


Types 👈👈👈👈👈
1. Choreography Saga 
	Events
2. Orchestration Saga 
	BPMN  : Business Process Model and Notation 
		Graphical Way
	Camunda
	Central Coordinator

---

Compensating Transaction

---


ACID : Use ACID within a single microservice where all operations are on the same database.
BASE : Use BASE between multiple microservices.

👈👈👈👈👈
A → Atomicity 
C → Consistency 
I → Isolation 
D → Durability

B A → Basically Available
S → Soft State
E → Eventual Consistency


ACID Vs BASE 


---




---


How to Handle Distributed Transactions?
1. SAGA Pattern
   +-- Choreography
   +-- Orchestration
2. Eventual Consistency
3. Compensating Transactions
4. Transactional Outbox Pattern
5. Idempotency
6. Retry Mechanism
7. Avoid Distributed Locking
8. Usually Avoid 2 Phase Commit

----


2 Phase Commit 
2PC
1. Prepare
2. Commit


3 Phase Commit

3PC
1. CanCommit
2. PreCommit
3. DoCommit

Are they really used or not ?

----

Transactional Outbox Pattern 🤔🤔🤔 