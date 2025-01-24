<img width="1131" alt="Screenshot 2025-01-23 at 6 54 33 PM" src="https://github.com/user-attachments/assets/e767f78e-4ac8-40f3-9ea4-7679df00b1f4" />

### Here are the main options for setting up Hibernate in a Spring environment:

1. **Using `LocalSessionFactoryBean`:**  
   - A Spring-provided factory bean to configure and bootstrap Hibernate's `SessionFactory`.  
   - Recommended for direct Hibernate usage when not relying on JPA.  

2. **Using `HibernateJpaVendorAdapter` with `LocalContainerEntityManagerFactoryBean`:**  (SPRING ORM WITH JPA)
   - Combines JPA with Hibernate as the JPA provider.  
   - This is the most common approach when using Spring Data JPA or integrating Hibernate via JPA.

3. **Obtaining a `SessionFactory` from JNDI:**  
   - Suitable for enterprise setups where the application server manages the `SessionFactory`.  
   - Requires JNDI lookups for Hibernate configuration.
