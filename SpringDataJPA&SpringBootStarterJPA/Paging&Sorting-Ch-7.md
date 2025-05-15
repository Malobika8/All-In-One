### **1. What is Paging?**

Paging is a way to break large amounts of data into smaller chunks, called pages. This allows you to:
- **Limit the amount of data fetched** in a single request.
- **Improve performance** when handling large datasets.
- Make the system more **responsive** by sending data in parts.

#### Example:
Let’s say you have 100 course materials and want to show 10 per page. You would request the first page (which contains course materials 1-10), then the second page (containing 11-20), and so on.

---

### **2. What is Sorting?**

Sorting arranges data in a specific order. It can either be:
- **Ascending** (smallest to largest, alphabetically A-Z, etc.)
- **Descending** (largest to smallest, alphabetically Z-A, etc.)

#### Example:
You may want to fetch course materials and sort them by the `url` field in ascending order.

---

### **3. Spring Data JPA - `Pageable` and `Sort`**

- **`Pageable`** is an interface in Spring Data that represents a request for a specific page of data. It contains:
  - **Page number**: Which page you want (0-based index, meaning 0 = first page).
  - **Page size**: How many items you want per page.

- **`Sort`** is a class that defines how the data should be ordered (ascending or descending) based on a specific field.

---

### **4. How Does Paging and Sorting Work in Spring Data JPA?**

Spring provides `JpaRepository` that already includes support for paging and sorting. You don’t need to write extra code for these basic features.

#### Example: Repository

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface CourseMaterialRepository extends JpaRepository<CourseMaterial, Long> {
}
```

`JpaRepository` extends `PagingAndSortingRepository`, which already includes methods like:
- `findAll(Pageable pageable)` — to fetch a page of results.
- `findAll(Sort sort)` — to fetch all results sorted by a specific field.

---

### **5. How to Use Pageable and Sort in Service Layer**

#### Example: Paging Service

We use `PageRequest.of(pageNumber, pageSize)` to create a `Pageable` object. `PageRequest` is a simple implementation of the `Pageable` interface.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.stereotype.Service;

@Service
public class CourseMaterialService {

    @Autowired
    private CourseMaterialRepository courseMaterialRepository;

    public Page<CourseMaterial> getPagedCourseMaterials(int page, int size) {
        // PageRequest.of(page, size) creates a Pageable object (page is 0-based index)
        PageRequest pageable = PageRequest.of(page, size);
        return courseMaterialRepository.findAll(pageable);
    }
}
```

- `PageRequest.of(page, size)` creates a `Pageable` object.
  - `page` is the page number (starts from 0).
  - `size` is how many items per page.

#### Example: Sorting Service

You can use `Sort.by(field).ascending()` or `Sort.by(field).descending()` to specify how to sort data.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Sort;
import org.springframework.stereotype.Service;

@Service
public class CourseMaterialService {

    @Autowired
    private CourseMaterialRepository courseMaterialRepository;

    public List<CourseMaterial> getSortedCourseMaterials(String sortBy, boolean isAscending) {
        // Sort by the given field (e.g., "url") in ascending or descending order
        Sort sort = isAscending ? Sort.by(sortBy).ascending() : Sort.by(sortBy).descending();
        return courseMaterialRepository.findAll(sort);
    }
}
```

---

### **6. Combining Paging and Sorting**

You can combine both `Pageable` and `Sort` to fetch sorted data with paging. Here’s how:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Sort;
import org.springframework.stereotype.Service;

@Service
public class CourseMaterialService {

    @Autowired
    private CourseMaterialRepository courseMaterialRepository;

    public Page<CourseMaterial> getPagedAndSortedCourseMaterials(int page, int size, String sortBy, boolean isAscending) {
        // Create sorting object (ascending or descending)
        Sort sort = isAscending ? Sort.by(sortBy).ascending() : Sort.by(sortBy).descending();
        
        // Create Pageable object (page, size, and sorting)
        PageRequest pageable = PageRequest.of(page, size, sort);
        
        // Fetch data with pagination and sorting
        return courseMaterialRepository.findAll(pageable);
    }
}
```

#### Breakdown:
- `PageRequest.of(page, size, sort)` combines pagination and sorting into one request.
- `findAll(pageable)` returns a `Page` object with the requested page, sorted by the specified field.

---

### **7. Exposing Paging and Sorting via REST API**

You can expose paging and sorting functionality via a REST API.

#### Example: Controller

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Page;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CourseMaterialController {

    @Autowired
    private CourseMaterialService courseMaterialService;

    @GetMapping("/course-materials")
    public Page<CourseMaterial> getCourseMaterials(
            @RequestParam(defaultValue = "0") int page,       // Default to the first page
            @RequestParam(defaultValue = "5") int size,      // Default 5 items per page
            @RequestParam(defaultValue = "url") String sortBy, // Default sort by `url`
            @RequestParam(defaultValue = "true") boolean isAscending) { // Default sort ascending
        return courseMaterialService.getPagedAndSortedCourseMaterials(page, size, sortBy, isAscending);
    }
}
```

- `@RequestParam(defaultValue = "0")` sets default values for the parameters in case the user doesn’t provide them in the request.

#### Example API Request:
```
GET /course-materials?page=0&size=5&sortBy=courseMaterialId&isAscending=false
```

This will fetch the first 5 course materials, sorted by `courseMaterialId` in descending order.

---

### **8. What is `Page` and How to Use It?**

`Page<T>` is an interface provided by Spring Data JPA that represents a **single page** of results. It contains not just the data but also useful information like:
- **Total number of pages**
- **Total number of elements**
- **Current page number**
- **Size of the page**

#### Example of a `Page` response:
```json
{
  "content": [
    { "courseMaterialId": 5, "url": "http://example5.com" },
    { "courseMaterialId": 4, "url": "http://example4.com" }
  ],
  "totalPages": 10,
  "totalElements": 50,
  "size": 5,
  "number": 0,
  "first": true,
  "last": false
}
```

- **`content`**: List of the current page’s data.
- **`totalPages`**: Total number of pages available.
- **`totalElements`**: Total number of items available.
- **`size`**: Number of items per page.
- **`number`**: Current page number.

---

### **9. Final Recap**

1. **Paging** is used to split large datasets into smaller, manageable chunks.
2. **Sorting** arranges data in a specified order (ascending or descending).
3. **`Pageable`** is used to represent a page request (with page number and page size).
4. **`Sort`** defines the sorting behavior for a query.
5. **`Page<T>`** is the result object containing the data of a specific page and useful metadata (like total pages).

