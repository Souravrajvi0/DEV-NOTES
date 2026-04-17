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

---

```java
public class Employee {

    private int id;
    private String name;
    private String address;

    public void printPerformanceReport() { ... }

    public double computeSalary() { ... }

    public void updateEmployeeData() { ... }

    public void fetchEmployeeData() { ... }
}

```


# 🚨 Core Problem: Too Many Responsibilities

This class is responsible for:

1. Holding employee data
    
2. Printing reports
    
3. Salary calculation
    
4. Updating employee data
    
5. Fetching employee data
    

That’s **5 different responsibilities**.


## 🔴 Problem 1: Reporting Changes

If the report format changes:

- PDF instead of console
    
- JSON export
    
- Email report
    
- Add performance metrics
    

We must modify:

`printPerformanceReport()`

So the class changes because of reporting.

---

## 🔴 Problem 2: Salary Logic Changes

If:

- Tax rules change
    
- Bonus policy changes
    
- Performance-based pay added
    

We must modify:

`computeSalary()`

So the class changes because of payroll policy.

---

## 🔴 Problem 3: Database Changes

If:

- Switch from MySQL → MongoDB
    
- Add caching
    
- Add validation
    
- Change schema
    

We must modify:

`updateEmployeeData() fetchEmployeeData()`

So the class changes because of persistence.


# 💥 The Big Issue

Different teams own different responsibilities:

- HR team → salary rules
    
- Reporting team → performance reports
    
- DB team → persistence layer
    

Now all of them modify the SAME class.

This creates:

- Merge conflicts
    
- Risk of breaking unrelated logic
    
- Hard testing
    
- Tight coupling

# 🔥 This Violates SRP

**Single Responsibility Principle says:**

> A class should have only one reason to change.

But this class has multiple.

# 📉 Other Architectural Problems

## 1️⃣ Low Cohesion

Cohesion = How closely related methods are.

Here:

- Salary logic
    
- DB logic
    
- Reporting logic
    

They are unrelated.

So cohesion is LOW.

---

## 2️⃣ Tight Coupling

If tomorrow:

- We want to test salary logic only
    
- We don’t care about DB
    

Too bad. Everything is inside one class.

Testing becomes hard.

---

## 3️⃣ Hard To Scale Teamwise

In big companies:

- 200 engineers
    
- Parallel feature development
    

Monolithic classes become a bottleneck.


---

# 🧠 How It Should Be Designed (Proper LLD)

We separate responsibilities.

---

## ✅ Better Design

```
class Employee {
    private int id;
    private String name;
    private String address;
}
```

Pure data model only.

---

```
class SalaryCalculator {
    public double computeSalary(Employee emp) { ... }
}
```

---

```
class EmployeeRepository {
    public void update(Employee emp) { ... }
    public Employee fetch(int id) { ... }
}
```

---

```
class PerformanceReportPrinter {
    public void print(Employee emp) { ... }
}
```

Now:

- Salary changes → modify SalaryCalculator
- DB changes → modify Repository
- Report changes → modify Printer

Each class has ONE responsibility.

High cohesion.  
Low coupling.

---

# 🏢 Why Big Companies Care So Much

Because:

When codebase grows to 5 million lines:

- Small bad decisions become huge maintenance cost.
- Refactoring becomes risky.
- Bugs multiply.

LLD prevents future chaos.

---

# ⚡ Deep Insight

The problem is NOT that the code doesn't work.

It works.

The problem is:

> It does not scale in complexity.

Scalability is not only about traffic.  
It’s also about **change scalability**.

Can your code survive 5 years of feature updates?

That’s what LLD evaluates.



# 🔹 What is SRP?

> A class should have only **one reason to change**.

Most beginners misunderstand this.

It does NOT mean:

- “Class should do only one thing”
    

It means:

- “Class should have only one type of responsibility”
    
- “Only one stakeholder should force changes to it”
    

That difference is VERY important.


# 🔥 The Real Meaning: “Reason to Change”

Ask this question:

👉 Why would this class change in the future?

If you can answer that in multiple different ways  
→ SRP is violated.

```java
class Employee {
    String name;
    double salary;

    void calculateSalary() { ... }
    void saveToDatabase() { ... }
    void generateReport() { ... }
}

```


Now ask:

Why would this class change?

1. Salary rules change
    
2. Database changes
    
3. Report format changes
    

Three different reasons.

Three different stakeholders.

❌ SRP violated.


# 🎯 What Is Responsibility?

Responsibility = A specific area of concern.

Examples:

- Business logic
    
- Persistence logic
    
- Reporting logic
    
- Validation logic
    
- Notification logic

Each of these is separate responsibility.

# 🧠 Deep Insight: Stakeholders

This is how seniors think.

Who would ask you to modify this class?

- Finance team → salary changes
    
- DB team → database changes
    
- Reporting team → report format changes
    

If multiple departments affect the same class  
→ It’s wrong design.



```
class Employee {
    String name;
    double salary;
}
```
```
class SalaryCalculator {
    double calculate(Employee emp) { ... }
}
```
```
class EmployeeRepository {
    void save(Employee emp) { ... }
}
```
```
class EmployeeReportGenerator {
    void generate(Employee emp) { ... }
}
```

Now:

- Finance changes → only SalaryCalculator changes
- DB changes → only Repository changes
- Reporting changes → only ReportGenerator changes

Each class has one reason to change.

✔ High cohesion  
✔ Low coupling  
✔ Easy testing  
✔ Scalable design


# 🔥 Why SRP Is So Powerful

Because change is constant.

Code is written once.  
Maintained for years.

SRP reduces:

- Side effects
    
- Merge conflicts
    
- Unrelated breakage
    
- Fear of modification

# SRP is NOT about number of methods.

A class can have 20 methods and still follow SRP  
if they all serve the same responsibility.

Example:

```
class StringUtils {
    trim()
    toUpper()
    toLower()
    reverse()
}
```

All methods are string-related utilities.

That’s one responsibility.

SRP is satisfied.


# ⚠ Common SRP Mistake

People sometimes over-split.

Too many tiny classes.  
Unnecessary abstraction.

SRP does NOT mean:

- Every method → new class
    
- Every line → separate class
    

It means:

- One axis of change per class.
