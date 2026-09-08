# Replication Factor 

Definition  : 

RF ≥ F+1 to tolerate F broker failures,

This is independent 
replication.factor=3

Example:
Topic: orders
Replication Factor = 3
Partition 0:
Broker 1 → Leader
Broker 2 → Replica | Follower | Preferred Replica 🤔🤔🤔  
Broker 3 → Replica

- I think Leader Replica Preferred Replica is correct way 🤔🤔🤔 
- Don't we have some kind of voting ? 🤔🤔🤔 
- Cannot Broker 3 become a Preferred Replica ? 🤔🤔🤔 


How data will be synced across leaders and Followers  

Explain me the meaning of 3 i.e 1 Leader  + 2 Follower 
If Broker 1 crashes:
Broker 2 → New Leader

Common choice :

| Environment | Replication Factor |
| ----------- | ------------------ |
| Development | 1                  |
| Staging     | 2 or 3             |
| Production  | 3                  |

For a production system, RF = 3 is a very common starting point.


Is there any mathematical formula for determining it ? 🤔🤔🤔 
We have very large system ?
Will they have Only RF :3 
Like big MNC ? 🤔🤔🤔 

---

# Min.insync.replicas


min.insync.replicas 
minISR = RF-1
RF ≥ F+1 to tolerate F broker failures,


What does this F represent ? 
How many brokers can crash, and I still want my data/service to survive?

Broker 1 → Leader
Broker 2 → Replica
Broker 3 → Replica

Broker 1 💥
Broker 2 💥
Broker 3 ✅

You lost 2 brokers, but one copy still exists.
Therefore:
F = 2
RF = 3

ISR = RF-1 => 1
minISR = RF-1 => 2
ack-all : ISR>=minISR 

This is extremely important.

Suppose:
Replication Factor = 3
Broker 1 → Leader
Broker 2 → Follower
Broker 3 → Follower

Set:

min.insync.replicas=2
It means Kafka requires at least 2 in-sync replicas for a successful durable write when the producer uses:
acks=all

Recommended combination
replication.factor=3
min.insync.replicas=2
acks=all
This gives good durability.

```
Scenario
Initially:
ISR = [Broker1, Broker2, Broker3]

One broker dies:
ISR = [Broker1, Broker2]
Still okay because:
ISR >= min.insync.replicas
2 >= 2




Another broker becomes unavailable:
ISR = [Broker1]
Now:
1 < 2
Kafka rejects writes rather than accepting data with insufficient replication.

```

That is a tradeoff:
Availability ↓
Durability ↑

What if we have only 1 ISR ?   🤔🤔🤔 
Think about a different edge case ?🤔🤔🤔 
How will they behave around it ?🤔🤔🤔 

|     |                    |            |        |      |        |        | ISR >= minISR |
| :-: | :----------------: | :--------: | :----: | :--: | :----: | :----: | :-----------: |
| RF  | Failed Replicas(F) | ISR = RF-F | minISR | Read | acks=0 | acks=1 |   acks=all    |
|  3  |         0          |     3      |   2    |  ✅   |   ✅*   |   ✅    |       ✅       |
|  3  |         1          |     2      |   2    |  ✅   |   ✅*   |   ✅    |       ✅       |
|  3  |         2          |     1      |   2    |  ✅   |   ✅*   |   ✅    |       ❌       |
|  3  |         3          |     0      |   2    |  ❌   |   ❌    |   ❌    |       ❌       |
| RF  | Failed Replicas(F) | ISR = RF-F | minISR | Read | acks=0 | acks=1 |   acks=all    |
|  2  |         0          |     2      |   1    |  ✅   |   ✅*   |   ✅    |       ✅       |
|  2  |         1          |     1      |   1    |  ✅   |   ✅*   |   ✅    |       ✅       |
|  2  |         2          |     0      |   1    |  ❌   |   ❌    |   ❌    |       ❌       |
| RF  | Failed Replicas(F) | ISR = RF-F | minISR | Read | acks=0 | acks=1 |   acks=all    |
|  1  |         0          |     1      |   0    |  ✅   |   ✅*   |   ✅    |       ✅       |
|  1  |         1          |     0      |   0    |  ❌   |   ❌    |   ❌    |       ❌       |
| RF  | Failed Replicas(F) | ISR = RF-F | minISR | Read | acks=0 | acks=1 |   acks=all    |
|  0  |         —          |     0      |   —    |  ❌   |   ❌    |   ❌    |       ❌       |

  
RF = 3
minISR = RF-1
RF >= F+1
ISR = RF-F
==acks=all ACCEPT if ISR >= minISR==
acks=all REJECT if ISR < minISR


---
Producer  Acknowledment 
1. acks 0 : Don't wait for acknowledgment
2. acks 1 : Leader acknowledges
3. acks all : wait for all replicas currently in ISR.

How data will get synced b/w leader and follower ?
Leader + Followers / Replication
What about Replication Lag 🤔🤔🤔 
How to handle it ? 🤔🤔🤔 

| acks | Producer waits for            |
| ---- | ----------------------------- |
| 0    | Nobody                        |
| 1    | Leader                        |
| all  | All replicas currently in ISR |

---