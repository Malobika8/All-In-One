## 🔍 What is `<context:annotation-config />`?

`<context:annotation-config />` is used **only to enable annotation-based dependency injection** in Spring — things like:

* `@Autowired`
* `@PostConstruct`
* `@PreDestroy`
* `@Resource`
* `@Inject`

But it **does not** automatically scan your packages to find classes annotated with `@Component`, `@Service`, `@Repository`, or `@Controller`.

---

## ✅ When to use `<context:annotation-config />`

You use it **when:**

1. You are defining your beans manually in `beans.xml` (i.e., using `<bean>` tags)
2. But you still want to use annotations **inside those bean classes** — like `@Autowired`, `@PostConstruct`, etc.

---

### ✅ Example

```xml
<!-- beans.xml -->
<beans ...>
    <context:annotation-config />

    <!-- Manually defined beans -->
    <bean id="myService" class="com.example.MyService" />
    <bean id="myRepo" class="com.example.MyRepo" />
</beans>
```

```java
public class MyService {
    @Autowired
    private MyRepo myRepo;
}
```

Here, `@Autowired` works **only because** you have `<context:annotation-config />`.

---

## ❌ What it does NOT do:

It does **NOT** scan packages to find classes annotated with `@Component`, `@Service`, etc.

For that, you need:

```xml
<context:component-scan base-package="com.example" />
```

This not only enables annotation-based DI (like `annotation-config`), but **also automatically registers** all classes annotated with Spring stereotypes (`@Component`, `@Service`, etc.).

---

## 🔁 Summary: annotation-config vs component-scan

| Tag                                            | What it does                                                                          | What it doesn’t do           |
| ---------------------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------- |
| `<context:annotation-config />`                | Enables support for `@Autowired`, `@PostConstruct`, etc.                              | Does not scan for components |
| `<context:component-scan base-package="..."/>` | Enables all of the above **AND** scans the package for `@Component`, `@Service`, etc. | —                            |

---

### ✅ Best Practice Today

Use:

```xml
<context:component-scan base-package="com.example" />
```

And you **don’t need `<context:annotation-config />` separately** — `component-scan` already includes that functionality.

---

