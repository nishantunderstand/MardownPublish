Thread

Syncrhonizatuion

Critical Section
	1 Thread : 
		Synchronized method 
		Synchronized Block (Better than Method)
	2 Thread or more : 
		Seamphore
	

---
Object has By Default Lock 
i.e. Mutex Lock
	wait
	notify
	notifyAll
	
---
Lock Interface
RetrantLock 
Manually Lock or unlock




----

🔐 Locks (Mutual Exclusion)
Intrinsic Lock → synchronized
Extrinsic Lock → Lock, ReentrantLock

Synchronizers (Coordination / Control)
Semaphore
CountDownLatch
CyclicBarrier
Phaser

Lock = Binary Semaphore (1 permit) ✔

Lock	1 permit (only 1 thread)
Semaphore	N permits (multiple threads allowed)

ReentrantLock : 1 Thread at time
Seamphore : N Thread at a time


ReentrantLock = 🚪 Single-entry door with key (owner-based)
Semaphore = 🎟️ Ticket system (permits, no ownership)

“ReentrantLock ensures mutual exclusion with ownership, while Semaphore controls concurrency using permits without ownership.”



Semaphore → “How many can enter?”
CountDownLatch → “Wait until done”
CyclicBarrier → “Wait for each other”
Phaser → “Multi-level coordination”