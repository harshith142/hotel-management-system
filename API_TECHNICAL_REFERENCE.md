# 🔧 API Endpoints - Complete Technical Reference

**Generated:** January 25, 2026  
**Framework:** Spring Boot REST API  
**Frontend:** Angular with Standalone Components  

---

## 📚 COMPLETE API REFERENCE BY CONTROLLER

### 1️⃣ AuthController
**Base Path:** `/api/auth`  
**Authentication Required:** None (public endpoints)

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 1 | POST | `/login` | Customer login | `{username, password}` | `{id, username, email, role, token}` |
| 2 | POST | `/admin/login` | Admin/Staff login | `{username, password}` | `{id, username, email, role, token}` |

---

### 2️⃣ UserController
**Base Path:** `/api`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 3 | POST | `/users` | Register user (ADMIN/STAFF) | `{name, email, username, password, role}` | `{id, name, email, username, role, message}` |
| 4 | POST | `/staff` | Register staff member | `{name, email, username, password}` | `{id, name, email, username, role: STAFF, message}` |

---

### 3️⃣ CustomerController
**Base Path:** `/api/customers`  
**Authentication Required:** Partial (POST public, PUT requires CUSTOMER)

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 5 | POST | `/register` | Customer registration | `{name, email, mobile, address, username, password}` | `{id, name, email, mobile, address, username, role: CUSTOMER, message}` |
| 6 | PUT | `/profile` | Update customer profile | `{name, email, mobile, address}` | `{id, name, email, mobile, address, updatedAt, message}` |

---

### 4️⃣ AdminUserController
**Base Path:** `/api/admin/users`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 7 | POST | (base) | Create user | `{name, email, mobile, username, password, role}` | `{message: "User created successfully"}` |
| 8 | GET | (base) | Get all users | None | `[{id, username, email, name, role, status, createdAt}]` |
| 9 | DELETE | `/{userId}` | Delete user | None | `{message: "User deleted successfully", deletedUserId}` |

---

### 5️⃣ RoomController
**Base Path:** `/api/rooms`  
**Authentication Required:** None (public endpoints)

| # | Method | Endpoint | Description | Query Params | Response |
|---|--------|----------|-------------|--------------|----------|
| 10 | GET | (base) | Get all rooms | None | `[{id, roomNumber, type, price, amenities, occupancy, status}]` |
| 11 | GET | `/{id}` | Get room by ID | None | `{id, roomNumber, type, price, amenities, occupancy, status, bookings}` |
| 12 | GET | `/search` | Search rooms | `checkInDate, checkOutDate, type, minPrice, maxPrice, occupancy, amenities` | `[{id, roomNumber, type, price, amenities, occupancy, status, availability}]` |
| 13 | GET | `/available` | Get available rooms | None | `[{id, roomNumber, type, price, status: AVAILABLE}]` |

---

### 6️⃣ AdminRoomController
**Base Path:** `/api/admin/rooms`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 14 | POST | (base) | Create single room | `{roomNumber, type, price, amenities, occupancy}` | `{id, roomNumber, type, price, amenities, occupancy, status, message}` |
| 15 | POST | `/bulk` | Create multiple rooms | `[{roomNumber, type, price}]` | `{createdCount, totalRequested, failedRooms, message}` |
| 16 | PUT | `/{roomId}` | Update room details | `{roomNumber, type, price, amenities, occupancy}` | `{id, roomNumber, type, price, amenities, occupancy, updatedAt, message}` |
| 17 | PUT | `/{roomId}/status` | Update room status | Query: `status=AVAILABLE\|OCCUPIED\|MAINTENANCE` | `{id, roomNumber, status, updatedAt, message}` |
| 18 | DELETE | `/{roomId}` | Delete room | None | `{message: "Room deleted successfully", deletedRoomId}` |

---

### 7️⃣ BookingController
**Base Path:** `/api/bookings`  
**Authentication Required:** CUSTOMER/ADMIN (varies by endpoint)

| # | Method | Endpoint | Description | Auth | Request | Response |
|---|--------|----------|-------------|------|---------|----------|
| 19 | POST | (base) | Create booking | CUSTOMER/ADMIN | `{customerId, roomId, checkinDate, checkoutDate}` | `{id, customerId, roomId, checkInDate, checkOutDate, totalPrice, status: PENDING, message}` |
| 20 | GET | `/customer/{customerId}` | Get customer bookings | CUSTOMER/ADMIN | None | `[{id, customerId, roomId, roomNumber, roomType, checkInDate, checkOutDate, status, totalPrice}]` |
| 21 | GET | `/customer/{customerId}/history` | Get booking history | CUSTOMER/ADMIN | None | `[{id, customerId, roomNumber, roomType, checkInDate, checkOutDate, numberOfNights, totalPrice, status, completedAt}]` |
| 22 | GET | `/room/{roomId}` | Get bookings by room | ADMIN | None | `[{id, customerId, customerName, checkInDate, checkOutDate, status, totalPrice, createdAt}]` |
| 23 | PUT | `/{bookingId}/confirm` | Confirm booking | ADMIN | None | `{id, customerId, roomId, checkInDate, checkOutDate, status: CONFIRMED, totalPrice, confirmedAt, message}` |
| 24 | PUT | `/{bookingId}/cancel` | Cancel booking | CUSTOMER/ADMIN | None | `{id, customerId, roomId, status: CANCELLED, cancelledAt, message}` |
| 25 | DELETE | `/{bookingId}` | Delete booking | ADMIN | None | `{message: "Booking deleted successfully", deletedBookingId}` |

---

### 8️⃣ AdminBookingController
**Base Path:** `/api/admin/bookings`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Response |
|---|--------|----------|-------------|----------|
| 26 | GET | (base) | Get all bookings | `[{id, customerId, customerName, roomId, roomNumber, checkInDate, checkOutDate, status, totalPrice, createdAt}]` |
| 27 | GET | `/revenue` | Get revenue report | `{totalRevenue, totalBookings, confirmedBookings, cancelledBookings, averageBookingValue, monthlyRevenue, roomOccupancyRate}` |

---

### 9️⃣ PaymentController
**Base Path:** `/api/payments`  
**Authentication Required:** CUSTOMER/ADMIN

| # | Method | Endpoint | Description | Auth | Request | Response |
|---|--------|----------|-------------|------|---------|----------|
| 28 | POST | `/pay` | Process payment | CUSTOMER | `{billId, paymentMode}` | `{id, billId, amount, paymentMode, status: SUCCESS, transactionId, message}` |
| 29 | GET | `/customer/{id}` | Get customer payments | CUSTOMER/ADMIN | None | `[{id, billId, bookingId, amount, paymentMode, status, transactionId, createdAt}]` |
| 30 | GET | `/{paymentId}` | Get payment details | ADMIN | None | `{id, billId, customerId, amount, paymentMode, status, transactionId}` |

---

### 🔟 AdminPaymentController
**Base Path:** `/api/admin/payments`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 31 | POST | (base) | Create payment | `{billId, amount, paymentMode}` | `{id, billId, amount, paymentMode, status, message}` |
| 32 | GET | (base) | Get all payments | None | `[{id, billId, customerId, customerName, amount, paymentMode, status, transactionId, createdAt}]` |
| 33 | GET | `/{paymentId}` | Get payment by ID | None | `{id, billId, customerId, amount, paymentMode, status, transactionId, createdAt}` |

---

### 1️⃣1️⃣ BillController
**Base Path:** `/api/admin/bills`  
**Authentication Required:** ADMIN role

| # | Method | Endpoint | Description | Request | Response |
|---|--------|----------|-------------|---------|----------|
| 34 | POST | (base) | Create bill | `{customerId, bookingId, amount, taxAmount, discountAmount}` | `{id, customerId, bookingId, amount, status: PENDING, message}` |
| 35 | GET | (base) | Get all bills | None | `[{id, customerId, customerName, bookingId, amount, taxAmount, status, createdAt}]` |
| 36 | GET | `/{billId}` | Get bill by ID | None | `{id, customerId, bookingId, amount, taxAmount, discountAmount, status, createdAt}` |
| 37 | PUT | `/{billId}/status` | Update bill status | Query: `status=PENDING\|PAID\|CANCELLED` | `{id, customerId, status, updatedAt, message}` |
| 38 | DELETE | `/{billId}` | Delete bill | None | `{message: "Bill deleted successfully", deletedBillId}` |

---

### 1️⃣2️⃣ ComplaintController
**Base Path:** `/api/complaints`  
**Authentication Required:** Varies by endpoint

| # | Method | Endpoint | Description | Auth | Request | Response |
|---|--------|----------|-------------|------|---------|----------|
| 39 | POST | (base) | Raise complaint | CUSTOMER | `{customerId, description}` | `{id, customerId, description, status: OPEN, priority: MEDIUM, createdAt, message}` |
| 40 | GET | (base) | Get complaints | ADMIN | Query: `status=OPEN\|IN_PROGRESS\|RESOLVED\|CLOSED` (optional) | `[{id, customerId, customerName, description, status, priority, createdAt}]` |
| 41 | GET | `/{id}` | Get complaint by ID | ADMIN/Owner | None | `{id, customerId, customerName, customerEmail, customerPhone, bookingId, description, status, priority, createdAt, updatedAt, resolution, assignedTo, attachments}` |
| 42 | GET | `/admin` | Get all complaints | ADMIN/STAFF | None | `[{id, customerId, customerName, bookingId, description, status, priority, createdAt, updatedAt, resolution, assignedTo}]` |
| 43 | GET | `/customer/{customerId}` | Get customer complaints | CUSTOMER/ADMIN | None | `[{id, customerId, bookingId, description, status, priority, createdAt, updatedAt, resolution}]` |
| 44 | PUT | `/{id}/status` | Update complaint status | ADMIN/STAFF | `{status}` | `{id, customerId, status, updatedAt, message}` |
| 45 | PUT | `/admin/{complaintId}/resolve` | Resolve complaint | ADMIN/STAFF | `{resolution}` | `{id, customerId, status: RESOLVED, resolution, resolvedAt, resolvedBy, message}` |

---

## 🔐 AUTHENTICATION DETAILS

### JWT Token Structure
```json
{
  "id": "user_id",
  "username": "username",
  "email": "user@example.com",
  "role": "CUSTOMER|ADMIN|STAFF",
  "iat": "token_issued_at",
  "exp": "token_expiration"
}
```

### Authorization Header Format
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Role Permissions Summary
| Endpoint | CUSTOMER | ADMIN | STAFF |
|----------|----------|-------|-------|
| Customer Registration | ✅ | - | - |
| Room Browsing | ✅ | ✅ | - |
| Create Booking | ✅ | ✅ | - |
| Cancel Own Booking | ✅ | ✅ | - |
| Confirm Booking | - | ✅ | - |
| User Management | - | ✅ | - |
| Room Management | - | ✅ | - |
| View All Bookings | - | ✅ | - |
| Complaint Management | ✅ (own) | ✅ | ✅ |
| Payment Processing | ✅ | ✅ | - |

---

## 📋 REQUEST/RESPONSE EXAMPLES

### Example 1: Customer Login
```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "password123"
  }'
```

**Response (200):**
```json
{
  "id": 1,
  "username": "johndoe",
  "email": "john@example.com",
  "role": "CUSTOMER",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### Example 2: Create Booking
```bash
curl -X POST http://localhost:8080/api/bookings \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {token}" \
  -d '{
    "customerId": 1,
    "roomId": 5,
    "checkinDate": "2024-02-01",
    "checkoutDate": "2024-02-05"
  }'
```

**Response (201):**
```json
{
  "id": 10,
  "customerId": 1,
  "roomId": 5,
  "checkInDate": "2024-02-01",
  "checkOutDate": "2024-02-05",
  "totalPrice": 18000,
  "status": "PENDING",
  "createdAt": "2024-01-25T10:30:00Z",
  "message": "Room booked successfully"
}
```

---

### Example 3: Search Rooms
```bash
curl -X GET "http://localhost:8080/api/rooms/search?checkInDate=2024-02-01&checkOutDate=2024-02-05&type=DELUXE&maxPrice=5000" \
  -H "Content-Type: application/json"
```

**Response (200):**
```json
[
  {
    "id": 2,
    "roomNumber": "102",
    "type": "DELUXE",
    "price": 4500,
    "amenities": ["WiFi", "AC", "TV", "Mini Bar"],
    "occupancy": 2,
    "status": "AVAILABLE",
    "availability": true
  },
  {
    "id": 3,
    "roomNumber": "103",
    "type": "DELUXE",
    "price": 4500,
    "amenities": ["WiFi", "AC", "TV", "Gym Access"],
    "occupancy": 2,
    "status": "AVAILABLE",
    "availability": true
  }
]
```

---

### Example 4: Update Room Status
```bash
curl -X PUT "http://localhost:8080/api/admin/rooms/5/status?status=MAINTENANCE" \
  -H "Authorization: Bearer {token}"
```

**Response (200):**
```json
{
  "id": 5,
  "roomNumber": "105",
  "status": "MAINTENANCE",
  "updatedAt": "2024-01-25T11:30:00Z",
  "message": "Room status updated successfully"
}
```

---

## ✅ HTTP STATUS CODES

| Code | Meaning | Use Case |
|------|---------|----------|
| 200 | OK | Successful GET, PUT, DELETE |
| 201 | Created | Successful POST (resource created) |
| 204 | No Content | Successful DELETE (no content) |
| 400 | Bad Request | Validation error, missing required fields |
| 401 | Unauthorized | Missing or invalid authentication token |
| 403 | Forbidden | Authenticated but insufficient permissions |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate resource, constraint violation |
| 500 | Internal Server Error | Server error, database error |

---

## 🎯 COMMON VALIDATION PATTERNS

### Email Format
```
Format: user@domain.com
Validation: RFC 5322 compliant
```

### Phone Number
```
Format: 10 digits only
Example: 9876543210
Validation: ^[0-9]{10}$
```

### Date Format
```
Format: YYYY-MM-DD
Example: 2024-01-25
Validation: ISO 8601 compliant
```

### Password Requirements
```
Minimum Length: 6 characters
Recommended: Include uppercase, lowercase, numbers, special chars
```

### Username Requirements
```
Length: 5+ characters
Characters: Alphanumeric and underscore only
Format: ^[a-zA-Z0-9_]{5,}$
```

---

## 🚀 DEPLOYMENT NOTES

### Environment Setup
1. Database must be configured (Derby/MySQL/PostgreSQL)
2. JWT secret key configured
3. CORS enabled for frontend domain
4. Spring Security configured
5. Server port configured (default: 8080)

### Testing
1. Use Postman or cURL for endpoint testing
2. Include Authorization header for protected endpoints
3. Test with valid and invalid inputs
4. Verify HTTP status codes
5. Check response payload structure

### Performance Considerations
1. Implement pagination for list endpoints (future enhancement)
2. Add caching for frequently accessed data
3. Optimize database queries with proper indexing
4. Monitor API response times

---

## 📞 SUPPORT

**Issues/Bugs:** Report with endpoint, method, and error details  
**Feature Requests:** Document with use case and expected behavior  
**Documentation:** Refer to API_IMPLEMENTATION_SUMMARY.md

---

**Version:** 1.0  
**Last Updated:** January 25, 2026  
**Status:** Production Ready ✅
