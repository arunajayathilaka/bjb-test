# High Level Design


![image](\images\highlevel-architecture.png)


#### High-Level Design Summary (Microservices)
- The system uses **Microservices Architecture** where each business function (Order, Inventory, Product, Payment, Customer) is an independent service.

- An **API Gateway** acts as a single entry point for clients.

- **Kafka** enables event-driven communication between services, e.g., inventory updates trigger product updates.

- **Redis Cache** in the Product Service ensures high-speed access to frequently read data.

- Each service has its own **database** for data isolation and scalability.


#### API Documentation

1. [api/v1/orders](OrderCreationAPI.md)
2. [api/v1/orders/{id}](OrderByIdAPI.md)
3. [api/v1/orders/{orderId}/status](UpdateOrderStatusAPI.md)
4. [api/v1/orders/{id}/cancel](CancelOrderAPI.md)
5. [api/v1/orders/customer/{customerId}](OrdersByCustomerAPI.md)


#### Order Creation Flow

![image](\images\order-creation-flow.png)


#### Payment Flow

![image](\images\payment-flow.png)


#### Retrieve Product Flow

In this design, whenever the inventory of a product changes (e.g., stock level update), the **Inventory Service** publishes a **Kafka message** with the event type `PRODUCT_UPDATE`. This event carries essential product information such as product ID, updated quantity.

The **Product Service** listens to these Kafka events in real-time. Upon receiving a `PRODUCT_UPDATE` event, it updates the corresponding **Redis cache** with the latest product information.

This **event-driven mechanism** ensures that:

**Redis cache** always holds up-to-date product data.

**High-volume read** requests for product details are served efficiently and with **low latency** from Redis.

The primary database is **protected from read-heavy traffic**, improving overall **system scalability** and performance.

![image](\images\retrieve-product-flow.png)