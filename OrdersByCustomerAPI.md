# 📄 API Design Document:  Orders by Customer API

## 1. Overview

This API retrieves a list of all orders placed by a specific customer using their unique `customerId`.

---

## 2. Endpoint

```
GET /api/customers/{customerId}/orders
```

---

## 3. Request

### 3.1 Path Parameter

| Parameter   | Type   | Required | Description                        |
|------------|--------|----------|------------------------------------|
| customerId | string | Yes      | Unique identifier of the customer |

---

### 3.2 Query Parameters (Optional)
| Parameter   | Type   | Description                                 |
|------------|--------|---------------------------------------------|
| status     | string | Filter orders by status (e.g., `PENDING`, `SHIPPED`, `CANCEL`) |
| page       | number | Page number for pagination (default: 1)     |
| size       | number | Page size for pagination (default: 10)      |
---

### 3.3 Example Request

```http
GET /api/customers/{customerId}/orders
```

---

## 4. Response

### 4.1 Success Response (HTTP 200)

```json
{
  "customerId": "cust-001",
  "orders": [
    {
      "orderId": "order-123",
      "status": "Pending",
      "totalAmount": 150.75,
      "createdAt": "2024-07-10T15:00:00Z"
    },
    {
      "orderId": "order-124",
      "status": "Shipped",
      "totalAmount": 89.99,
      "createdAt": "2024-07-05T10:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "size": 10,
    "totalPages": 2,
    "totalOrders": 15
  }
}
```

---

### 4.2 Error Responses

| Status Code | Description                          | Response Body Example                   |
|-------------|--------------------------------------|-----------------------------------------|
| 400 Bad Request | Invalid request parameters         | `{ "error": "Invalid parameters." }`     |
| 404 Not Found  | Customer not found                  | `{ "error": "Customer not found." }`     |
| 500 Internal Server Error | Server error                   | `{ "error": "Internal server error." }` |


---

## 5. Business Rules
- Supports pagination for large result sets.
- Can filter orders by status for better usability.
---

## 6. Security

- **Authentication:** Bearer token (JWT or session)


