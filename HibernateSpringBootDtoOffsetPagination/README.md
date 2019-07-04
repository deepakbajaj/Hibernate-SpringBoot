**[How To Implement Offset Pagination in Spring Boot](https://github.com/AnghelLeonard/Hibernate-SpringBoot/tree/master/HibernateSpringBootOffsetPagination)**

**Description:** When we rely on an *offset* paging we have the performance penalty induced by throwing away *n* records before reached the desired *offset*. Larger *n* leads to a significant performance penalty. Another penalty is the extra-`SELECT` needed to count the total number of records. But, for small datasets, *offset* and *keysey* provides almost the same performances. Spring Boot provides built-in support for *offset* pagination via the `Page` API, therefore it is very easy to use it in an application.

**Important note:** This application extracts records as entities, but if all you want to do is to read this data in pages then consider DTOs to avoid consuming memory and CPU for nothing. As a rule, extract entites only if you plan to modify them. In this case, we need a native SQL or another approach instead of `Page<T>`.

**But:** If *offset* pagination is causing you performance issues then please check recipes: [here](https://github.com/AnghelLeonard/Hibernate-SpringBoot/tree/master/HibernateSpringBootSliceAllCriteriaBuilderSortAndSpecificationAndQueryHints) (slice technique for find all records), [here](https://github.com/AnghelLeonard/Hibernate-SpringBoot/tree/master/HibernateSpringBootWindowFunctionPaging) (*offset* with window functions) and [here](https://github.com/AnghelLeonard/Hibernate-SpringBoot/tree/master/HibernateSpringBootKeysetPagination) (*keyset* pagination).

**Key points:**\
     - write a repository that extends `PagingAndSortingRepository`\
     - call or write methods that returns `Page`

**Examples:**\
     - call the built-in `findAll(Pageable)` without sorting:\
     `repository.findAll(PageRequest.of(page, size));`\
     - call the built-in `findAll(Pageable)` with sorting:\
     `repository.findAll(PageRequest.of(page, size, new Sort(Sort.Direction.ASC, "name")));`\
     - use Spring Data query creation to define new methods in your repository:\
     `Page<Author> findByName(String name, Pageable pageable);`\
     `Page<Author> queryFirst10ByName(String name, Pageable pageable);`

-------------------------------

**You may like to try as well:**
<a href="https://leanpub.com/java-persistence-performance-illustrated-guide"><p align="center"><img src="https://github.com/AnghelLeonard/Hibernate-SpringBoot/blob/master/Java%20Persistence%20Performance%20Illustrated%20Guide.jpg" height="410" width="350"/></p></a>