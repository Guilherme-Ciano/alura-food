# Alura Food - Payments Microservice

This project is a payments microservice developed as part of the Alura Food application. It demonstrates the implementation of a robust, scalable, and resilient microservice architecture using Java and the Spring Framework.

---

## Project Overview

The Alura Food project aims to showcase a modern microservice architecture. This specific repository focuses on the **Payments Microservice**, responsible for handling all payment-related operations within the Alura Food ecosystem.

---

## Key Features & Technologies

This project covers a wide range of essential microservices concepts and technologies:

### 1. Initial Setup & Project Foundation

* **Monolith to Microservice Motivation:** Understanding the rationale behind breaking down monolithic applications into smaller, independent microservices.
* **Development Environment Setup:** Guidance on installing Java 17, Maven, MySQL, IntelliJ IDEA, and Postman.
* **Spring Boot Project Initialization:** Starting new projects efficiently using `start.spring.io`.
* **Core Dependencies:** Inclusion of necessary dependencies for building a payments microservice.

### 2. Microservice Development Essentials

* **Package by Layer:** Organizing project classes intuitively into `model`, `repository`, `service`, and `controller` packages for clear separation of concerns.
* **JPA Entity Mapping:** Creating database table representations using `@Entity` and `@Table` for seamless ORM integration with JPA.
* **Lombok Integration:** Leveraging Lombok annotations (`@AllArgsConstructor`, `@NoArgsConstructor`, `@Getter`, `@Setter`) to reduce boilerplate code for constructors, getters, and setters.
* **Data Validation:** Implementing robust data validation with annotations like `@NotBlank`, `@NotNull`, `@Size`, and `@Positive`.
* **Enumerated Types (Enums):** Defining an `Enum` for `OrderStatus` (e.g., `CREATED`, `CONFIRMED`, `CANCELED`) for improved type safety and readability.
* **JPA Repository:** Utilizing `JpaRepository` to inherit basic CRUD operations (`findAll`, `findById`, `save`, etc.), streamlining data access.
* **Data Transfer Objects (DTOs):** Implementing DTOs to control the exposure and reception of data attributes via the API, enhancing flexibility and security.
* **Service Layer (Business Logic):** Separating business logic and repository access into a dedicated `Service` layer.
* **ModelMapper:** Using ModelMapper for efficient conversion between model and DTO objects.
* **REST Controller Development:** Building RESTful API endpoints with `@RestController` and defining routes.
* **HTTP Method Mapping:** Implementing API methods using `@GetMapping`, `@PostMapping`, `@PutMapping`, and `@DeleteMapping`.
* **Request Parameter Handling:** Using `@PathVariable` for URL parameters and `@RequestBody` for handling data in the request body.

### 3. Database Management & API Testing

* **Database Migrations (Flyway):** Understanding and implementing database migrations using Flyway for version control of schema changes.
* **Flyway Naming Convention:** Adhering to the `V<version_number>__<command_name>.sql` naming standard for Flyway scripts.
* **MySQL Configuration:** Configuring MySQL database connection properties in `application.properties`.
* **API Testing with Postman:** Practicing API requests using Postman, including GET, POST, PUT, and DELETE HTTP verbs.

### 4. Service Discovery & Registry

* **Service Discovery Concept:** Grasping the mechanism for microservices to discover each other by name, decoupling them from specific IPs or ports.
* **Service Registry Concept:** Understanding the role of a central server where microservices register themselves for discovery.
* **Eureka Server Implementation:** Implementing a service registry using Eureka Server, a part of Spring Cloud.
* **Eureka Client Configuration:** Configuring microservices to correctly perform self-registration with Eureka Client.

### 5. API Gateway & Load Balancing

* **API Gateway Integration:** Incorporating an API Gateway into the architecture to provide a single entry point for the application.
* **Microservice Access through Gateway:** Adapting how microservices are accessed, routing requests through the Gateway using the microservice name.
* **Port Information Retrieval:** Creating a method to return the port of the current instance handling the request.
* **Gateway-Eureka Integration:** Integrating the API Gateway with Eureka for efficient request load balancing across available microservice instances.

### 6. Inter-Microservice Communication & Resilience

* **Open Feign (Synchronous Communication):** Utilizing Spring Cloud Open Feign for declarative synchronous communication between microservices.
* **Payment Confirmation (PUT Request):** Implementing a PUT request from the payments service to the orders service to confirm payment.
* **Circuit Breaker Concept:** Understanding the circuit breaker pattern to prevent cascading failures by interrupting calls to failing services.
* **Fallback Implementation:** Implementing fallback mechanisms to gracefully handle communication failures and prevent service inoperability from affecting other services.

---

## Getting Started

To run this project locally, follow these steps:

1.  **Prerequisites:**
    * Java Development Kit (JDK) 17 or higher
    * Apache Maven
    * MySQL Database
    * An IDE (e.g., IntelliJ IDEA)
    * Postman (for API testing)

2.  **Clone the Repository:**
    ```bash
    git clone <your-repository-url>
    cd alura-food-payments-microservice
    ```

3.  **Database Setup:**
    * Create a MySQL database (e.g., `alura_food_payments`).
    * Update the `src/main/resources/application.properties` file with your MySQL connection details:
        ```properties
        spring.datasource.url=jdbc:mysql://localhost:3306/alura_food_payments?createDatabaseIfNotExist=true
        spring.datasource.username=your_username
        spring.datasource.password=your_password
        spring.jpa.hibernate.ddl-auto=update # Or 'validate' after initial setup
        ```
    * Flyway will handle schema migrations automatically on startup.

4.  **Build the Project:**
    ```bash
    mvn clean install
    ```

5.  **Run the Application:**
    ```bash
    mvn spring-boot:run
    ```

6.  **Access the API:**
    * Once the application is running, you can use Postman to send requests to the API endpoints.
    * Remember to also set up and run the Eureka Server and API Gateway projects for a complete microservice experience.

---

## API Endpoints (Payments Microservice)

Here are some example endpoints provided by the Payments Microservice:

* **GET /payments:** Retrieve all payments.
* **GET /payments/{id}:** Retrieve a payment by ID.
* **POST /payments:** Create a new payment.
* **PUT /payments/{id}:** Update an existing payment.
* **DELETE /payments/{id}:** Delete a payment.

**(Note: Specific request/response bodies will depend on your DTO definitions.)**

---

## Architecture Diagram (High-Level)

```
+----------------+       +-------------------+       +--------------------+
|                |       |                   |       |                    |
|   API Gateway  |<----->|  Eureka Server    |<----->| Payments Microservice |
| (Entry Point)  |       | (Service Registry)|       | (Instance 1)       |
|                |       |                   |       |                    |
+----------------+       +-------------------+       +--------------------+
        ^                                                    |
        |                                                    | (Synchronous)
        v                                                    v
+--------------------+                         +----------------------+
|                    |                         |                      |
| Payments Microservice |<--------------------->| Orders Microservice  |
| (Instance 2)       |                         | (Future/Other Service) |
|                    |                         |                      |
+--------------------+                         +----------------------+
```

---

## Future Enhancements

* Add more comprehensive unit and integration tests.
* Implement asynchronous communication patterns (e.g., Kafka, RabbitMQ).
* Integrate a centralized logging system.
* Implement distributed tracing.
* Explore containerization with Docker and orchestration with Kubernetes.

---

Feel free to explore the codebase and learn from the implemented concepts. Contributions and feedback are welcome!
