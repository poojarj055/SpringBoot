**RESTful Web Services** provide a powerful way to build APIs by leveraging standard HTTP methods, status codes, and other web principles. Here’s a breakdown of the key concepts related to RESTful web services, focusing on HTTP methods, status codes, and Spring Boot annotations.

### HTTP Methods in RESTful Web Services
HTTP methods are used to perform operations on resources in a RESTful service. The most commonly used methods are:

1. **GET**:  
   - **Purpose**: Retrieve data from a server at the specified resource.
   - **Idempotent**: Yes. Making multiple identical requests should have the same effect as making a single request.
   - **Example**: `GET /users/1` might return details about the user with ID 1.

2. **POST**:  
   - **Purpose**: Submit data to the server to create a new resource.
   - **Idempotent**: No. Multiple identical requests can result in multiple resources being created.
   - **Example**: `POST /users` might create a new user.

3. **PUT**:  
   - **Purpose**: Update an existing resource with new data.
   - **Idempotent**: Yes. Multiple identical requests should update the resource in the same way.
   - **Example**: `PUT /users/1` might update the details of the user with ID 1.

4. **DELETE**:  
   - **Purpose**: Delete the resource at the specified URL.
   - **Idempotent**: Yes. Deleting a resource multiple times has the same effect as deleting it once.
   - **Example**: `DELETE /users/1` might delete the user with ID 1.

5. **PATCH**:  
   - **Purpose**: Apply partial modifications to a resource.
   - **Idempotent**: Yes. If you apply the same patch multiple times, the result will be the same as if you applied it once.
   - **Example**: `PATCH /users/1` might update only certain fields of the user with ID 1.

### HTTP Status Codes
HTTP status codes indicate the result of the HTTP request. They are divided into different classes:

1. **1xx Informational**:  
   - These are provisional responses that indicate the request was received and is being processed.
   - Example: `100 Continue`

2. **2xx Success**:  
   - Indicates that the request was successfully received, understood, and accepted.
   - Example: 
     - `200 OK`: Standard response for successful HTTP requests.
     - `201 Created`: The request has been fulfilled and a new resource has been created.
     - `204 No Content`: The request was successful, but there is no content to send in the response.

3. **3xx Redirection**:  
   - Indicates that further action needs to be taken by the client to complete the request.
   - Example:
     - `301 Moved Permanently`: The resource has been permanently moved to a new location.
     - `302 Found`: The resource is temporarily under a different URL.

4. **4xx Client Error**:  
   - Indicates that the request contains bad syntax or cannot be fulfilled.
   - Example:
     - `400 Bad Request`: The server cannot process the request due to client-side errors.
     - `401 Unauthorized`: The client must authenticate itself to get the requested response.
     - `403 Forbidden`: The server understands the request but refuses to authorize it.
     - `404 Not Found`: The server cannot find the requested resource.

5. **5xx Server Error**:  
   - Indicates that the server failed to fulfill a valid request.
   - Example:
     - `500 Internal Server Error`: A generic error message when the server encounters an unexpected condition.
     - `503 Service Unavailable`: The server is not ready to handle the request, usually due to maintenance or overload.

### Spring Boot Annotations for RESTful Services
Spring Boot simplifies the development of RESTful web services using annotations:

1. **@RestController**:  
   - Combines `@Controller` and `@ResponseBody` to simplify the creation of RESTful web services.
   - Example: 
     ```java
     @RestController
     public class UserController {
         // Controller methods here
     }
     ```

2. **@RequestMapping**:  
   - Used to map web requests to specific handler classes or methods.
   - Can specify HTTP methods using the `method` attribute.
   - Example:
     ```java
     @RequestMapping(value = "/users", method = RequestMethod.GET)
     public List<User> getAllUsers() {
         // Logic to return all users
     }
     ```

3. **@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping**:  
   - Specialized versions of `@RequestMapping` for specific HTTP methods, simplifying the syntax.
   - Example:
     ```java
     @GetMapping("/users/{id}")
     public User getUserById(@PathVariable int id) {
         // Logic to return a specific user by ID
     }
     ```

4. **@PathVariable**:  
   - Binds a method parameter to a URI template variable.
   - Example:
     ```java
     @GetMapping("/users/{id}")
     public User getUserById(@PathVariable int id) {
         // Logic to return a specific user by ID
     }
     ```

5. **@RequestParam**:  
   - Binds a method parameter to a query parameter in the request.
   - Example:
     ```java
     @GetMapping("/users")
     public List<User> getUsersByRole(@RequestParam String role) {
         // Logic to return users by role
     }
     ```

6. **@RequestBody**:  
   - Binds the body of the HTTP request to a method parameter.
   - Example:
     ```java
     @PostMapping("/users")
     public User createUser(@RequestBody User user) {
         // Logic to create a new user
     }
     ```

7. **@ResponseStatus**:  
   - Sets the HTTP status code for a response.
   - Example:
     ```java
     @PostMapping("/users")
     @ResponseStatus(HttpStatus.CREATED)
     public User createUser(@RequestBody User user) {
         // Logic to create a new user
     }
     ```

8. **@ExceptionHandler**:  
   - Used to handle exceptions thrown by request-handling methods.
   - Example:
     ```java
     @ExceptionHandler(UserNotFoundException.class)
     @ResponseStatus(HttpStatus.NOT_FOUND)
     public ErrorResponse handleUserNotFound(UserNotFoundException ex) {
         return new ErrorResponse("User not found");
     }
     ```

### Summary
- **HTTP Methods**: Specify actions like `GET`, `POST`, `PUT`, `DELETE`, and `PATCH`.
- **HTTP Status Codes**: Indicate the result of the HTTP request, ranging from `200 OK` to `500 Internal Server Error`.
- **Spring Boot Annotations**: Simplify RESTful service creation using annotations like `@RestController`, `@GetMapping`, `@PostMapping`, etc.

Together, these concepts enable you to create powerful and well-structured RESTful web services with Spring Boot.
