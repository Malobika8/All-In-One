

## 🔤 Common keywords we can use

| Keyword                                            | Meaning                 |
| -------------------------------------------------- | ----------------------- |
| `findBy...`                                        | Start of a query method |
| `And`, `Or`                                        | Combine conditions      |
| `GreaterThan`, `LessThan`, `Between`               | Range conditions        |
| `Like`, `StartingWith`, `EndingWith`, `Containing` | Pattern matching        |
| `In`, `NotIn`                                      | For collections         |
| `IsNull`, `IsNotNull`                              | Null checks             |
| `OrderBy`                                          | Sorting                 |
| `Top`, `First`                                     | Limit result            |

## Spring Data JPA Repository Hierarchy - Spring Data JPA gives us interfaces with increasing capabilities:

Repository (marker)
   └── CrudRepository
         └── PagingAndSortingRepository
               └── JpaRepository
