# E-Commerce Product API

RESTful API built with Spring Boot for managing e-commerce products with PostgreSQL database.

**Author:** BIRORI KANYAMIBWA IVAN  
**Student ID:** 27255

## Features

- Complete CRUD operations for products
- Search and filter products by category, brand, price range
- Pagination support
- Stock management
- Duplicate product validation
- PostgreSQL database persistence

## Technologies Used

- Spring Boot 3.2.0
- Spring Data JPA
- PostgreSQL
- Maven
- Java 17

## Prerequisites

- Java 17 or higher
- Maven 3.6+
- PostgreSQL
- Postman (for testing)

## Database Setup

Create PostgreSQL database:
```sql
CREATE DATABASE ecommerce_db;
```

Update `src/main/resources/application.properties` with your PostgreSQL password:
```
spring.datasource.password=YOUR_PASSWORD
```

## Running the Application

```
mvn spring-boot:run
```

Application runs on: http://localhost:8080

## API Endpoints

### 1. Get All Products
**GET** `/api/products`

```
http://localhost:8080/api/products
```

![Get all products](images2/1.%20Get%20All%20Products.png)

### 2. Get Products with Pagination
**GET** `/api/products?page={page}&limit={limit}`

```
http://localhost:8080/api/products?page=0&limit=5
```

![Get products with pagination](images2/2.Get%20Products%20with%20Pagination.png)

### 3. Get Product by ID
**GET** `/api/products/{id}`

```
http://localhost:8080/api/products/2
```

![Get product by ID](images2/3.%20Get%20Product%20by%20ID.png)

### 4. Get Products by Category
**GET** `/api/products/category/{category}`

```
http://localhost:8080/api/products/category/Electronics
```

![Get product by category](images2/4.%20Get%20Products%20by%20Category.png)

### 5. Get Products by Brand
**GET** `/api/products/brand/{brand}`

```
http://localhost:8080/api/products/brand/Apple
```

![Get product by brand](images2/5.%20Get%20Products%20by%20Brand.png)

### 6. Search Products by Keyword
**GET** `/api/products/search?keyword={keyword}`

```
http://localhost:8080/api/products/search?keyword=phone
```

![Search product by keyword](images2/6.%20Search%20Products%20by%20Keyword.png)

### 7. Get Products by Price Range
**GET** `/api/products/price-range?min={min}&max={max}`

```
http://localhost:8080/api/products/price-range?min=100&max=500
```

![Get product by price range](images2/7.%20Get%20Products%20by%20Price%20Range.png)

### 8. Get Products by BOTH Price Range and Brand
**GET** `/api/products/filter?price={price}&brand={brand}`

```
http://localhost:8080/api/products/filter?price=999.99&brand=Apple
```

![Search both by price and brand](images2/8.%20Get%20Products%20by%20BOTH%20Price%20Range%20and%20Brand.png)

### 9. Get In-Stock Products
**GET** `/api/products/in-stock`

```
http://localhost:8080/api/products/in-stock
```

![Get in-stock products](images2/9.%20Get%20In-Stock%20Products.png)

### 10. Add New Product
**POST** `/api/products`

Headers: `Content-Type: application/json`

Body:
```json
{
  "name": "iPhone 15",
  "description": "Latest Apple smartphone",
  "price": 999.99,
  "category": "Electronics",
  "stockQuantity": 50,
  "brand": "Apple"
}
```

Response: `201 Created`

![Add new product](images2/10.%20Add%20New%20Product.png)

### 11. Update Product
**PUT** `/api/products/{id}`

Headers: `Content-Type: application/json`

Body:
```json
{
  "name": "iPhone 15 Pro",
  "description": "Latest Apple flagship smartphone",
  "price": 1199.99,
  "category": "Electronics",
  "stockQuantity": 30,
  "brand": "Apple"
}
```

Response: `200 OK` or `404 Not Found`

![Update product](images2/11.%20Update%20Product.png)

### 12. Update Stock Quantity
**PATCH** `/api/products/{id}/stock?quantity={quantity}`

```
http://localhost:8080/api/products/1/stock?quantity=100
```

Response: `200 OK` or `404 Not Found`

![Update stock quantity](images2/12.%20Update%20Stock%20Quantity.png)

### 13. Delete Product
**DELETE** `/api/products/{id}`

```
http://localhost:8080/api/products/1
```

Response: `204 No Content` or `404 Not Found`

![Delete product](images2/13.%20Delete%20Product.png)

## HTTP Status Codes

- `200 OK` - Successful GET, PUT, PATCH requests
- `201 Created` - Successful POST request
- `204 No Content` - Successful DELETE request
- `404 Not Found` - Resource not found
- `409 Conflict` - Duplicate product name

## Project Structure

```
src/main/java/com/restapi/
├── RestApiApplication.java
├── controller/
│   └── ecommerce/
│       └── ProductController.java
├── model/
│   └── ecommerce/
│       └── Product.java
├── repository/
│   └── ecommerce/
│       └── ProductRepository.java
└── service/
    └── ecommerce/
        └── ProductService.java
```

## Database Schema

**Table: product**

| Column | Type | Constraints |
|--------|------|-------------|
| product_id | BIGINT | PRIMARY KEY, AUTO_INCREMENT |
| name | VARCHAR | NOT NULL, UNIQUE |
| description | VARCHAR | |
| price | DOUBLE | |
| category | VARCHAR | |
| stock_quantity | INTEGER | |
| brand | VARCHAR | |
