1. [[Kafka-Failure-1.excalidraw]]
2. [[Kafka-Failure-2.excalidraw]]


# Kafka Consumer Crash & Offset Commit

Let's understand the topic from the ground up.

---

# 1. First Principle 🧱

First principle:

> **Kafka does not know whether your business logic succeeded. It only knows which offset you committed.**

Kafka stores messages in a partition:

```text
Partition 0

Offset
  0     A
  1     B
  2     C
  3     D
  4     E
```

A consumer reads them:

```text
Kafka                         Consumer

  A  ───────────────────────→ process A
  B  ───────────────────────→ process B
  C  ───────────────────────→ process C
```

Kafka needs to know:

> "Where should this consumer continue from after restart?"

That's what the **committed offset** is for.

Think of it as a **checkpoint**.

```text
Messages:

A → B → C → D → E
        ↑
   last checkpoint
```

---

# 2. Second Principle 🧠

Now let's ask:

### What is an offset?

An offset is simply the **position of a record inside a partition**.

```text
Partition 0

Offset     Message

  0          A
  1          B
  2          C
  3          D
```

Suppose consumer has processed:

```text
A
B
C
```

but has committed only up to:

```text
Offset = 2
```

The consumer crashes.

Kafka says:

> "My last known checkpoint is offset 2."

Therefore, after restart, the consumer can continue from the next uncommitted record.

```text
             CRASH
               ↓
A → B → C → D → E
          ↑
     last committed
               ↓
          restart
               ↓
          D → E
```

The key principle:

> **Kafka's committed offset represents consumer progress, not business success.**

---

# 3. The Most Important Crash Scenario 🔥

Consider:

```text
Kafka
  |
  | Message: Order-101
  ↓
Consumer
  |
  ↓
Process Order
  |
  ↓
Database updated ✅
  |
  X
CRASH 💥
  |
  X
Offset NOT committed
```

Consumer restarts:

```text
Kafka
  |
  ↓
Last committed offset
  |
  ↓
Order-101
  |
  ↓
Process again
```

So:

```text
Order-101
    ↓
DB update
    ↓
CRASH
    ↓
Order-101 again
    ↓
DB update again
```

This is **duplicate processing**.

---

# 4. Real-Life Simple Example 🏦

Imagine a bank employee processing transactions from a notebook.

```text
Notebook:

1. ₹100 transfer
2. ₹500 transfer
3. ₹200 transfer
4. ₹300 transfer
```

The employee processes transaction #2.

Then the employee writes:

```text
"Completed till transaction #2"
```

This is like:

```text
PROCESS
   ↓
COMMIT OFFSET
```

But suppose:

```text
Process ₹500
     ↓
Employee crashes 💥
     ↓
Didn't mark it completed
```

When another employee resumes:

```text
"Last confirmed transaction = #1"

Therefore:

Process #2 again
```

That's exactly the Kafka situation.

---

# 5. Four Important Failure Scenarios

This is where interviewers like to test you.

## Scenario 1 — Crash BEFORE processing

```text
Poll
 ↓
💥 Crash
 ↓
No processing
 ↓
No commit
```

Message will be processed again.

```text
At-least-once
```

---

## Scenario 2 — Process BEFORE commit

```text
Poll
 ↓
Process ✅
 ↓
💥 Crash
 ↓
Commit ❌
```

After restart:

```text
Process again
```

➡️ **Duplicate processing**

---

## Scenario 3 — Commit BEFORE processing

```text
Poll
 ↓
Commit ✅
 ↓
💥 Crash
 ↓
Process ❌
```

Now Kafka thinks:

> "This message is already handled."

Consumer may skip it.

➡️ **Potential message loss**

This is why blindly committing before processing is dangerous. 🤔🤔🤔 

---

## Scenario 4 — Process → Commit → Crash

```text
Poll
 ↓
Process ✅
 ↓
Commit ✅
 ↓
💥 Crash
```

After restart:

```text
Kafka sees committed offset
        ↓
moves forward
        ↓
doesn't normally reprocess it
```

---

# 6. Delivery Semantics

These failure scenarios lead to three major Kafka concepts.

### At-most-once

```text
COMMIT
  ↓
PROCESS
```

Possible result:

```text
0 or 1 processing
```

Message can be lost.

---

### At-least-once

```text
PROCESS
  ↓
COMMIT
```

Possible result:

```text
1 or more processing
```

Message won't normally be lost due to this failure ordering, but duplicates can happen.

---

### Exactly-once

The goal:

```text
PROCESS + OFFSET COMMIT
        ↓
    Atomic operation
```

Meaning:

> Either both happen, or neither happens.

Kafka provides transactional mechanisms for certain Kafka-to-Kafka workflows, but **exactly-once is not automatically guaranteed for arbitrary external systems such as a database**.

---

# 7. Important Nuance ⚠️

### "Consumer processed offset 100" ≠ "Kafka committed offset 100"

These are different concepts.

Kafka consumer internally tracks positions such as:

```text
Position
   ↓
What consumer has fetched/read

Committed Offset
   ↓
What Kafka has stored as checkpoint
```

Example:

```text
Kafka:

100 → A
101 → B
102 → C
103 → D

Consumer position = 103
Committed offset = 101
```

The consumer may have already fetched/processed further messages while Kafka's durable checkpoint is still behind.

If it crashes:

```text
Position disappears ❌

Committed offset remains ✅
```

Therefore it can resume from the committed position.

---

# 8. Another Important Nuance: Commit Offset Meaning

Suppose:

```text
Offset:

100 → A
101 → B
102 → C
```

Consumer processes A and B.

It may commit:

```text
offset = 102
```

Why 102?

Because Kafka's committed offset generally represents the **next record to consume**, not "the last record processed."

So:

```text
Processed:
100
101

Commit:
102
```

Mental shortcut:

> **Commit offset = "start from here next time."**

---

# 9. Interview Trap 🚨

### Interviewer:

> "Consumer processed message 100. Therefore Kafka has acknowledged message 100. Correct?"

❌ **Wrong.**

Processing and committing are separate.

Correct answer:

> "Processing means the consumer has handled the record. The committed offset is the checkpoint persisted for the consumer group. If processing succeeds but the commit fails, the record can be processed again."

---

### Another Trap

Interviewer:

> "Kafka guarantees exactly-once because it doesn't send duplicates."

❌ Wrong.

Kafka can result in duplicate processing depending on the consumer failure/commit timing. 🤔🤔🤔 

For example:

```text
Process
   ↓
💥 Crash
   ↓
Commit never happened
   ↓
Restart
   ↓
Process again
```

---

# 10. Database Trap 🔥

This is an extremely common interview question.

Suppose:

```text
Kafka
  ↓
Consumer
  ↓
Update DB
  ↓
Commit Kafka offset
```

What if:

```text
Update DB ✅
      ↓
    CRASH 💥
      ↓
Kafka commit ❌
```

After restart:

```text
Kafka sends message again
        ↓
DB update again
```

You now have a **duplicate business operation**. 

This is why real systems often use:

```text
Kafka
  ↓
Consumer
  ↓
Idempotent processing
  ↓
Database
```

For example, store a unique transaction/event ID:

```text
eventId = abc123
```

Before processing:

```text
Has abc123 already been processed?
       /        \
     YES        NO
      ↓          ↓
    Skip       Process
                 ↓
             Save abc123
```

---

# 11. Mental Model 🧠

Remember **three things**:

```text
┌───────────────────────────────┐
│          KAFKA                │
│                               │
│ Messages → offsets            │
│                               │
│ "What exists?"                │
└───────────────┬───────────────┘
                │
                ↓
┌───────────────────────────────┐
│        CONSUMER               │
│                               │
│ Process messages              │
│                               │
│ "What have I done?"           │
└───────────────┬───────────────┘
                │
                ↓
┌───────────────────────────────┐
│      COMMITTED OFFSET         │
│                               │
│ Checkpoint                    │
│                               │
│ "Where should I restart?"     │
└───────────────────────────────┘
```

### The golden rule:

> **Process first → Commit later → Crash in between = Duplicate processing.**

And:

> **Commit first → Process later → Crash in between = Possible message loss.**

Therefore:

```text
              Kafka Consumer
                   │
                   ↓
              Process
                   │
          ┌────────┴────────┐
          │                 │
       Success           Failure
          │                 │
          ↓                 ↓
       Commit            Retry
```

### One-line interview answer

> **Kafka offset commit is a checkpoint. If a consumer crashes after processing but before committing, Kafka resumes from the last committed offset, so the message may be processed again, resulting in at-least-once delivery and possible duplicates.**