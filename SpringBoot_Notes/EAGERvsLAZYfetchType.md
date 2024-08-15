In JPA (Java Persistence API), `FetchType` is used to define the strategy for fetching related entities from the database when a parent entity is retrieved. There are two primary fetching strategies:

### 1. **FetchType.EAGER**
   - **Immediate Loading:** With `FetchType.EAGER`, when you retrieve an entity, all related entities are loaded immediately, regardless of whether you access them in your code or not.
   - **Example:** If you have an entity `PropertyEntity` with a related `UserEntity` using `FetchType.EAGER`, both the `PropertyEntity` and `UserEntity` will be fetched from the database as soon as you query for `PropertyEntity`.
   - **Pros:**
     - Simplifies access to related data since all related entities are loaded upfront.
   - **Cons:**
     - **Performance Impact:** If the related entity contains a lot of data or if there are multiple related entities, fetching all of them eagerly can result in unnecessary overhead, slowing down the initial query.
     - **Over-fetching:** You might end up fetching data that you don't actually need.

   - **Usage Example:**

     ```java
     @ManyToOne(fetch = FetchType.EAGER)
     @JoinColumn(name = "USER_ID")
     private UserEntity userEntity;
     ```

     When you load a `PropertyEntity`, the associated `UserEntity` will be loaded immediately.

### 2. **FetchType.LAZY**
   - **On-Demand Loading:** With `FetchType.LAZY`, the related entities are not loaded immediately when you retrieve the parent entity. Instead, they are loaded on demand, i.e., when you actually access them in your code.
   - **Example:** If you have an entity `PropertyEntity` with a related `UserEntity` using `FetchType.LAZY`, the `UserEntity` will only be fetched from the database when you try to access it from the `PropertyEntity`.
   - **Pros:**
     - **Performance Optimization:** Only the data you actually need is loaded, which can reduce memory usage and improve performance, especially when dealing with large datasets.
     - **Avoids Over-fetching:** Related entities are only loaded when accessed, so unnecessary data fetching is minimized.
   - **Cons:**
     - **Potential for LazyInitializationException:** If the session is closed before the related entity is accessed, and you try to access it later, you'll encounter a `LazyInitializationException`. This often happens in environments like Spring where sessions are short-lived.
     - **Complexity:** Managing when the related data is loaded can be more complex, especially in cases where you need the data but are outside of a session context.

   - **Usage Example:**

     ```java
     @ManyToOne(fetch = FetchType.LAZY)
     @JoinColumn(name = "USER_ID")
     private UserEntity userEntity;
     ```

     The `UserEntity` will only be loaded when you explicitly access it from the `PropertyEntity`.

### Summary
- **`FetchType.EAGER`:** Loads related entities immediately. Good for scenarios where you always need the related data. Can impact performance negatively if the related data is large or complex.
- **`FetchType.LAZY`:** Loads related entities on demand. Good for optimizing performance and memory usage, but can cause issues like `LazyInitializationException` if not managed properly.

Choosing between `EAGER` and `LAZY` depends on your application's specific requirements, data access patterns, and performance considerations.
