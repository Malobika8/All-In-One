In Hibernate, an **Embeddable** is a concept that allows you to define reusable and composable components or value objects as part of your entity model. These embeddable objects are not entities themselves but are treated as part of the owning entity, meaning they don't have their own identity or lifecycle.

The **@Embeddable** annotation in Hibernate is used to mark a class whose instances can be embedded into an entity. The fields of the embeddable object are mapped to the same database table as the owning entity.

---

### **Key Points About @Embeddable**
1. **Reusability**:
   - You can define common reusable components, such as `Address`, `Name`, or `AuditInfo`, and embed them in multiple entities.
   
2. **Part of the Owning Entity**:
   - The lifecycle of the embeddable is tied to the owning entity. It doesn't have its own identity (e.g., no primary key).

3. **Database Mapping**:
   - The properties of the embeddable object are persisted as columns in the table of the owning entity.

4. **Simplifies Design**:
   - Allows better modularization and encapsulation of related fields.

---

### **Example: Using @Embeddable**

#### **1. Define an Embeddable Class**
```java
import jakarta.persistence.Embeddable;

@Embeddable
public class Address {
    private String street;
    private String city;
    private String state;
    private String zipCode;

    // Getters and setters
    public String getStreet() {
        return street;
    }

    public void setStreet(String street) {
        this.street = street;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    public String getZipCode() {
        return zipCode;
    }

    public void setZipCode(String zipCode) {
        this.zipCode = zipCode;
    }
}
```

#### **2. Use the Embeddable in an Entity**
```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Embedded;

@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @Embedded
    private Address address; // Embedding the Address class

    // Getters and setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }
}
```

#### **3. Database Table**
For the `Employee` entity, Hibernate would generate a table like:

| ID  | NAME    | STREET       | CITY      | STATE     | ZIPCODE   |
|------|---------|--------------|-----------|-----------|-----------|
| 1    | John Doe | 123 Elm St  | New York  | NY        | 10001     |

Here, the columns `STREET`, `CITY`, `STATE`, and `ZIPCODE` come from the `Address` embeddable.

---

### **Customizing Column Names**

You can customize the column names of the embeddable fields in the owning entity's table using the `@AttributeOverrides` and `@AttributeOverride` annotations.

```java
import jakarta.persistence.*;

@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @Embedded
    @AttributeOverrides({
        @AttributeOverride(name = "street", column = @Column(name = "HOME_STREET")),
        @AttributeOverride(name = "city", column = @Column(name = "HOME_CITY")),
        @AttributeOverride(name = "state", column = @Column(name = "HOME_STATE")),
        @AttributeOverride(name = "zipCode", column = @Column(name = "HOME_ZIP"))
    })
    private Address homeAddress;

    // Getters and setters
}
```

In this case, the table would have columns like `HOME_STREET`, `HOME_CITY`, `HOME_STATE`, and `HOME_ZIP`.

---

### **When to Use Embeddables**
1. **Shared Attributes**:
   - Common fields like `createdBy`, `createdDate`, etc., can be encapsulated into an embeddable class.

2. **Value Objects**:
   - Represent domain concepts without identity (e.g., `Address`, `Name`).

3. **Logical Grouping**:
   - Group related fields into a single reusable object for clarity and maintainability.

---

### **Lifecycle and Limitations**
- The embeddable class does not have its own lifecycle; it is persisted, updated, or deleted along with the owning entity.
- It cannot have relationships (e.g., `@OneToMany`) or an `@Id`.

---

### **Conclusion**
The `@Embeddable` annotation in Hibernate is a useful feature for structuring your application model, improving code reusability, and simplifying entity design. It works well when you want to encapsulate a group of related fields as a reusable component of your entities.

# At a glance

<img width="1131" alt="Screenshot 2025-01-21 at 6 02 02 PM" src="https://github.com/user-attachments/assets/cdde5c25-c512-4d01-ba39-e10da8487f34" />
<img width="951" alt="Screenshot 2025-01-21 at 6 09 36 PM" src="https://github.com/user-attachments/assets/71963247-c61a-45c0-a8ab-7a2e188aa2d9" />
<img width="828" alt="Screenshot 2025-01-21 at 6 10 44 PM" src="https://github.com/user-attachments/assets/58584b7b-1547-4427-bf5a-1ea5e49acef9" />
<img width="790" alt="Screenshot 2025-01-21 at 6 10 22 PM" src="https://github.com/user-attachments/assets/738e12a7-7f36-4ff6-a306-c2ef32a589a1" />
