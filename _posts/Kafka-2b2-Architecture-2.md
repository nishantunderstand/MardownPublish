# Producer

Producer acks + Idempotence + Retries
Producer delivery.timeout.ms
Producer Buffer Memory

request.timeout.ms vs delivery.timeout.ms 
request.timeout.ms : One Request
delivery.timeout.ms  : Whole Delivery Attempt Including retries


---

# Consumer and ConsumerGroup

Topic = 3 partitions
Consumer Group A
Consumer 1
Consumer 2
Consumer 3
Consumer 4

If we have 3 Partition, Then we need 3 Consumer 
Consumers ≤ Partitions

Number of useful consumers ≤ Number of partitions
Consumer 4 will be idle.
P0 → Consumer 1
P1 → Consumer 2
P2 → Consumer 3
Consumer 4 → Idle

So partition count directly affects consumer scalability.

How to decide on a Consumer Group ?
Who needs to independently read to this event.

For Example 
This event Need to be read by Payment, Inventory , Rating 
Then I need 3 groups.
Consumer Group 
5 Consumer  12 partition 🤔🤔🤔 




How to decide the partition ??
C1
C2
C3
C4
C5 : 
12 / 5
Quotient = 2
Remainder = 2

Then Try to Rebalance itself 
How much parallelism does each group need?
Different Consumer Groups can have different numbers of consumers
Can these Consumer groups have Different Number Partitions ?

Example:

| Consumer Group | Incoming Rate | Capacity per Consumer | Needed Consumers |
| -------------- | ------------- | --------------------- | ---------------- |
| Payment        | 10,000/sec    | 2,000/sec             | 5                |
| Inventory      | 10,000/sec    | 5,000/sec             | 2                |
| Shipping       | 10,000/sec    | 1,000/sec             | 10               |
| Analytics      | 10,000/sec    | 10,000/sec            | 1                |


---


Kafka Consumer Lag
Case 1 — Consumer is slow
Case 2 — Consumer processing is expensive
Case 3 — Consumer is down

How Do We Reduce Consumer Lag?
Option 1 — Add consumers
Option 2 — Increase processing speed
Option 3 — Increase partition count 🤔🤔🤔 

Consumer Lag vs Offset Commit 🤔🤔🤔 

Consumer Polling Model  🤔🤔🤔 

Consumer Group Coordinator

Consumer Rebalancing

When does Rebalancing happen ?
1. Consumer joins
2. Consumer leaves/crashes
3. Partition count changes
4. Consumer is considered dead




I think it is related to Consumer Reblancing Strategy.

Eager vs Cooperative Rebalancing

Consumer-group partition assignment strategies
1. RangeAssignor
2. RoundRobinAssignor
3. StickyAssignor
4. CooperativeStickyAssignor






`poll()` and `max.poll.interval.ms` 🤔🤔🤔 

max.poll.interval.ms is about maximum time between poll calls.
session.timeout.ms is about consumer liveness through heartbeats.

Modern Kafka Sends heartbeats 🤔🤔🤔 









---

  
