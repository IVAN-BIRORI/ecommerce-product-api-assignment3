# E-Commerce Product API

Hey! This is my REST API project for managing products in an e-commerce system. I built it using Spring Boot and PostgreSQL for my Web Technology class. The API lets you do all the basic stuff you'd need for a product catalog - adding products, viewing them, updating details, and removing items.

**Author:** BIRORI KANYAMIBWA IVAN  
**Student ID:** 27255

## What This Project Does

Basically, this API handles everything related to products in an online store. You can:
- Add new products to the database
- View all products or search for specific ones
- Update product info like price or stock
- Delete products you don't need anymore
- Filter products by category, brand, or price range
- Check which products are currently in stock

## CRUD Operations Summary

Here's where you can find each CRUD operation:

| Operation | HTTP Method | Endpoint | Description |
|-----------|-------------|----------|-------------|
| **CREATE** | POST | `/api/products` | Add a new product (Endpoint #10) |
| **READ** | GET | `/api/products` | Get all products (Endpoints #1-9) |
| **UPDATE** | PUT | `/api/products/{id}` | Update entire product (Endpoint #11) |
| **UPDATE** | PATCH | `/api/products/{id}/stock` | Update just the stock (Endpoint #12) |
| **DELETE** | DELETE | `/api/products/{id}` | Remove a product (Endpoint #13) |

## Technologies I Used

- Spring Boot 3.2.0 - makes it easy to create REST APIs
- Spring Data JPA - handles all the database stuff
- PostgreSQL - where all the product data is stored
- Maven - for managing dependencies
- Java 17

## How to Set It Up

First, make sure you have Java 17, Maven, and PostgreSQL installed on your machine.

Create the database in PostgreSQL:
```sql
CREATE DATABASE ecommerce_db;
```

Then open `src/main/resources/application.properties` and put your PostgreSQL password:
```
spring.datasource.password=YOUR_PASSWORD
```

## Running the App

Just run this command:
```
mvn spring-boot:run
```

The API will start on http://localhost:8080 and you can test it with Postman.

## All API Endpoints

---
### READ Operations (Getting Data)
---

### 1. Get All Products
**GET** `/api/products`

This one just gives you every product in the database. Simple and straightforward.

```
http://localhost:8080/api/products
```

![Get all products](images2/1.%20Get%20All%20Products.png)

### 2. Get Products with Pagination
**GET** `/api/products?page={page}&limit={limit}`

When you have lots of products, you don't want to load them all at once. This endpoint lets you get them in smaller chunks.

```
http://localhost:8080/api/products?page=0&limit=5
```

![Get products with pagination](images2/2.Get%20Products%20with%20Pagination.png)

### 3. Get Product by ID
**GET** `/api/products/{id}`

Need details about one specific product? Just pass in the ID and you'll get all its info.

```
http://localhost:8080/api/products/2
```

![Get product by ID](images2/3.%20Get%20Product%20by%20ID.png)

### 4. Get Products by Category
**GET** `/api/products/category/{category}`

Filters products by their category. Good for when customers want to browse Electronics, Clothing, etc.

```
http://localhost:8080/api/products/category/Electronics
```

![Get product by category](images2/4.%20Get%20Products%20by%20Category.png)

### 5. Get Products by Brand
**GET** `/api/products/brand/{brand}`

Same idea but for brands. Want all Apple products? This is the endpoint.

```
http://localhost:8080/api/products/brand/Apple
```

![Get product by brand](images2/5.%20Get%20Products%20by%20Brand.png)

### 6. Search Products by Keyword
**GET** `/api/products/search?keyword={keyword}`

This searches through product names and descriptions. Type "phone" and you'll get anything with phone in the name or description.

```
http://localhost:8080/api/products/search?keyword=phone
```

![Search product by keyword](images2/6.%20Search%20Products%20by%20Keyword.png)

### 7. Get Products by Price Range
**GET** `/api/products/price-range?min={min}&max={max}`

Perfect for budget filtering. Set a minimum and maximum price and get products in that range.

```
http://localhost:8080/api/products/price-range?min=100&max=500
```

![Get product by price range](images2/7.%20Get%20Products%20by%20Price%20Range.png)

### 8. Get Products by BOTH Price and Brand
**GET** `/api/products/filter?price={price}&brand={brand}`

Combines two filters at once - find products from a specific brand at a specific price.

```
http://localhost:8080/api/products/filter?price=999.99&brand=Apple
```

![Search both by price and brand](images2/8.%20Get%20Products%20by%20BOTH%20Price%20Range%20and%20Brand.png)

### 9. Get In-Stock Products
**GET** `/api/products/in-stock`

Only shows products that are actually available (stock quantity > 0). No point showing stuff that's sold out!

```
http://localhost:8080/api/products/in-stock
```

![Get in-stock products](images2/9.%20Get%20In-Stock%20Products.png)

---
### CREATE Operation (Adding Data)
---

### 10. Add New Product (CREATE)
**POST** `/api/products`

This is the CREATE part of CRUD. Send product details in JSON format and it gets saved to the database. If you try to add a product with a name that already exists, you'll get a 409 Conflict error - no duplicates allowed!

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

---
### UPDATE Operations (Modifying Data)
---

### 11. Update Product (UPDATE)
**PUT** `/api/products/{id}`

This is the UPDATE part of CRUD. Use this when you need to change multiple fields of a product - like updating the price, description, or any other details. You send the complete updated product info.

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

### 12. Update Stock Quantity (UPDATE - Partial)
**PATCH** `/api/products/{id}/stock?quantity={quantity}`

This is also UPDATE but only for the stock quantity. PATCH is used when you just want to change one field instead of sending the whole product again. Super useful for inventory management.

```
http://localhost:8080/api/products/1/stock?quantity=100
```

Response: `200 OK` or `404 Not Found`

![Update stock quantity](images2/12.%20Update%20Stock%20Quantity.png)

---
### DELETE Operation (Removing Data)
---

### 13. Delete Product (DELETE)
**DELETE** `/api/products/{id}`

This is the DELETE part of CRUD. Removes a product from the database permanently. Returns 204 (No Content) if successful, or 404 if the product doesn't exist.

```
http://localhost:8080/api/products/1
```

Response: `204 No Content` or `404 Not Found`

![Delete product](images2/13.%20Delete%20Product.png)

---

## HTTP Status Codes

These are the responses you'll get from the API:

| Code | Meaning | When You'll See It |
|------|---------|-------------------|
| 200 | OK | GET, PUT, PATCH worked fine |
| 201 | Created | POST successfully added a product |
| 204 | No Content | DELETE removed the product |
| 404 | Not Found | Product with that ID doesn't exist |
| 409 | Conflict | Tried to add a product with a name that already exists |

## Project Structure

Here's how I organized the code:

```
src/main/java/com/restapi/
├── RestApiApplication.java         (starts the application)
├── controller/
│   └── ecommerce/
│       └── ProductController.java  (handles HTTP requests)
├── model/
│   └── ecommerce/
│       └── Product.java            (the product entity)
├── repository/
│   └── ecommerce/
│       └── ProductRepository.java  (database queries)
└── service/
    └── ecommerce/
        └── ProductService.java     (business logic)
```

The structure follows the standard Spring Boot pattern - Controller handles requests, Service contains the logic, Repository talks to the database, and Model defines the data structure.

## Database Schema

The product table in PostgreSQL:

| Column | Type | Constraints |
|--------|------|-------------|
| product_id | BIGINT | PRIMARY KEY, AUTO_INCREMENT |
| name | VARCHAR | NOT NULL, UNIQUE |
| description | VARCHAR | |
| price | DOUBLE | |
| category | VARCHAR | |
| stock_quantity | INTEGER | |
| brand | VARCHAR | |

---

Thanks for checking out my project!
