
# 📄 API Design Document: Cancel Order by ID API

## 1. Overview

This API allows clients to **cancel a specific order** using its unique order ID.

---

## 2. Endpoint

```
Patch api/v1/orders/{orderId}/cancel
```

---

## 3. Request

### 3.1 Path Parameter

| Parameter | Type   | Required | Description                |
|-----------|--------|----------|----------------------------|
| orderId   | string | Yes      | Unique identifier of the order to cancel |

### 3.2 Example Request

```http
PATCH /api/orders/ORD123/cancel
Authorization: Bearer <token>
```

---

## 4. Response

### 4.1 Success Response (HTTP 200 OK)

```json
{
  "orderId": "123456",
  "status": "CANCEL",
  "message": "Order has been successfully cancelled."
}
```

### 4.2 Error Responses

| Status Code | Description                    | Response Body Example                               |
|-------------|-------------------------------|----------------------------------------------------|
| 400 Bad Request | Invalid `orderId` format or order not cancellable | `{ "error": "Order cannot be cancelled." }`        |
| 404 Not Found  | Order with given `orderId` not found | `{ "error": "Order not found." }`                   |
| 500 Internal Server Error | Server error processing the request | `{ "error": "Internal server error." }`            |

---

## 5. Business Rules
- Can only `CANCEL` if not already `DELIVERED` or `SHIPPED`

---

## 6. Security

- **Authentication:** Required (Bearer Token)

Example header:
```
Authorization: Bearer <token>
```

---
