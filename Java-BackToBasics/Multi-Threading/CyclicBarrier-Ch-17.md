
## 🔄 What is a **CyclicBarrier** in Java?

`CyclicBarrier` is a **synchronization aid** in `java.util.concurrent` that allows a **group of threads to wait for each other** at a **common barrier point**.

Think of it like a **meeting point** where all threads must arrive before moving forward **together**.

---

### 🧠 Real-life Analogy:

Imagine 5 friends want to start a game. Each one needs to say “Ready” before the game begins. Nobody starts playing until **all 5** have said “Ready”. Once they have, the game starts **simultaneously** for everyone.

That’s a **CyclicBarrier** in action.

---

## 🔧 Basic Syntax

```java
CyclicBarrier barrier = new CyclicBarrier(int parties);
```

- `parties`: Number of threads that must call `await()` before they can all proceed.

Optional version:
```java
CyclicBarrier barrier = new CyclicBarrier(int parties, Runnable barrierAction);
```
- `barrierAction`: Runs once when all threads reach the barrier (e.g. logging, setup, etc.)

---

## 🧩 Simple Example

```java
import java.util.concurrent.*;

public class BarrierExample {
    public static void main(String[] args) {
        int threadCount = 3;

        CyclicBarrier barrier = new CyclicBarrier(threadCount, () -> {
            System.out.println("All threads reached the barrier. Proceeding together!");
        });

        Runnable task = () -> {
            System.out.println(Thread.currentThread().getName() + " is doing some work...");
            try {
                Thread.sleep((long) (Math.random() * 2000)); // simulate work
                System.out.println(Thread.currentThread().getName() + " is waiting at the barrier.");
                barrier.await(); // waits here
                System.out.println(Thread.currentThread().getName() + " passed the barrier.");
            } catch (InterruptedException | BrokenBarrierException e) {
                e.printStackTrace();
            }
        };

        for (int i = 0; i < threadCount; i++) {
            new Thread(task).start();
        }
    }
}
```

---

### 🔁 Why “Cyclic”?

Because **it can be reused** after the threads cross the barrier.

For example, if you use it in a loop, it can pause threads again at the next iteration.

```java
for (int i = 0; i < 3; i++) {
    barrier.await();  // wait at barrier in each round
}
```

This is unlike `CountDownLatch`, which can be used **only once**.

---

### ⚠️ Notes:

- If one thread fails or is interrupted, the barrier is **broken**.
- You can check this using `barrier.isBroken()`.
- A `BrokenBarrierException` is thrown if the barrier is broken while waiting.

---

## 🔄 `CyclicBarrier` vs `CountDownLatch`

| Feature | `CyclicBarrier` | `CountDownLatch` |
|--------|------------------|------------------|
| Reusable? | ✅ Yes | ❌ No |
| Waits for how many? | All threads to arrive | One or more threads wait for a few |
| Who waits? | All threads | Usually main thread waits |
| Action on trigger? | Optional Runnable | None |

---

## 🚦 Summary:

- Threads **wait** at a **barrier** until all arrive
- Once all have called `await()`, they all **proceed together**
- It’s **cyclic**, so you can use it **again and again**
- Useful for **multi-phase** tasks or coordinated steps (e.g., simulations, games, parallel algorithms)

---

## 🌀 Why is it called **CyclicBarrier**?

**“Cyclic”** means **reusable in cycles** — as in, after all threads have reached the barrier **once**, the barrier **resets itself** so the same group of threads can use it **again and again** in the next round.

That’s it.

---

### 👟 Real-World Analogy: Group Race Rounds

Imagine 3 runners are doing **3 rounds** of a relay race.

1. All runners must **line up together at the starting line** (barrier).
2. Once all 3 are ready, they **start running** (barrier opens).
3. After finishing round 1, they go back to the starting line (barrier resets).
4. Again, they wait for each other.
5. Then they do round 2.
6. Same for round 3.

👉 The **barrier resets** after each round — this is what makes it **cyclic**.

---

## 🔁 Now in Code

Here’s how it looks with `CyclicBarrier` used in a **loop**:

```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> {
    System.out.println("All threads reached the barrier. Moving to next round.\n");
});

Runnable task = () -> {
    try {
        for (int i = 1; i <= 3; i++) {
            System.out.println(Thread.currentThread().getName() + " is working in round " + i);
            Thread.sleep((long)(Math.random() * 1000));
            
            System.out.println(Thread.currentThread().getName() + " waiting at barrier in round " + i);
            barrier.await();  // Barrier point for this round

            System.out.println(Thread.currentThread().getName() + " passed barrier in round " + i + "\n");
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
};

for (int i = 0; i < 3; i++) {
    new Thread(task).start();
}
```

---

### 🔁 How this works:

- 3 threads each do work in **3 rounds**.
- In every round, they all call `barrier.await()` — **and wait**.
- Once **all 3 threads** reach the barrier, it opens for that round.
- Then the barrier is **automatically reset**, ready for the **next round**.

That’s the **“cyclic”** part.

---

### 💡 Contrast with CountDownLatch

- `CountDownLatch` can **only be used once**. Once the count hits 0, it’s done forever.
- `CyclicBarrier` can be **reused again and again** in a loop or multiple phases.

---

Let's dive into a **real-world style example** of using `CyclicBarrier` in a **parallel matrix operation**, broken down step by step. We’ll simulate a simple **phased matrix computation** using threads — and you’ll see exactly where the `CyclicBarrier` shines. 💡

---

## 🧠 Scenario: Matrix Normalization in Phases

Imagine you have a **large matrix**, and you want to process it in **parallel** across multiple threads — say, each thread handles one row.

But we want to do it in **phases**:

1. **Phase 1**: Each thread computes the **sum of its row**.
2. **Phase 2**: Each thread **normalizes** its row (divides each element by the sum).
3. Each phase should **only start after all threads complete the previous one**.

So we need **synchronization between phases** — that’s where `CyclicBarrier` fits perfectly.

---

## ✅ Code Example: Phased Matrix Normalization

```java
import java.util.concurrent.*;

public class MatrixComputation {
    static final int SIZE = 3;
    static final int[][] matrix = {
        {2, 4, 6},
        {1, 3, 5},
        {9, 7, 3}
    };

    static final double[][] normalized = new double[SIZE][SIZE];
    static final int[] rowSums = new int[SIZE];

    public static void main(String[] args) {
        CyclicBarrier barrier = new CyclicBarrier(SIZE, () -> {
            System.out.println("=== All threads reached barrier ===\n");
        });

        ExecutorService executor = Executors.newFixedThreadPool(SIZE);

        for (int i = 0; i < SIZE; i++) {
            final int row = i;
            executor.submit(() -> {
                try {
                    // Phase 1: compute row sum
                    int sum = 0;
                    for (int val : matrix[row]) {
                        sum += val;
                    }
                    rowSums[row] = sum;
                    System.out.println("Thread " + row + " computed sum: " + sum);

                    barrier.await(); // wait for all threads to finish phase 1

                    // Phase 2: normalize the row
                    for (int j = 0; j < SIZE; j++) {
                        normalized[row][j] = (double) matrix[row][j] / sum;
                    }
                    System.out.println("Thread " + row + " normalized row.");

                    barrier.await(); // wait again before printing final result

                } catch (Exception e) {
                    e.printStackTrace();
                }
            });
        }

        executor.shutdown();
        try {
            executor.awaitTermination(5, TimeUnit.SECONDS);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }

        System.out.println("\n=== Normalized Matrix ===");
        for (double[] row : normalized) {
            for (double val : row) {
                System.out.printf("%.2f ", val);
            }
            System.out.println();
        }
    }
}
```

---

## 🧩 What's Happening Here:

1. **Each thread processes one row**.
2. `barrier.await()` is used **twice**:
   - After computing the row sum.
   - After normalizing the row.
3. `CyclicBarrier` ensures **no thread moves to the next phase until all are done with the current one**.
4. Final matrix is printed only after all threads are done.

---

## 🌀 Why CyclicBarrier is Ideal Here

- It allows coordination across **multiple phases**.
- It **resets itself** automatically after each `await()` round.
- No need to manually manage counters or flags.
- Ideal for **multistep scientific or batch processing** tasks.

---
