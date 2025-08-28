# CSRF (Cross-Site Request Forgery) in Spring Security

---

## 1. What is CSRF?

* **CSRF (Cross-Site Request Forgery)** is an attack where a malicious website tricks a logged-in user’s browser into sending unauthorized requests to another site where the user is authenticated.
* Example:

  * You’re logged into **bank.com** in one tab.
  * You visit **evil.com** in another tab.
  * Evil.com silently submits a request like `POST bank.com/transfer?amount=10000&to=evil`.
  * The browser automatically attaches your **JSESSIONID cookie** to `bank.com`.
  * Bank sees it as a legitimate request from you.

---

## 2. Why is JSESSIONID not enough?

* **JSESSIONID** is stored in a cookie and automatically included with every request to the domain (`bank.com`).
* Browser doesn’t care where the request originated (`bank.com` or `evil.com`).
* That means **authentication (session) is confirmed, but request intent is not**.
* Attackers exploit this by making *cross-site* requests.

---

## 3. Purpose of CSRF Protection

* To ensure that **the request originated from the legitimate site** (`bank.com`) and not from an attacker-controlled site (`evil.com`).
* This is achieved by requiring a **secret token** (CSRF token) in each state-changing request.

---

## 4. How CSRF Token Works

1. **Generated on server** when a session starts.
2. **Sent to client** as part of the page (e.g., hidden form field, meta tag, JavaScript variable).
3. **Must be included by the client** in each sensitive request (`POST`, `PUT`, `DELETE`).
4. **Server validates**:

   * Does the token match the one stored in session?
   * If yes → request accepted.
   * If missing or invalid → request rejected.

---

## 5. Why evil.com can’t use CSRF Token

* **Same-Origin Policy**: JavaScript running on `evil.com` cannot read responses, storage, or DOM of `bank.com`.
* Even though you (the user) can see CSRF token in Developer Tools, **evil.com cannot** because:

  * It cannot access the HTML or hidden fields of `bank.com`.
  * It cannot read cookies or local storage for `bank.com`.
* Therefore:

  * **JSESSIONID is auto-sent by browser** with every request to `bank.com`.
  * **CSRF token must be manually included** in request body/headers → only `bank.com` scripts can add it.
  * `evil.com` can’t fetch and attach it.

---

## 6. Flow Diagram

### Without CSRF Protection:

1. Browser sends request → `evil.com` triggers → browser includes `JSESSIONID`.
2. Bank sees request as authenticated.
3. Malicious request succeeds ❌.

### With CSRF Protection:

1. Request must contain CSRF token.
2. Browser auto-sends `JSESSIONID`, but **CSRF token is missing** if triggered from `evil.com`.
3. Bank rejects request ✅.

---

## 7. CSRF in Spring Security

* Spring Security enables CSRF protection **by default** for web apps that use sessions and forms.
* Token is stored in `HttpSession` and also exposed in HTML forms or meta tags.
* Spring validates token for **state-changing HTTP methods**:

  * `POST`, `PUT`, `DELETE`, `PATCH`.
  * Not required for `GET`, `HEAD`, `OPTIONS` (safe methods).

---

## 8. Modern Alternative: SameSite Cookies

* Modern browsers support **`SameSite` cookie attribute**:

  * `Strict` → cookie sent only if request originates from the same site.
  * `Lax` → cookie sent for top-level navigation but not for background requests (protects against most CSRF).
  * `None` → cookie always sent (old behavior, needs `Secure` flag).
* With `SameSite=Lax` or `Strict`, CSRF risk is reduced.
* Some apps disable CSRF tokens if they rely on `SameSite` cookies — but **tokens are still considered more reliable**, especially for legacy browsers.

---

## 9. Summary

* **JSESSIONID alone is not safe** because browser auto-sends it from any site.
* **CSRF token ensures intent** — proves the request really came from the legitimate site.
* **evil.com cannot read or include CSRF token** due to Same-Origin Policy.
* **Spring Security** automatically provides CSRF protection by generating and validating tokens.
* **SameSite cookies** are a modern browser-level defense, but CSRF tokens remain the most robust solution.

---

👉 One-liner to remember:
**Authentication proves *who* you are (JSESSIONID).
CSRF token proves *where the request came from*.**

---

