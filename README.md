# hotel-management-system
A robust backend RESTful API service for managing hotel operations, room bookings, guest profiles, and billing, built with Java, Spring Boot, and JDBC for direct SQL execution.
# Hotel Management System 🏨

A comprehensive backend service designed to streamline hotel operations, handle room reservations, manage guest records, and process billing using direct relational database interactions.



[ API Client ]
│
│ uses REST API
▼
[ REST API / Hotel API ]
│
├───────► manages ───────► [ Room Bookings ]
├───────► manages ───────► [ Guest Profiles ]  (Hotel Operations)
├───────► manages ───────► [ Billing ]
│
└───────► executes SQL ──► [ Persistence / SQL Database ]
## 🛠️ Tech Stack & Prerequisites
- **Language:** Java 17+
- **Framework:** Spring Boot 3.x (Spring Web)
- **Database Access:** Spring JDBC / `JdbcTemplate` (Raw SQL queries for high control and execution speed)
- **Database:** MySQL / PostgreSQL
- **Build Tool:** Maven / Gradle

## ✨ Core Features
- **Room Management:** Add, update, and check availability of rooms (Single, Double, Suite).
- **Guest Profiles:** Register and maintain guest information and booking history.
- **Reservation System:** Book rooms, manage check-in / check-out statuses, and prevent double bookings.
- **Billing & Invoicing:** Generate invoices based on stay duration, room type, and extra amenities.
- **SQL Driven:** Custom SQL scripts for efficient schema creation, queries, and data manipulation.

## 🚀 Getting Started

### 1. Database Setup
Create your SQL database and run the schema setup script:
```sql
CREATE DATABASE hotel_management_db;
-- Run initial tables script located at /src/main/resources/schema.sql****
spring.datasource.url=jdbc:mysql://localhost:3306/hotel_db
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

./mvnw clean spring-boot:run
