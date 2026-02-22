# 🚪 API Gateway - PetShop Microservice

API Gateway là cổng trung gian (Entry Point) của hệ thống **PetShop Microservice**.  
Service này chịu trách nhiệm định tuyến (routing), xác thực (authentication) và chuyển tiếp request đến các microservice nội bộ như:

- Auth Service
- User Service
- Product Service
- Order Service

---

## 🏗 Vai trò trong hệ thống

API Gateway đóng vai trò:

- Là điểm truy cập duy nhất từ client
- Routing request đến đúng service
- Forward JWT token đến các service nội bộ
- Centralized security
- Hỗ trợ CORS
- Logging & Monitoring (nếu có cấu hình)

---

## 🚀 Tech Stack

- **Java 17**
- **Spring Boot 3**
- **Spring Cloud Gateway**
- **Spring Security**
- **JWT**
- **Eureka Client (nếu dùng service discovery)**
- **Maven**

---

## 📌 Kiến trúc tổng thể


Client
│
▼
API Gateway
│
├── Auth Service
├── User Service
├── Product Service
└── Order Service


Tất cả request từ frontend hoặc client app sẽ đi qua Gateway trước khi đến service đích.

---

## 🔀 Routing Configuration

Ví dụ cấu hình trong `application.yml`:

```yml
spring:
  cloud:
    gateway:
      routes:
        - id: auth-service
          uri: lb://AUTH-SERVICE
          predicates:
            - Path=/api/auth/**
        - id: user-service
          uri: lb://USER-SERVICE
          predicates:
            - Path=/api/users/**
        - id: product-service
          uri: lb://PRODUCT-SERVICE
          predicates:
            - Path=/api/products/**
        - id: order-service
          uri: lb://ORDER-SERVICE
          predicates:
            - Path=/api/orders/**
🔐 Security

Gateway xử lý:

Validate JWT trước khi forward

Bỏ qua authentication cho:

/api/auth/**

Swagger endpoints

Forward token cho các service phía sau

📂 Cấu trúc project
src/main/java/com/huytpq/api_gateway
├── config          # Security / CORS config
├── filter          # JWT filter
├── route           # Custom route config (nếu có)
├── ApiGatewayApplication.java
▶️ Chạy project
mvn clean install
mvn spring-boot:run

Hoặc:

java -jar target/api-gateway-0.0.1-SNAPSHOT.jar
🌐 Port mặc định
http://localhost:8080
📦 Yêu cầu chạy kèm

Để hệ thống hoạt động đầy đủ, cần chạy:

Auth Service

User Service

Product Service

Order Service

Eureka Server (nếu dùng service discovery)
