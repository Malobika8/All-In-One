```
   ┌───────────────────┐
   │   Client Browser   │
   └─────────┬─────────┘
             │  HTTP Request
             ▼
   ┌─────────────────────────┐
   │   DispatcherServlet     │
   └─────────┬───────────────┘
             │
     1️⃣ Find handler
             │
             ▼
   ┌─────────────────────────┐
   │     HandlerMapping      │  ← (Matches URL + HTTP Method)
   └─────────┬───────────────┘
             │  Handler Object + Method
             ▼
   ┌─────────────────────────┐
   │     HandlerAdapter      │  ← (Invokes the handler method)
   └─────────┬───────────────┘
             │  ModelAndView
             ▼
   ┌─────────────────────────┐
   │     ViewResolver        │
   └─────────┬───────────────┘
             │  View Object
             ▼
   ┌─────────────────────────┐
   │        View              │
   └─────────┬───────────────┘
             │ Render (HTML/JSON/XML)
             ▼
   ┌───────────────────┐
   │   Client Browser   │
   └───────────────────┘

```

- HandlerMapping → Decides which controller method should handle the request.
- HandlerAdapter → Actually invokes that method, handling method parameters, return types, etc.

🔍 **HandlerAdapter’s role** in Spring MVC:

* **It doesn’t decide the mapping** — that’s `HandlerMapping`’s job.
* It **invokes** the mapped handler method (controller method) after `HandlerMapping` finds it.
* It works with **argument resolvers** to ensure method parameters are populated correctly (e.g., `@RequestParam`, `@PathVariable`, `@RequestBody`), converting request data into the method’s parameter types.
* It works with **return value handlers** to handle the method’s return (e.g., converting it into JSON, resolving a view name, etc.).
* It basically ensures: *“I’ve got the correct method, I’ll set up the parameters, call it, and handle the result properly.”*

Think of it as the **bridge** between the raw `HttpServletRequest/Response` and the controller method you wrote.

