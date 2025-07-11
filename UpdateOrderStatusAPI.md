
# 📄 API Design Document: Update Order Status API

## 1. Overview

This API allows clients to update the **status** of an existing order. It uses the `PATCH` method as the update is a **partial modification** of the order resource.

---

## 2. Endpoint

```
PATCH /api/orders/{orderId}/status
```

---

## 3. Request

### 3.1 Path Parameter

| Name      | Type   | Description                      | Required |
|-----------|--------|----------------------------------|----------|
| `orderId` | String | Unique identifier for the order  | Yes      |

---

### 3.2 Request Body

```json
{
  "status": "DELIVERED"
}
```

| Field    | Type   | Description                          | Required | Allowed Values                                               |
|----------|--------|--------------------------------------|----------|--------------------------------------------------------------|
| `status` | String | New status to set for the order      | Yes      | `PENDING`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `RETURNED` |

---

### 3.3 Example Request

```http
PATCH /api/orders/ORD123/status
Content-Type: application/json

{
  "status": "SHIPPED"
}
```

---

## 4. Response

### 4.1 Success Response (HTTP 200)

```json
{
  "orderId": "ORD123",
  "status": "SHIPPED",
  "message": "Order status updated successfully."
}
```

---

### 4.2 Error Responses

| Status Code | Description                            | Example Message                            |
|-------------|----------------------------------------|--------------------------------------------|
| 400         | Invalid status or transition            | `Invalid status: ARCHIVED`                 |
| 404         | Order not found                         | `Order not found: ORD123`                  |
| 403         | Unauthorized update attempt             | `You are not allowed to update this order` |

---

## 5. Business Rules

- Status transitions should follow valid flows:
  - `PENDING` → `PROCESSING` → `SHIPPED` → `DELIVERED`
  - Cannot move backward once `DELIVERED` or `SHIPPED`
---

## 6. Security

- **Authentication:** Bearer token (JWT or session)

---

