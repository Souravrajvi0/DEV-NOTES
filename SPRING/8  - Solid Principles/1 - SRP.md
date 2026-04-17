# SYSTEM DESIGN

# 1️⃣ What is System Design?
System design is divided into:

- **HLD → High Level Design**
- **LLD → Low Level Design**

Think of it like building a city.

- HLD = City planning
- LLD = Individual building architecture

---

# 2️⃣ What is High Level Design (HLD)?

## 🏗 HLD = Architecture of the entire system

It answers questions like:

- What components exist?
- How do they communicate?
- What databases are used?
- Where does caching sit?
- Is it monolith or microservices?
- How does it scale?

---

### Example: Instagram System (HLD)

If we design Instagram:

### Components:

- Load Balancer
- Web Servers
- API Servers
- Database
- Cache (Redis)
- CDN
- Object Storage

HLD focuses on:

- Horizontal scaling
- Database sharding
- Caching strategy
- Failover
- CAP theorem decisions
- Throughput & latency

---

### 🔥 Big Company Main Concern (HLD side)

1. Scalability
2. Availability
3. Fault tolerance
4. Performance under heavy load

---

# 3️⃣ What is Low Level Design (LLD)?

Now zoom inside one service.

Suppose we zoom inside:

👉 “User Service”

Now we design:

- Classes
- Interfaces
- Relationships
- Methods
- Dependency structure
- Code maintainability

That is **LLD**.

---

### LLD Example: E-commerce Order Service

We decide:

- Order class
- PaymentProcessor interface
- CardPayment class
- UPIPayment class
- OrderService class
- Repository layer

LLD focuses on:

- Clean code
- Extensibility
- Maintainability
- Separation of concerns
- SOLID principles
- Design patterns

---

# 4️⃣ Why Big Companies Worry About Maintainability?

Because code lives for 10+ years.

Imagine:

- 200 engineers
- 5 million lines of code
- 100 microservices
- Frequent feature updates

If code is messy:

- Every change breaks something
- Debugging becomes nightmare
- Refactoring impossible
- Onboarding slow

This is why LLD matters.

---

# 5️⃣ What is Bad Code vs Good Code?

## ❌ Bad Code Example

```
class OrderService {
    public void processOrder(String paymentType) {
        if(paymentType.equals("CARD")) {
            // card logic
        } else if(paymentType.equals("UPI")) {
            // upi logic
        } else if(paymentType.equals("NETBANKING")) {
            // netbanking logic
        }
    }
}
```

Problem:

- Adding new payment → modify this class
- Violates Open/Closed principle
- Tight coupling
- Hard to test

---

## ✅ Good Code Example

```
interface PaymentProcessor {
    void pay();
}

class CardPayment implements PaymentProcessor {
    public void pay() {}
}

class UPIPayment implements PaymentProcessor {
    public void pay() {}
}

class OrderService {
    private PaymentProcessor paymentProcessor;

    public OrderService(PaymentProcessor paymentProcessor) {
        this.paymentProcessor = paymentProcessor;
    }

    public void processOrder() {
        paymentProcessor.pay();
    }
}
```

Now:

- Add new payment → just create new class
- No modification needed
- Loose coupling
- Easily testable

---

# 6️⃣ This Leads to Design Patterns

When engineers noticed recurring problems:

- Object creation problems
- Dependency problems
- Code duplication problems
- Tight coupling problems

They created **design patterns**.

Design patterns are:

> Reusable solutions to common design problems.

---

### Examples of Design Patterns

| Category | Pattern | Problem Solved |
| --- | --- | --- |
| Creational | Singleton | Only one object |
| Creational | Factory | Object creation logic |
| Structural | Adapter | Incompatible interfaces |
| Behavioral | Strategy | Switching behaviors |

---

# 7️⃣ Now Comes SOLID Principles

SOLID = 5 design principles that make code:

- Maintainable
- Extendable
- Scalable (in code structure sense)

SOLID stands for:

### S → Single Responsibility Principle

One class → one reason to change

### O → Open/Closed Principle

Open for extension, closed for modification

### L → Liskov Substitution Principle

Child class should replace parent safely

### I → Interface Segregation Principle

Don't force classes to implement unused methods

### D → Dependency Inversion Principle

Depend on abstractions, not concrete classes

---

# 8️⃣ How Everything Connects

Let’s connect all concepts:

Scalability problem at system level → HLD

Maintainability problem at code level → LLD

LLD problems → solved by:

- Clean Architecture
- SOLID principles
- Design Patterns
- Layered Architecture
- Dependency Injection

---

# 9️⃣ What Interviewers Check in LLD

They look for:

1. Proper class responsibility
2. Loose coupling
3. High cohesion
4. Extensibility
5. Correct use of patterns
6. Edge case handling
7. Naming clarity
8. Testability

They don’t care about syntax.  
They care about thinking.

---

# 🔥 Important Concept: Cohesion vs Coupling

- High Cohesion = Class does one thing well
- Low Coupling = Classes don’t depend tightly on each other

Best system:  
High cohesion + Low coupling

---

# 🔟 Scalability vs Maintainability Difference

| Scalability | Maintainability |
| --- | --- |
| System handles more traffic | Code handles more features |
| Load balancing | Modular classes |
| Caching | SOLID |
| Sharding | Design patterns |

---

# 1️⃣1️⃣ Why This Is Important For You

Since you're building backend systems and microservices:

- HLD helps you design services
- LLD helps you write clean code
- SOLID helps you avoid tech debt
- Design patterns help you solve recurring problems

Without this:

You’ll write working code.  
With this:  
You’ll write engineering code.
