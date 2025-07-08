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
