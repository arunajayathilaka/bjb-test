
# 📄 API Design Document: Get Order by ID API

## 1. Overview

This API allows clients to **retrieve detailed information of a specific order** using its unique order ID.

---

## 2. Endpoint

```
GET /api/orders/{orderId}
```

---

## 3. Request

### 3.1 Path Parameter

| Name      | Type   | Description                    | Required |
|----------|--------|----------------------------------|----------|
| `orderId` | String | Unique identifier for the order | Yes      |

### 3.2 Example Request

```http
GET /api/orders/ORD123
Authorization: Bearer <token>
```

---

## 4. Response

### 4.1 Success Response (HTTP 200 OK)

```json
{
  "orderId": "ORD123",
  "customerId": "CUST456",
  "status": "SHIPPED",
  "totalAmount": 120.75,
  "createdAt": "2024-07-11T09:00:00Z",
  "items": [
    {
      "productId": "PROD1001",
      "productName": "Wireless Mouse",
      "quantity": 2,
      "price": 25.00
    },
    {
      "productId": "PROD1002",
      "productName": "Keyboard",
      "quantity": 1,
      "price": 70.75
    }
  ],
  "shippingAddress": {
    "line1": "123 Main Street",
    "line2": "Apt 4B",
    "city": "New York",
    "state": "NY",
    "postalCode": "10001",
    "country": "USA"
  },
  "paymentMethod": "CREDIT_CARD"
}
```

### 4.2 Error Responses

| Status Code | Meaning                 | Example Message              |
|------------|-------------------------|------------------------------|
| 404        | Order not found          | `Order not found: ORD123`     |
| 403        | Unauthorized access      | `Access denied`               |
| 500        | Internal server error    | `Failed to retrieve order`    |

---

## 5. Business Rules

- Complete order details including items, shipping, and payment are returned.

---

## 6. Security

- **Authentication:** Required (Bearer Token)

Example header:
```
Authorization: Bearer <token>
```

---
