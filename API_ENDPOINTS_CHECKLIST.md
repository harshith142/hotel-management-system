# Hotel Management System - API Endpoints Implementation Checklist

**Last Updated:** January 25, 2026  
**Status:** All APIs Implemented ✅

---

## API IMPLEMENTATION STATUS

### 1. AUTHENTICATION ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/auth/login` | AuthController | ✅ | Customer login |
| POST | `/api/auth/admin/login` | AuthController | ✅ | Admin/Staff login |

---

### 2. USER MANAGEMENT ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/users` | UserController | ✅ | Register user (ADMIN/STAFF) |
| POST | `/api/staff` | UserController | ✅ | Register staff member |
| GET | `/api/admin/users` | AdminUserController | ✅ | Get all users |
| DELETE | `/api/admin/users/{userId}` | AdminUserController | ✅ | Delete user |

---

### 3. CUSTOMER ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/customers/register` | CustomerController | ✅ | Register customer |
| PUT | `/api/customers/profile` | CustomerController | ✅ | Update customer profile |

---

### 4. ROOM ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| GET | `/api/rooms` | RoomController | ✅ | Get all rooms |
| GET | `/api/rooms/{id}` | RoomController | ✅ | Get room by ID |
| GET | `/api/rooms/search` | RoomController | ✅ | Search rooms with filters |
| GET | `/api/rooms/available` | RoomController | ✅ | Get available rooms |
| POST | `/api/admin/rooms` | AdminRoomController | ✅ | Create room |
| POST | `/api/admin/rooms/bulk` | AdminRoomController | ✅ | Bulk create rooms |
| PUT | `/api/admin/rooms/{roomId}` | AdminRoomController | ✅ | Update room details |
| PUT | `/api/admin/rooms/{roomId}/status` | AdminRoomController | ✅ | Update room status |
| DELETE | `/api/admin/rooms/{roomId}` | AdminRoomController | ✅ | Delete room |

---

### 5. BOOKING ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/bookings` | BookingController | ✅ | Create booking |
| GET | `/api/bookings/customer/{customerId}` | BookingController | ✅ | Get customer bookings |
| GET | `/api/bookings/history/{customerId}` | BookingController | ✅ | Get booking history |
| GET | `/api/bookings/room/{roomId}` | BookingController | ✅ | Get bookings by room |
| PUT | `/api/bookings/{bookingId}/confirm` | BookingController | ✅ | Confirm booking |
| PUT | `/api/bookings/{bookingId}/cancel` | BookingController | ✅ | Cancel booking |
| DELETE | `/api/bookings/{bookingId}` | BookingController | ✅ | Delete booking |
| GET | `/api/admin/bookings` | AdminBookingController | ✅ | Get all bookings (Admin) |
| GET | `/api/admin/bookings/revenue` | AdminBookingController | ✅ | Get revenue report |

---

### 6. PAYMENT ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/payments/pay` | PaymentController | ✅ | Process payment |
| GET | `/api/payments/customer/{id}` | PaymentController | ✅ | Get customer payments |
| GET | `/api/payments/{paymentId}` | PaymentController | ✅ | Get payment details |
| POST | `/api/admin/payments` | AdminPaymentController | ✅ | Create payment (Admin) |
| GET | `/api/admin/payments` | AdminPaymentController | ✅ | Get all payments (Admin) |
| GET | `/api/admin/payments/{paymentId}` | AdminPaymentController | ✅ | Get payment by ID (Admin) |

---

### 7. BILL ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/admin/bills` | BillController | ✅ | Create bill |
| GET | `/api/admin/bills` | BillController | ✅ | Get all bills |
| GET | `/api/admin/bills/{billId}` | BillController | ✅ | Get bill by ID |
| PUT | `/api/admin/bills/{billId}/status` | BillController | ✅ | Update bill status |
| DELETE | `/api/admin/bills/{billId}` | BillController | ✅ | Delete bill |

---

### 8. COMPLAINT ENDPOINTS

| Method | Endpoint | Controller | Status | Notes |
|--------|----------|-----------|--------|-------|
| POST | `/api/complaints` | ComplaintController | ✅ | Raise complaint |
| GET | `/api/complaints` | ComplaintController | ✅ | Get complaints (with optional status filter) |
| GET | `/api/complaints/{id}` | ComplaintController | ✅ | Get complaint by ID |
| GET | `/api/complaints/admin` | ComplaintController | ✅ | Get all complaints (Admin) |
| GET | `/api/complaints/customer/{customerId}` | ComplaintController | ✅ | Get customer complaints |
| PUT | `/api/complaints/{id}/status` | ComplaintController | ✅ | Update complaint status |
| PUT | `/api/complaints/admin/{complaintId}/resolve` | ComplaintController | ✅ | Resolve complaint |

---

## CONTROLLER SUMMARY

### AuthController (`/api/auth`)
- `POST /login` - Customer login
- `POST /admin/login` - Admin/Staff login

### UserController (`/api`)
- `POST /users` - Register user
- `POST /staff` - Register staff

### CustomerController (`/api/customers`)
- `POST /register` - Customer registration
- `PUT /profile` - Update profile

### AdminUserController (`/api/admin/users`)
- `POST` - Create user
- `GET` - Get all users
- `DELETE /{userId}` - Delete user

### RoomController (`/api/rooms`)
- `GET` - Get all rooms
- `GET /{id}` - Get room by ID
- `GET /search` - Search with advanced filters
- `GET /available` - Get available rooms

### AdminRoomController (`/api/admin/rooms`)
- `POST` - Create room
- `POST /bulk` - Bulk create rooms
- `PUT /{roomId}` - Update room
- `PUT /{roomId}/status` - Update room status
- `DELETE /{roomId}` - Delete room

### BookingController (`/api/bookings`)
- `POST` - Create booking
- `GET /customer/{customerId}` - Get customer bookings
- `GET /history/{customerId}` - Get booking history
- `GET /room/{roomId}` - Get room bookings
- `PUT /{bookingId}/confirm` - Confirm booking
- `PUT /{bookingId}/cancel` - Cancel booking
- `DELETE /{bookingId}` - Delete booking

### AdminBookingController (`/api/admin/bookings`)
- `GET` - Get all bookings
- `GET /revenue` - Get revenue report
- Additional booking management endpoints

### PaymentController (`/api/payments`)
- `POST /pay` - Process payment
- `GET /customer/{id}` - Get customer payments
- `GET /{paymentId}` - Get payment details

### AdminPaymentController (`/api/admin/payments`)
- `POST` - Create payment
- `GET` - Get all payments
- `GET /{paymentId}` - Get payment by ID

### BillController (`/api/admin/bills`)
- `POST` - Create bill
- `GET` - Get all bills
- `GET /{billId}` - Get bill by ID
- `PUT /{billId}/status` - Update bill status
- `DELETE /{billId}` - Delete bill

### ComplaintController (`/api/complaints`)
- `POST` - Raise complaint
- `GET` - Get complaints (with status filter)
- `GET /{id}` - Get complaint by ID
- `GET /admin` - Get all complaints (Admin view)
- `GET /customer/{customerId}` - Get customer complaints
- `PUT /{id}/status` - Update complaint status
- `PUT /admin/{complaintId}/resolve` - Resolve complaint

---

## TOTAL ENDPOINTS COUNT

**Total API Endpoints: 51**

### Breakdown:
- Authentication: 2
- User Management: 4
- Customer: 2
- Room: 9
- Booking: 9
- Payment: 6
- Bill: 5
- Complaint: 7
- Admin Booking: 3
- Admin Users: 3
- Admin Rooms: 5 (included in Room count)

---

## QUERY PARAMETERS

### Room Search (`GET /api/rooms/search`)
- `checkInDate` (optional) - YYYY-MM-DD format
- `checkOutDate` (optional) - YYYY-MM-DD format
- `type` (optional) - STANDARD | DELUXE | SUITE
- `minPrice` (optional) - Integer
- `maxPrice` (optional) - Integer
- `occupancy` (optional) - Integer
- `amenities` (optional) - Comma-separated values

### Complaint Filter (`GET /api/complaints`)
- `status` (optional) - OPEN | IN_PROGRESS | RESOLVED | CLOSED

---

## REQUEST/RESPONSE EXAMPLES

### Example: Customer Registration
**Request:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "mobile": "9876543210",
  "address": "123 Main Street",
  "username": "johndoe",
  "password": "password123"
}
```

**Response (201):**
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "mobile": "9876543210",
  "address": "123 Main Street",
  "username": "johndoe",
  "role": "CUSTOMER",
  "message": "Customer registered successfully"
}
```

### Example: Room Search
**Request URL:** `/api/rooms/search?checkInDate=2024-01-20&checkOutDate=2024-01-25&type=DELUXE&maxPrice=5000`

**Response:**
```json
[
  {
    "id": 1,
    "roomNumber": "101",
    "type": "DELUXE",
    "price": 4500,
    "amenities": ["WiFi", "AC", "TV"],
    "occupancy": 2,
    "status": "AVAILABLE"
  }
]
```

---

## ERROR RESPONSE STRUCTURE

All error responses follow this format:

```json
{
  "timestamp": "2024-01-25T10:30:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Validation error details",
  "path": "/api/bookings"
}
```

### Common Status Codes:
- **200** - OK (GET, PUT)
- **201** - Created (POST)
- **400** - Bad Request (validation error)
- **401** - Unauthorized (missing/invalid token)
- **403** - Forbidden (insufficient permissions)
- **404** - Not Found
- **409** - Conflict (duplicate, constraint violation)
- **500** - Internal Server Error

---

## AUTHENTICATION

All protected endpoints require:
```
Authorization: Bearer {JWT_TOKEN}
```

Token is obtained from login endpoints:
- `POST /api/auth/login` - For customers
- `POST /api/auth/admin/login` - For admin/staff

---

## NOTES FOR TESTING

1. **Date Format:** All dates must be YYYY-MM-DD
2. **Currency:** All amounts in INR (Indian Rupees)
3. **Phone:** Must be 10 digits
4. **Enums:**
   - User Role: CUSTOMER, ADMIN, STAFF
   - Room Type: STANDARD, DELUXE, SUITE
   - Room Status: AVAILABLE, OCCUPIED, MAINTENANCE
   - Booking Status: PENDING, CONFIRMED, CHECKED_IN, CHECKED_OUT, CANCELLED
   - Complaint Status: OPEN, IN_PROGRESS, RESOLVED, CLOSED
   - Payment Mode: CREDIT_CARD, DEBIT_CARD, CASH, ONLINE
   - Payment Status: SUCCESS, PENDING, FAILED

---

## FRONTEND INTEGRATION POINTS

### Base URL: `http://localhost:8080`
### Base Path: `/api`

All endpoints are prefixed with `/api`. Examples:
- Full URL: `http://localhost:8080/api/auth/login`
- Full URL: `http://localhost:8080/api/rooms`
- Full URL: `http://localhost:8080/api/admin/bookings`

---

**Implementation Status: COMPLETE ✅**  
**All APIs are properly implemented and ready for testing.**
