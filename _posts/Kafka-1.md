
1. [[Kafka-Architecuture.excalidraw]]
2. [[Kafka-Failure-1.excalidraw]]


[Spring Boot + Kafka Course | Learn Apache Kafka in One Shot!](https://www.youtube.com/watch?v=gpx7smdUkgU&t=667s)  : Only Theory 

---

Service to Service 
1. Message
	1. MessageQueue : RabbitMQ, ActiveMQ
	2. Log  : Kafka 

Where does Amazon SNS (Simple Notiification Service) ? 🤔🤔🤔 

MessageQueue and MessageOriented Middleware (MOM) 🤔🤔🤔 

---

MessageOriented Middleware (MOM)
It is software that allows applications to communicate through messages instead of direct calls.

Message Broker
Loosely Coupling

Producer → Message Broker → Consumer
ActiveMQ 
RabbitMQ
Kafka
Redis Pub-Sub

---

Parameter of Judgement :  🤔🤔🤔 
Message Storage 
Consumer OFF / ON 
Message Replay 
Consumer Groups 
Scalability 
Pull vs Push Model 
Ordering 
Kafka does NOT guarantee global ordering across all partitions.
Ordering is guaranteed only inside each partition.


---

Depend Upon Nature of Business  : 

When to Pick Rabbit MQ 
If system has:
- moderate traffic
- straightforward work queues
- task distribution
- relatively short-lived messages
- no significant replay requirement
I'd seriously consider RabbitMQ.



RabbitMQ / ActiveMQ
1. task processing
2. work queues
3. request distribution
4. routing
5. low-latency messaging


Why Kafka ? Why not use ActiveMQ or Rabbit MQ ? 
[Apache Kafka Will Finally Makes Sense After This Video](https://www.youtube.com/watch?v=yjqwhr23vCs)


When to use Kafka ?
Why Kafka?
Why do we need Kafka?

Advantages of Kafka
Disadvantage of kafka


Kafka
event streaming
high throughput
distributed systems
event-driven microservices
analytics
log/data pipelines
replaying events
multiple independent consumers

[https://www.instagram.com/reels/Db5v8fxPvUS/](https://www.instagram.com/reels/Db5v8fxPvUS/)


Message Queue  : 1 Publisher : 1 Subscriber
Pub-Sub  : 1 Publisher : N Subscriber
Kafka : 1 Publisher : N Subscriber + Distributed + Persistent Log 
KAFKA Vs RabbitMQ vs ActiveMQ vs AWS SNS 


SNS vs KAFKA vs RabbitMQ
https://www.instagram.com/reels/Dc81cdeIZrP/


