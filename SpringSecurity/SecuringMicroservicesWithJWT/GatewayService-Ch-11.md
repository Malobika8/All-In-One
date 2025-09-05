<img width="957" height="590" alt="Screenshot 2025-09-05 at 11 40 11 AM" src="https://github.com/user-attachments/assets/bc99b12b-4d41-43d3-abd3-62face48c5e8" />
<img width="903" height="752" alt="Screenshot 2025-09-05 at 11 52 15 AM" src="https://github.com/user-attachments/assets/dd52a5db-7e9e-4188-8708-be03558940a3" />
<img width="974" height="346" alt="Screenshot 2025-09-05 at 11 40 30 AM" src="https://github.com/user-attachments/assets/7238b18f-e948-4e86-8728-48df1b53f452" />
<img width="855" height="604" alt="Screenshot 2025-09-05 at 11 40 49 AM" src="https://github.com/user-attachments/assets/4273b85d-1646-4508-913f-01780ab3746b" />

### ✅ What we need to implement next

1. **JWT Validation at Gateway** – so that only requests with valid JWT tokens pass through.

   * We’ll need a **Gateway filter** that intercepts requests.
   * It will validate the token (via secret key or by calling Auth Service).
   * If valid → forward the request. If invalid/expired → block.

2. **Filter requests based on roles** –

   * For example:

     * `ROLE_ADMIN` → can create/update products.
     * `ROLE_USER` → can place orders.
   * This will be enforced in **Product** and **Order** services using `@PreAuthorize` or Security config.

3. **Role-based Authorization in downstream services** –

   * Each microservice (Product/Order) must extract roles from JWT.
   * Then apply Spring Security method-level authorization.

There can be 2 implementations- **JWT validation at Gateway only** (centralized check) & **each service validating JWT**

* **Centralized (at Gateway only):**

  * Simpler, only Gateway validates.
  * Downstream services trust Gateway headers.

* **Distributed (Gateway + Each Service):**

  * More secure (services don’t blindly trust Gateway).
  * More work, but production-ready.

