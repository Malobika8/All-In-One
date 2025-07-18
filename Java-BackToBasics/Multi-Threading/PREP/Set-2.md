# Situational Question:
> Suppose you're building a banking app.
> Two threads are performing `withdraw()` and `deposit()` at the same time on the same account object.
> What problems might arise?
> How would you ensure thread safety?

👉 Answer both:

1. What problems will happen?
2. How would you solve it?

### Sol:

In a multithreaded banking system, if two threads perform `withdraw()` and `deposit()` at the same time on the same account, a **race condition** can occur.
For example, one thread might be reading the balance while another is updating it — leading to **inconsistent or incorrect account balance**.

> To ensure thread safety:

* Identify the **critical section** — the code that reads/modifies the account balance.
* Protect it using a **`synchronized` block or method**, so only one thread can access it at a time.
* This ensures operations like `withdraw()` and `deposit()` are **atomic** and the account always stays in a **consistent state**.

> If needed for performance, we could also use **`ReentrantLock`** for finer-grained control (like try-locking, interruptibility, etc.).

---

# Task:

**Write an `Account` class with:**

* A `balance` field.
* `deposit(int amount)` and `withdraw(int amount)` methods.
* Both methods should be **thread-safe** using `synchronized`.

Then in `main()`, create two threads:

* One deposits 1000 three times.
* One withdraws 500 two times.

### Sol:

```java

class Main {
   
    public static void main(String[] args) throws InterruptedException {
        // List<Employee> list = Arrays.asList(
        // new Employee("pika", 30000, "hr"),
        // new Employee("lama", 40000, "it"),
        // new Employee("arun", 25000, "it"),
        // new Employee("john", 35000, "hr"),
        // new Employee("ankit", 27000, "finance")
        // );
        List<Thread> list = new ArrayList<>();
        Account account = new Account(20000);
        
        Runnable credit = ()->{
            account.deposit(1000);
        };
        Runnable debit = ()->{
            account.withdraw(500);
        };
        
        for(int i=0;i<3;i++){
            Thread thread1 = new Thread(credit); 
            thread1.start();
            list.add(thread1);
        }
        for(int i=0;i<2;i++){
            Thread thread2 = new Thread(debit); 
            thread2.start();
            list.add(thread2);
        }
        
        for(Thread th:list)
            th.join();
            
        System.out.println(account.getBalance());
    }
}

class Account{
    
    private int balance;
    
    Account(int balance){
        this.balance = balance;
    }
    
    public int getBalance(){
        return balance;
    }
    
    public synchronized void deposit(int amount){
        balance = balance+amount;
    }
    public synchronized void withdraw(int amount){
        balance = balance-amount;
    }
}
```

---


