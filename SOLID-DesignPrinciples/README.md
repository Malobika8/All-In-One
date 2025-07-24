# 🧠 **SOLID Principles Recap**

---

### 🟢 **S – Single Responsibility Principle (SRP)**

> A class should have **only one reason to change**.

✅ One class = One job
🔧 Split responsibilities (e.g., business logic vs. email sending)

**Example:**
Break `UserService` into `UserRegistration`, `PasswordValidator`, `EmailSender`.

---

### 🟡 **O – Open/Closed Principle (OCP)**

> Classes should be **open for extension**, but **closed for modification**.

✅ Add new behavior **without touching existing code**
🔧 Use interfaces, inheritance, or composition

**Example:**
Use `Payment` interface with `UPIPayment`, `PaypalPayment` instead of `if-else` in `PaymentProcessor`.

---

### 🟠 **L – Liskov Substitution Principle (LSP)**

> Subclasses should be **substitutable** for their base classes **without breaking correctness**.

✅ If `A` is a parent of `B`, you should be able to use `B` anywhere `A` is expected
🔧 Watch out for overridden methods that throw exceptions

**Example:**
Avoid `Square extends Rectangle` if `Square.setWidth()` breaks behavior.

---

### 🔵 **I – Interface Segregation Principle (ISP)**

> Clients should **not be forced** to depend on methods they **don’t use**.

✅ Break large interfaces into **small, specific ones**
🔧 Prefer multiple fine-grained interfaces over a single fat one

**Example:**
Split `Machine` into `Printer`, `Scanner`, `FaxMachine` — so `Bicycle` or `OldPrinter` only implement what they need.

---

### 🟣 **D – Dependency Inversion Principle (DIP)**

> **High-level modules** should depend on **abstractions**, not on concrete implementations.

✅ Program to **interfaces**, not `new`-ing classes
🔧 Inject dependencies using constructors (Spring does this automatically)

**Example:**
Use a `Notifier` interface for `EmailService`, `SMSService`, and inject it into `NotificationService`.

---

## ✅ Real-World Summary with Spring Boot

| Principle | How Spring supports it                                                                      |
| --------- | ------------------------------------------------------------------------------------------- |
| SRP       | Encourages small `@Service`, `@Component`, `@Repository` classes                            |
| OCP       | Supports pluggable behaviors via `@Component`, AOP, strategies                              |
| LSP       | Uses interface-driven designs (`CrudRepository`, etc.)                                      |
| ISP       | Breaks down functionality into focused interfaces (`CrudRepository`, `JpaRepository`, etc.) |
| DIP       | Uses dependency injection (`@Autowired`, constructor injection, Bean wiring)                |

---

