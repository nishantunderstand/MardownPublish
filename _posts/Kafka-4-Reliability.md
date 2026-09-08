# Idempotency

Idempotency Kafka Key Use Case
Producer enable.idempotence 

retries

Network failures happen.

Can we producer Idempotent ?  
enable.idempotence=true

Can we consumer Idempotent  🤔🤔🤔 
Can we consumerGroup Idempotent  : Doesn't Exists

---

Kafka Key  🤔🤔🤔 
Kafka uses the key primarily for partition selection
Kafka Key + Idempotency

---

Kafka Batch 
Kafka can batch messages.

1. Based on time : linger.ms
2. Based on Size : batch.size

Maximum approximate batch size before sending.

Example:
batch.size=32768

Conceptually:
Producer Buffer 🤔🤔🤔 


```
[M1][M2][M3][M4][M5]
──────────────────────
        32 KB

```

When the batch fills, it can be sent without waiting for linger.ms.

1. High throughput → larger batches
2. Low latency → smaller batching / lower linger

Difference B/W throughout and latency 🤔🤔🤔 


batch.size  → "How MUCH data should I collect?"
linger.ms   → "How LONG should I wait?"


WHICHEVER HAPPENS FIRST → SEND  

Whoever wins Between batch.size and linger.ms  : Based on that it send.

# Compression

compression.type=zstd

Other options:
1. none
2. gzip
3. snappy
4. lz4
5. zstd

Tradeoff:
1. Compression
2. Less network
3. Less disk usage
4. More CPU

A common modern choice is often:
lz4 → fast
zstd → better compression, with CPU tradeoffs

---
Messaging Protocols
TCP
HTTP
AMQP

What is difference Between Communication and Message Protcols ? 🤔🤔🤔 

---

Kafka Streams
1. KStream
2. KTable

----

Offset Commit 
1. Auto Commit
2. Manual Commit 

Delivery Semantics  Guarantees
1. At-most-once : No duplicates, but possible loss
2. At-least-once : No loss, but duplicates possible 🤔🤔🤔 
3. Exactly-once

Offset Commit and Delivery Semantics

---

cleanup.policy : whether the topic uses deletion, compaction, or both.

cleanup.policy=delete

Log Compaction  : How Old it is ?
Kafka can delete messages based on **time** or **size**.



Compaction
Suppose a user has Active, Suspended, Waiting , Premium
It will only store the latest One, i.e. Premium.




Retention vs Compaction 
1. Retention = delete messages based on age/size.
2. Compaction = keep the latest value for each key.



Retention Policy
Types 
1. Time-Based Retention
2. Size-Based Retention

---
# Reliability & Data Management

Kafka : Bytes
Serialization / Deserialization 🤔🤔🤔 
Where this conversion is happening ?
DownStream System  🤔🤔🤔 



Error Handling
Dead Letter Topic 
Retry Topic 
Retry Mechanism
DLT Dead Letter Topic  : We need to externally Define Topic 
DLQ Dead Letter Queue 
Poison Pill Problem
Retry : "Try again; this might work later."


Amazon SNS, ActiveMQ, Rabbit : They have DLQ InBuilt 🤔🤔🤔 

DLT vs DLQ

Retry Topic  vs  DLT Dead Letter Topic