# Use the token for authorization

1. **Login** → Get token from `/login`.
2. **Send token in request headers** for protected endpoints:

   ```
   Authorization: Bearer <your-token>
   ```
3. Create a **JWT filter** that:

   * Extracts token from the `Authorization` header.
   * Validates token using `JwtUtil`.
   * Loads user details and sets `SecurityContextHolder`.

That way, our app is fully stateless — no session needed, everything is handled with JWT.

---

# Let’s build the **JWT filter** step by step.

### 1. Create a JWT Authentication Filter

This filter will intercept every request, extract the token from the `Authorization` header, validate it, and set the `SecurityContext`.

```java
package com.spring.security.filter;

import com.spring.security.service.CustomUserDetailsManager;
import com.spring.security.util.JwtUtil;
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Autowired
    JwtUtil jwtUtil;

    @Autowired
    CustomUserDetailsManager customUserDetailsManager;

    @Autowired
    AuthenticationManager authenticationManager;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String authHeader = request.getHeader("Authorization");
        String token = null;
        String username = null;

        //Extract token from header
        if(authHeader!=null && authHeader.startsWith("Bearer")){
            token = authHeader.substring(7).trim();
            username = jwtUtil.extractUsername(token);
        }

        //Validate and set authentication
        if(username!=null && SecurityContextHolder.getContext().getAuthentication()==null){
            UserDetails userDetails = customUserDetailsManager.loadUserByUsername(username);

            if(jwtUtil.validateToken(token, userDetails)){
                UsernamePasswordAuthenticationToken upaToken = new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
                upaToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(upaToken);
            }
        }

        filterChain.doFilter(request, response);
    }
}

```

---

### 2. Register the Filter in Security Configuration

In your `SecurityConfig` class, add this filter **before** the `UsernamePasswordAuthenticationFilter`.

```java
package com.spring.security.config;

import com.spring.security.filter.JwtAuthenticationFilter;
import com.spring.security.service.CustomUserDetailsManager;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.AuthenticationProvider;
import org.springframework.security.authentication.ProviderManager;
import org.springframework.security.authentication.dao.DaoAuthenticationProvider;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

import javax.sql.DataSource;

@Configuration
@ComponentScan(basePackages = "com")
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    CustomUserDetailsManager customUserDetailsManager;

    @Autowired
    JwtAuthenticationFilter jwtAuthenticationFilter;

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity httpSecurity) throws Exception {

        httpSecurity.csrf(csrf -> csrf.disable());
        httpSecurity.authorizeHttpRequests(customizer->customizer
                .requestMatchers("/WEB-INF/views/**", "/register", "/processRegister", "/login")
                .permitAll()
                .anyRequest()
                .authenticated());

        //httpSecurity.formLogin(Customizer.withDefaults());
        httpSecurity.httpBasic(Customizer.withDefaults());

        httpSecurity.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);

        return httpSecurity.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder(12);
    }

    @Bean
    public AuthenticationProvider authenticationProvider(PasswordEncoder passwordEncoder){
        DaoAuthenticationProvider authenticationProvider = new DaoAuthenticationProvider(passwordEncoder);
        authenticationProvider.setUserDetailsService(customUserDetailsManager);
        return authenticationProvider;
    }

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationProvider authenticationProvider){
        return new ProviderManager(authenticationProvider);
    }
}

```

---

### 3. Test the Flow

1. **POST** `/login` with username/password → get JWT.
2. **Call any protected endpoint** with header:

   ```
   Authorization: Bearer <token>
   ```

   If token is valid, request will succeed.

---


