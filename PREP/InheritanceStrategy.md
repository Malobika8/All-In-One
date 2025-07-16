## ✅ Step 12: Inheritance Strategies in JPA

### 🔹 Why Inheritance Mapping?

In real apps, you may have:

```java
@Entity
class Vehicle { }

@Entity
class Car extends Vehicle { }

@Entity
class Bike extends Vehicle { }
```

We need a way to **map inheritance hierarchies to relational tables.**
JPA gives us 3 strategies.

## ✅ The 3 Inheritance Strategies

### 1. `SINGLE_TABLE` (Default)

* All classes (super + subclasses) go into **one table**
* One column holds a **discriminator** to identify subclass

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "type")
class Vehicle { }

@Entity
@DiscriminatorValue("CAR")
class Car extends Vehicle { }

@Entity
@DiscriminatorValue("BIKE")
class Bike extends Vehicle { }
```

| id | type | commonField | carField | bikeField |
| -- | ---- | ----------- | -------- | --------- |

✅ ✅ Fastest
❌ Nulls in unused subclass columns

### 2. `JOINED` (Normalized, Relational Style)

* Superclass fields → one table
* Subclass fields → separate tables, joined by FK

```java
@Entity
@Inheritance(strategy = InheritanceType.JOINED)
class Vehicle { }

@Entity
class Car extends Vehicle { }
```

| vehicle  | car        |
| -------- | ---------- |
| id, name | id, engine |

✅ ✅ Normalized schema
❌ Needs JOIN queries (slower)

### 3. `TABLE_PER_CLASS` (One Table per Class)

* Each subclass has its **own table**, including superclass fields

```java
@Entity
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
class Vehicle { }

@Entity
class Car extends Vehicle { }
```

\| car (id, name, engine) | bike (id, name, cc) |

✅ Independent subclass tables
❌ No shared primary key space
❌ UNION queries needed

#### ✅ When to Use What?

| Use Case                                | Best Strategy     |
| --------------------------------------- | ----------------- |
| Performance + Simplicity                | `SINGLE_TABLE`    |
| Clean DB schema                         | `JOINED`          |
| Subclasses unrelated, stored separately | `TABLE_PER_CLASS` |

---

# You have `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)` and store both `Car` and `Bike`. How does JPA know which subclass each row belongs to?

### Sol:

In the SINGLE_TABLE strategy, all data for super and subclasses goes into one table.
We use a @DiscriminatorColumn to store a special column (e.g., type) that tells JPA which subclass a row belongs to.
Each subclass can optionally define its own @DiscriminatorValue.

```
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "vehicle_type")
class Vehicle { }

@Entity
@DiscriminatorValue("CAR")
class Car extends Vehicle { }

@Entity
@DiscriminatorValue("BIKE")
class Bike extends Vehicle { }
```

- A row with vehicle_type = 'CAR' will be loaded as a Car instance
- 'BIKE' will be loaded as a Bike


