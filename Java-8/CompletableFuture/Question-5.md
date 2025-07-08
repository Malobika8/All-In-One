Let's do a **real-world-style CompletableFuture challenge** that combines everything:

---

# ✅ **Challenge: User Profile Fetcher**

### 🔹 Scenario:

* You need to **fetch a user** by ID
* Then **fetch the user's settings** (language) — based on the user
* If **any step fails**, handle it gracefully with fallback
* Also, log the result regardless of success or failure

---

### 🧩 Requirements:

1. `fetchUserById(String id)` returns `CompletableFuture<User>`
2. `fetchSettingsForUser(User user)` returns `CompletableFuture<Settings>`
3. If **user fetch fails**, return `User("Guest")`
4. If **settings fetch fails**, return `Settings("Default Language")`
5. Use:

   * `.exceptionally` for user fallback
   * `.handle` for settings fallback and transformation
   * `.whenComplete` to log final outcome (user + settings)

---

### 👇 Starter Code Template (Fill It In):

```java
public class Main {
    public static void main(String[] args) {
        CompletableFuture<User> cfUser = fetchUserById("1")
            // TODO: handle error and return fallback user using exceptionally
            ;

        CompletableFuture<String> result = cfUser
            // TODO: thenCompose to fetch settings
            // TODO: handle settings failure with .handle and return "User <name> uses <language>"
            ;

        // TODO: log final outcome with whenComplete

        System.out.println("Final Output: " + result.join());
    }

    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            if (true) throw new RuntimeException("User not found");
            return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            if (true) throw new RuntimeException("Settings service unavailable");
            return new Settings("English");
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
}
```

---

### ✅ Expected Output:

```
User fetch failed: User not found
Settings fetch failed for user: Guest
Final log: User Guest uses Default Language
Final Output: User Guest uses Default Language
```

---

## Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> cfUser = fetchUserById("1")
                .exceptionally(ex -> {
                    System.out.println("User fetch failed: User not found");
                    return new User("Guest");
                });

        CompletableFuture<String> finalResult = cfUser.thenCompose(user -> {
                    return fetchSettingsForUser(user)
                            .handle((result, ex)->{
                                if(ex != null){
                                    System.out.println("Settings fetch failed for user: " + user.name());
                                    return new Settings("Default Language");
                                }
                                return result;
                            })
                            .thenApply(settings -> "User " + user.name() + " uses " + settings.language());
                })
                .whenComplete((result, ex) -> System.out.println("Final log: " + result));

        System.out.println("Final Output: " + finalResult.join());

    }

    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            if (true) throw new RuntimeException("User not found");
            return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            if (true) throw new RuntimeException("Settings service unavailable");
            return new Settings("English");
        });
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {
        }
    }

    record User(String name) {
    }

    record Settings(String language) {
    }
```

---

# ✅ Challenge: User + Settings + Notification

### 🔹 Scenario:

You're building a user dashboard service.

You need to:

1. **Fetch the user** by ID
2. **Fetch user settings** (language)
3. **Send a welcome notification** (async) — after both user and settings are ready
4. If anything fails, use **fallbacks**
5. Always **log the final message**

---

### 🧩 Requirements:

* `fetchUserById(String id)` → `CompletableFuture<User>`
  → If fails: return `User("Guest")` and log `"User fetch failed"`

* `fetchSettingsForUser(User user)` → `CompletableFuture<Settings>`
  → If fails: return `Settings("English")` and log `"Settings fetch failed for user: <name>"`

* `sendWelcomeNotification(User user, Settings settings)` → `CompletableFuture<Boolean>`
  → Simulate sending message.
  → If fails: log `"Notification failed for <name>"`, but continue gracefully with value `false`

* Construct final message:
  `"User <name> uses <language>. Notification sent: <true/false>"`

* Log the final message with `whenComplete`

---

### ✅ Method Stubs:

```java
static CompletableFuture<User> fetchUserById(String id) { ... }

static CompletableFuture<Settings> fetchSettingsForUser(User user) { ... }

static CompletableFuture<Boolean> sendWelcomeNotification(User user, Settings settings) { ... }
```

---

### 🧾 Expected Output (when all fail):

```
User fetch failed
Settings fetch failed for user: Guest
Notification failed for Guest
Final log: User Guest uses English. Notification sent: false
Final Output: User Guest uses English. Notification sent: false
```

---

### 🔧 Your Task:

Chain these:

1. Fetch user → `.exceptionally(...)`
2. thenCompose to fetch settings → `.handle(...)`
3. thenCompose to send notification → `.handle(...)`
4. thenApply to build final message
5. `.whenComplete(...)` to log
6. `.join()` and print

### Starter code template

```
import java.util.concurrent.CompletableFuture;

public class Main {
    public static void main(String[] args) {
        CompletableFuture<User> cfUser = fetchUserById("1")
            // TODO: .exceptionally(...) to return Guest and log error
            ;

        CompletableFuture<String> finalResult = cfUser.thenCompose(user -> 
            fetchSettingsForUser(user)
                // TODO: .handle(...) to fallback to default and log error
                .thenCompose(settings -> 
                    sendWelcomeNotification(user, settings)
                        // TODO: .handle(...) to fallback to false and log error
                        .thenApply(sent -> "User " + user.name() + " uses " + settings.language() +
                                ". Notification sent: " + sent)
                )
        ).whenComplete((result, ex) -> {
            // TODO: Final logging
        });

        System.out.println("Final Output: " + finalResult.join());
    }

    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("User service down");
            // return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("Settings unavailable");
            // return new Settings("Hindi");
        });
    }

    static CompletableFuture<Boolean> sendWelcomeNotification(User user, Settings settings) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("Notification system crashed");
            // return true;
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
}
```

---

## Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> cfUser = fetchUserById("1")
                .exceptionally(ex -> {
                    System.out.println("User fetch failed");
                    return new User("Guest");
                });

        CompletableFuture<String> result = cfUser.thenCompose(user -> {
            return fetchSettingsForUser(user)
                    .exceptionally(ex -> {
                        System.out.println("Settings fetch failed for user: " + user.name());
                        return new Settings("English");
                    })
                    .thenCompose(settings -> {
                        return sendWelcomeNotification(user, settings)
                                .exceptionally(ex -> {
                                    System.out.println("Notification failed for " + user.name());
                                    return false;
                                })
                                .thenApply(notification -> {
                                    return "User " + user.name() + " uses " + settings.language() +"" +
                                            ". Notification sent: " + notification.booleanValue();
                                });
                    });
        }).whenComplete((res, ex) -> {
            System.out.println("Final log: " + res);
        });

        System.out.println("Final Output: " + result.join());
    }

    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("User service down");
            // return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("Settings unavailable");
            // return new Settings("Hindi");
        });
    }

    static CompletableFuture<Boolean> sendWelcomeNotification(User user, Settings settings) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            throw new RuntimeException("Notification system crashed");
            // return true;
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
```

# ✅ Challenge: Fetch Product Info + Pricing + Reviews in Parallel

### 🔹 Scenario:

You are building a product detail page.

You need to fetch in **parallel**:

1. `getProductInfo(productId)` → product name & description
2. `getProductPricing(productId)` → price
3. `getProductReviews(productId)` → rating

---

### 🧩 Requirements:

1. Fetch all three in parallel
2. Use `CompletableFuture.allOf(...)` to wait for all
3. After all complete:

   * Combine results
   * Format the output:
     `"Product: <name> | Price: <price> | Rating: <rating>"`
4. Use `.join()` at the end
5. Simulate delays in all services (e.g. 1 second each)

---

### ✅ Method Stubs:

```java
static CompletableFuture<Product> getProductInfo(String productId)
static CompletableFuture<Pricing> getProductPricing(String productId)
static CompletableFuture<Review> getProductReviews(String productId)
```

---

### 🧾 Sample Output:

```
Product: UltraPen | Price: ₹499.0 | Rating: 4.5
```

---

### Starter code

```
static CompletableFuture<Product> getProductInfo(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Product("UltraPen", "A smooth writing experience.");
        });
    }

    static CompletableFuture<Pricing> getProductPricing(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Pricing(499.0);
        });
    }

    static CompletableFuture<Review> getProductReviews(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Review(4.5);
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record Product(String name, String description) {}
    record Pricing(double price) {}
    record Review(double rating) {}
```

## Solution

```
public static void main(String[] args) {
        CompletableFuture<Product> f1 = getProductInfo("1");
        CompletableFuture<Pricing> f2 = getProductPricing("1");
        CompletableFuture<Review> f3 = getProductReviews("1");

        CompletableFuture<Void> result = CompletableFuture.allOf(f1, f2, f3);
        CompletableFuture<String> string = result.thenApply(v -> {
            return "Name: " + f1.join().name() + " , Pricing: " + f2.join().price() + " , Rating: " + f3.join().rating();
        });

        System.out.println(string.join());
    }
    static CompletableFuture<Product> getProductInfo(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Product("UltraPen", "A smooth writing experience.");
        });
    }

    static CompletableFuture<Pricing> getProductPricing(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Pricing(499.0);
        });
    }

    static CompletableFuture<Review> getProductReviews(String productId) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Review(4.5);
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record Product(String name, String description) {}
    record Pricing(double price) {}
    record Review(double rating) {}
```

