# Kafka Cluster Configuration

1. broker.id  : ZooKeeper-based Kafka    
2. node.id : KRaft-based Kafka

Difference 🤔🤔🤔 

---

# Topic 

How to Decide a Topic ?

Based on Business service + Logical event, We can decide 

Order Service
 ├── OrderCreated
 ├── OrderCancelled
 └── OrderUpdated

Payment Service
 ├── PaymentSuccess
 └── PaymentFailed

Inventory Service
 ├── InventoryReserved
 └── InventoryFailed
 
Based on We have 3 Business Event, 3 Topic 

---






What is the difference between Kafka key and partition?
Key -> Where Message Goes
Partition : Where Message Stored





Topic  : logical category/group of messages.



> Kafka Message aka Record


Partition 
A **partition is an ordered log of records** inside a topic.
Physical/logical subdivision of that topic
Ordered append-only log of records.



OffSet
Position of the record inside its partition
Offset belongs to a Partition
OffSet : An offset identifies a record's position within a partition.
Does it belongs to Topic 🤔🤔🤔 


Topic vs Partition vs Offset
Topic + Partitions + Offset

Can a Broker have multiple Topics?	🤔🤔🤔 
Can a Topic have multiple Partitions?	
Can a Partition have multiple Offsets? 🤔🤔🤔 


==One Partition can be assigned to only one Consumer within the same Consumer Group.==
Can two consumers read from the same Topic? (Same or Different Consumer Group)
Can Brokers Be in Different Locations?
Can a Topic Have Multiple Partitions?






Message Ordering
Does Kafka guarantee message ordering?
1. Topic 
2. Multiple Topic 
3. Partiton 
4. Multiple Partition
5. Offset

Local Ordering 
Global Ordering 


Kafka Ordering + Key + Partition 

Ordering 
Kafka Ordering is Topic wide 🤔🤔🤔  
Ordering within a partition.  🤔🤔🤔 








# Partition



Partitions — num.partitions

- What
- Why
- Where
- Who
- How
- When
- Types
- Pro
- Cons

Partitions determine:
- Parallelism 🤔🤔🤔  BUT HOW 🤔🤔🤔 
- Throughput
- Maximum number of consumers processing simultaneously
- Ordering scope


How do we decide partitions?
Incoming traffic = 10,000 messages/sec
One consumer instance can process = 2,000 messages/sec
Partitions >= 10000 / 2000
Partitions >= 5
But we also need growth.
Current requirement = 5 partitions
Expected growth = 2x
You might choose: 10–12 partitions



Important rule
Maximum active consumers ≈ Number of partitions

Partition

PartitionSkew : UnEven Distribution
P0 → 90,000 msg/sec : This is becoming a bottleneck
P1 →  2,000 msg/sec
P2 →  2,000 msg/sec
P3 →  2,000 msg/sec
P4 →  4,000 msg/sec

Hot Partition : One partition receives disproportionately high traffic.
P0 : More Traffic Here
P1 : Less Traffic
P2 : Less Traffic

Sticky Partitioning🤔🤔🤔 



Don't you think PartitionSkew and Hot Partition are same thing 🤔🤔🤔 


---






---




---



---

Leader Election
Preferred Replica
Replication Lag
Broker 1 Dies, New Leader Broker 2

What if Broker 1 is back ?
What if Replica falls too far behind ?
Preferred Replica vs ISR 🤔🤔🤔 
Leader Election vs Consumer Rebalance 🤔🤔🤔 



---

Kafka Message Structure 
Kafka Message aka Record

![[Kafka-Message-Structure.png]]







