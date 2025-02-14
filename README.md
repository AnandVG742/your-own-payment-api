

---

# **Payment API Documentation**  

## **Overview**  
The Payment API provides a secure and efficient way for merchants to process payments, refunds, and retrieve transaction details. It supports multiple payment methods such as **credit cards, debit cards, UPI, and digital wallets**.  

## **Base URL**  
```
https://api.example.com/v1/payments
```

## **Authentication**  
All API requests must include an **API key** in the header:  
```http
Authorization: Bearer YOUR_API_KEY
```

## **Endpoints**  

### **1. Create Payment**  
**Method:** `POST /v1/payments`  
**Request:**  
```json
{
  "amount": 5000,
  "currency": "USD",
  "payment_method": "card",
  "customer": {
    "name": "John Doe",
    "email": "johndoe@example.com"
  },
  "card": {
    "number": "4111111111111111",
    "expiry_month": "12",
    "expiry_year": "2025",
    "cvv": "123"
  }
}
```
**Response:**  
```json
{
  "payment_id": "pay_12345",
  "status": "success",
  "amount": 5000,
  "currency": "USD",
  "timestamp": "2025-02-14T12:00:00Z"
}
```

### **2. Retrieve Payment**  
**Method:** `GET /v1/payments/{payment_id}`  
**Response:**  
```json
{
  "payment_id": "pay_12345",
  "status": "success",
  "amount": 5000,
  "currency": "USD",
  "timestamp": "2025-02-14T12:00:00Z",
  "customer": {
    "name": "John Doe",
    "email": "johndoe@example.com"
  }
}
```

### **3. Refund Payment**  
**Method:** `POST /v1/payments/{payment_id}/refund`  
**Request:**  
```json
{
  "amount": 5000,
  "reason": "Customer requested refund"
}
```
**Response:**  
```json
{
  "refund_id": "refund_98765",
  "payment_id": "pay_12345",
  "status": "refunded",
  "amount": 5000,
  "timestamp": "2025-02-14T13:00:00Z"
}
```

## **Error Handling**  

| Error Code | Description |
|------------|-------------|
| 400 | Bad Request (Invalid parameters) |
| 401 | Unauthorized (Invalid API key) |
| 404 | Not Found (Invalid payment ID) |
| 500 | Internal Server Error |

**Example Error Response:**  
```json
{
  "error": "Invalid API Key",
  "status": 401
}
```

## **Security Best Practices**  
✔ Use **HTTPS** for secure API calls.  
✔ Store API keys securely (never expose them in client-side code).  
✔ Implement **rate limiting** to prevent abuse.  
✔ Validate all user input to prevent **SQL Injection** and **XSS attacks**.  

## **Rate Limits**  
- **50 requests per minute** per user.  
- Requests exceeding this limit receive a **429 Too Many Requests** error.  

**Example Rate Limit Error:**  
```json
{
  "error": "Rate limit exceeded",
  "status": 429
}
```

## **License**  
This API is licensed under **MIT License**.  

---

