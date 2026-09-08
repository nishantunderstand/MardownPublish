## Kafka System Design — Given Data

You are designing an **e-commerce event-driven system using Apache Kafka**.

### Services & Events

```text
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

Shipping Service
 ├── ShipmentCreated
 └── ShipmentDelivered

Analytics Service
 └── All business events
```

### Current Traffic

```text
Total incoming events = 10,000 messages/sec
```

### Expected Growth

```text
Expected traffic growth = 2× within the next 12 months
```

### Consumer Processing Capacity

```text
Payment Consumer     = 2,000 messages/sec
Inventory Consumer   = 5,000 messages/sec
Shipping Consumer    = 1,000 messages/sec
Analytics Consumer   = 10,000 messages/sec
```

### Consumer Groups

```text
Payment
Inventory
Shipping
Analytics
```

### Availability Requirement

```text
System should tolerate broker failures
```

### Kafka Cluster

```text
Number of brokers = 5
```

### Durability Requirement

```text
Production system
No acknowledged message should be lost because of a single broker failure
```

### Additional Requirement

```text
Consumers should be able to scale horizontally.
```

### Your Task

Design:

```text
1. Topic structure
2. Number of partitions
3. Number of consumers per consumer group
4. Replication Factor
5. min.insync.replicas
6. Producer acknowledgement strategy
7. How your design handles 2× future traffic
```

**That's all the data. You design the Kafka architecture from this.**
