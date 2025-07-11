
# 📄 API Design Document: Create Order API

## 1. Overview

This API allows clients to **create a new order** for a customer by providing product items, shipping address, and payment details.

---

## 2. Endpoint

```
POST /api/orders
```

---

## 3. Request

### 3.1 Request Body Example

```json
{
  "customerId": "CUST123",
  "items": [
    {
      "productId": "PROD1001",
      "quantity": 2
    },
    {
      "productId": "PROD1002",
      "quantity": 1
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
  "paymentMethod": "CREDIT_CARD",
  "notes": "Please deliver between 9AM-5PM"
}
```

| Field            | Type        | Description                          | Required |
|------------------|------------|--------------------------------------|----------|
| `customerId`     | String      | ID of the customer                   | Yes      |
| `items`          | Array       | List of product items (id + qty)     | Yes      |
| `shippingAddress`| Object      | Shipping address                     | Yes      |
| `paymentMethod`  | String      | Payment method (`CREDIT_CARD`, `BANK_TRANFER`, `CASH_ON_DELIVERY`) | Yes |
| `notes`          | String      | Optional notes for the order         | No       |

---

## 4. Response

### 4.1 Success Response (HTTP 201 Created)

```json
{
  "orderId": "ORD56789",
  "status": "INITIATED",
  "totalAmount": 150.00,
  "createdAt": "2024-07-11T10:30:00Z",
  "message": "Order created successfully."
}
```

### 4.2 Error Responses

| Status Code | Meaning                 | Example Message                         |
|------------|-------------------------|-----------------------------------------|
| 400        | Invalid request data     | `Product ID is missing`                 |
| 404        | Customer or Product not found | `Customer not found: CUST123`      |
| 500        | Server error             | `Unable to create order at this time`   |

---

## 5. Business Rules

- Validate:
  - Customer exists.
  - Products exist & quantities are available.
  - Payment method is valid.
- Calculate total amount based on products and quantities.
- Set initial order status: `INITIATED`.

---

## 6. Security

- **Authentication:** Required (Bearer Token)

Example Header:
```
Authorization: Bearer <token>
```
