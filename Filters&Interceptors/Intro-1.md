# Introduction
In Spring Boot applications, handling HTTP requests often requires more than just business logic. You might need to log incoming requests, validate headers, enforce security policies, or modify responses globally. This is where filters and interceptors come into play. While both are used to process HTTP requests and responses, they operate at different layers of the application and serve distinct purposes. In this blog, we’ll explore how to use filters and interceptors effectively, complete with code examples and real-world use cases.

## 1. What Are Filters?
Filters are part of the Servlet API and operate at the web layer, intercepting requests before they reach the controller and responses after they leave the controller. They are ideal for tasks that need to be applied globally, such as:

- Logging requests/responses.
- Authentication/authorization.
- Request/response modification (e.g., adding headers).
- Compression/encryption.

### Example: Creating a Custom Filter

```
@Component
@Order(1) // Defines execution order for multiple filters
public class LoggingFilter implements Filter {

    @Override
    public void doFilter(
        ServletRequest request, 
        ServletResponse response, 
        FilterChain chain
    ) throws IOException, ServletException {
        
        HttpServletRequest httpRequest = (HttpServletRequest) request;
        System.out.println("Request received for: " + httpRequest.getRequestURI());
        
        // Pass request to the next filter or controller
        chain.doFilter(request, response);
        
        HttpServletResponse httpResponse = (HttpServletResponse) response;
        System.out.println("Response status: " + httpResponse.getStatus());
    }
}
```

## 2. What Are Interceptors?

Interceptors are part of Spring’s MVC framework and operate at the controller layer. They allow you to execute logic:

- Before a request is handled by a controller (preHandle).
- After the controller processes the request but before the view is rendered (postHandle).
- After the request is fully completed (afterCompletion).

Interceptors are perfect for:

- Adding/modifying model attributes.
- Measuring request processing time.
- Validating session data.
- Applying controller-specific logic.

### Example: Creating a Custom Interceptor

```
@Component
public class AuthInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(
        HttpServletRequest request, 
        HttpServletResponse response, 
        Object handler
    ) throws Exception {
        
        String authHeader = request.getHeader("Authorization");
        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            response.sendError(HttpStatus.UNAUTHORIZED.value(), "Missing token");
            return false; // Block the request
        }
        return true; // Proceed to controller
    }

    @Override
    public void postHandle(
        HttpServletRequest request, 
        HttpServletResponse response, 
        Object handler, 
        ModelAndView modelAndView
    ) throws Exception {
        // Add a timestamp to the model
        modelAndView.addObject("timestamp", System.currentTimeMillis());
    }
}
```

### Registering the Interceptor (in a @Configuration class):

```
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Autowired
    private AuthInterceptor authInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(authInterceptor)
                .addPathPatterns("/api/**"); // Apply to specific endpoints
    }
}
```

## 3. Key Differences: Filters vs. Interceptors

<img width="839" height="252" alt="Screenshot 2026-03-25 at 9 09 29 PM" src="https://github.com/user-attachments/assets/b588d0da-4efa-4463-99bd-55dfc65ddc9a" />

## 4. When to Use Which?

### Use Filters for:

- Cross-cutting concerns (e.g., logging, CORS).
- Tasks that need to run before Spring MVC processes the request.

### Use Interceptors for:

- Logic tied to the controller lifecycle (e.g., modifying model attributes).
- Validating session/authentication data specific to endpoints.
  
## 5. Real-World Use Cases
### - Rate Limiting with Filters: Track request counts per IP address and block excessive requests.
### - Performance Metrics with Interceptors: Measure how long a controller takes to process a request using preHandle and postHandle.
### - Request/Response Modification:
  * Encrypt sensitive data in responses using a filter.
  * Add custom headers to responses via an interceptor.

## 6. Best Practices
- Keep It Lightweight: Avoid heavy processing in filters/interceptors to minimize latency.
- Leverage Ordering: Use @Order for filters to control execution sequence.
- Test Thoroughly: Mock requests/responses to ensure your logic behaves as expected.

# Conclusion
Filters and interceptors are powerful tools for controlling request/response processing in Spring Boot applications. By understanding their differences and use cases, you can design cleaner, more maintainable code. Whether you’re logging requests, enforcing security, or adding custom headers, these components will help you keep your application robust and efficient.
