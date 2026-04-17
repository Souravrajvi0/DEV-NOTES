A **transaction** is a **logical unit of work** that must be treated as **one indivisible operation**.

> Either **everything inside it happens**, or **nothing happens at all**.

Think in **real-life terms**:

- You withdraw ₹1,000 from ATM
	- Money deducted from bank account
	- Cash dispensed
	- Receipt printed

If **any step fails**, the whole operation must **not partially happen**.

➡️ That *entire sequence* is a **transaction**.

---

# 2️⃣ Why transactions exist (the core problem they solve)

Without transactions, databases face **3 fatal problems**:

### ❌ Partial updates

- Money deducted but not credited elsewhere

### ❌ Inconsistent state

- One table updated, another not

### ❌ Concurrency chaos

- Two users modifying same data simultaneously

Transactions exist to **protect data integrity under failure and concurrency**.

---

# 3️⃣ Formal definition

> A **transaction** is a sequence of database operations that:

- Executes as a **single logical unit**
- Moves the database from **one consistent state → another consistent state**

---

# 4️⃣ The ACID properties (heart of transactions)

Every serious transaction system follows **ACID**.

## A — Atomicity (“all or nothing”)

> Either the whole transaction succeeds, or **everything is undone**.

If a transaction has 10 operations:

- 9 succeed + 1 fails → ❌ **all rolled back**

No half-states allowed.

---

## C — Consistency (“rules are never broken”)

> A transaction must take the database from **one valid state to another valid state**

Examples:

- Account balance cannot go negative
- Foreign keys must always point to valid rows
- Unique constraints must stay unique

If a transaction violates rules → ❌ **abort**

> ⚠️ Consistency is a **business + schema responsibility**, not magic

---

## I — Isolation (“as if alone”)

> Multiple transactions can run concurrently, but **each behaves as if it’s the only one**

Even if:

- 1000 users are updating same table
- Each transaction should **see a stable world**

This is the hardest property to implement.

---

## D — Durability (“once committed, forever”)

> Once a transaction commits, its changes **survive crashes, power loss, restarts**

Achieved using:

- Write-ahead logs (WAL)
- Disk flushes
- Replication

---

# 5️⃣ Transaction lifecycle (step-by-step)

A transaction moves through **states**.

### 1\. Active

Transaction is running.

### 2\. Partially Committed

All statements executed, but not yet written safely to disk.

### 3\. Committed

Changes are **permanent**.

### 4\. Failed

Something went wrong (constraint violation, crash).

### 5\. Aborted (Rolled Back)

All changes undone, database restored to previous state.

```
Active → Partially Committed → Committed
   ↓
 Failed → Aborted
```

---

# 6️⃣ Commit, Rollback, Abort (very important distinction)

### ✅ Commit

> “Everything went fine. Make changes permanent.”

- Flush logs to disk
- Release locks
- Other transactions can now see changes

---

### 🔄 Rollback

> “Undo everything done in this transaction.”

- Restore old values using logs
- Database returns to previous consistent state

Rollback can be:

- Manual
- Automatic (on error)

---

### ❌ Abort

> “Transaction failed and **must be rolled back**.”

Abort is a **decision/state**, rollback is the **action**.

> Abort ⇒ Rollback  
> Rollback ≠ always abort (can be user-requested)

---

# 7️⃣ What happens internally during rollback?

Databases **never overwrite data directly**.

Instead:

1. Before changing anything → write **UNDO log**
2. Make in-memory changes
3. On commit → write **REDO log**
4. On crash:
	- Use logs to undo or redo safely

This is called **Write-Ahead Logging (WAL)**.

---

# 8️⃣ Concurrency problems transactions solve

Without isolation, you get **anomalies**.

### Dirty Read

Reading uncommitted data

### Lost Update

Two transactions overwrite each other

### Non-repeatable Read

Same query gives different results

### Phantom Read

New rows appear mid-transaction

Isolation levels exist to **control trade-offs** (we’ll deep dive later).

---

# 9️⃣ Are transactions only in RDBMS?

**No. This is a BIG misconception.**

Let’s break it down clearly.

---

## ✅ RDBMS (PostgreSQL, MySQL, Oracle)

- **Full ACID transactions**
- Strong consistency
- Fine-grained locks / MVCC

✔️ Best for:

- Financial systems
- Inventory
- User accounts

---

## ⚠️ NoSQL databases (varies a LOT)

### Key-Value / Document Stores

| Database | Transaction Support |
| --- | --- |
| Redis | Single-command atomicity, limited multi-key |
| MongoDB | Multi-document ACID (since v4.0) |
| DynamoDB | Transactions added later |
| Cassandra | Limited (lightweight transactions) |

> Early NoSQL **sacrificed transactions for scale**  
> Modern NoSQL **reintroduced transactions carefully**

---

## 🧠 Distributed Systems Reality

Across **multiple machines**, transactions become **very expensive**.

Problems:

- Network failures
- Partial commits
- Clock skew

This led to:

- BASE model
- Eventual consistency
- Saga pattern

---

# 🔁 Distributed Transactions (2PC)

When transaction spans **multiple databases**:

- Phase 1: Prepare
- Phase 2: Commit

Problems:

- Coordinator failure
- Blocking
- Slow

That’s why **microservices avoid DB-level distributed transactions**.

---

# 10️⃣ Transactions vs “Atomic operations”

Important distinction:

- **Atomic operation** ≠ **Transaction**

Atomic:

- One operation (e.g., increment counter)

Transaction:

- Multiple steps treated as one unit

---

# 11️⃣ When NOT to use transactions

Transactions are **expensive**.

Avoid for:

- Logs
- Analytics
- Append-only data
- High-throughput events

Use:

- Event sourcing
- Idempotent writes
- Eventually consistent flows

---

# 12️⃣ Mental model you should keep

Think of a transaction as:

> “A **bubble of isolation** where changes are invisible to others  
> until I say **COMMIT**  
> or completely erased if I **ROLLBACK**.”

---

# 13️⃣ Why this matters for you (as a backend engineer)

Everything you’re working toward depends on this:

- LeetCode DB problems
- Payment systems
- Inventory locking
- Concurrency bugs
- Data corruption issues

Most **production bugs** are **transaction misunderstandings**, not syntax issues