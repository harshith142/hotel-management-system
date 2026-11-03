# 🎯 QUICK START - API ENDPOINTS FOR FRONTEND

**Base URL:** `http://localhost:8080/api`

---

## 🔗 COPY-PASTE READY ENDPOINTS

### Authentication
```
POST   /auth/login              → Login as customer
POST   /auth/admin/login        → Login as admin/staff
```

### User Management
```
POST   /users                   → Create user (ADMIN)
POST   /staff                   → Create staff (ADMIN)
GET    /admin/users             → Get all users (ADMIN)
DELETE /admin/users/:userId     → Delete user (ADMIN)
```

### Customer
```
POST   /customers/register      → Register customer
PUT    /customers/profile       → Update profile
```

### Rooms
```
GET    /rooms                   → All rooms
GET    /rooms/:id               → Room details
GET    /rooms/search            → Search rooms (with filters)
GET    /rooms/available         → Available rooms
POST   /admin/rooms             → Create room (ADMIN)
POST   /admin/rooms/bulk        → Bulk create (ADMIN)
PUT    /admin/rooms/:id         → Update room (ADMIN)
PUT    /admin/rooms/:id/status  → Update status (ADMIN)
DELETE /admin/rooms/:id         → Delete room (ADMIN)
```

### Bookings
```
POST   /bookings                → Create booking
GET    /bookings/customer/:id   → My bookings
GET    /bookings/history/:id    → Booking history
GET    /bookings/room/:id       → Room bookings
PUT    /bookings/:id/confirm    → Confirm (ADMIN)
PUT    /bookings/:id/cancel     → Cancel
DELETE /bookings/:id            → Delete
GET    /admin/bookings          → All bookings (ADMIN)
GET    /admin/bookings/revenue  → Revenue (ADMIN)
```

### Payments
```
POST   /payments/pay            → Pay bill
GET    /payments/customer/:id   → My payments
GET    /payments/:id            → Payment details
POST   /admin/payments          → Create payment (ADMIN)
GET    /admin/payments          → All payments (ADMIN)
GET    /admin/payments/:id      → Payment by ID (ADMIN)
```

### Bills
```
POST   /admin/bills             → Create bill (ADMIN)
GET    /admin/bills             → All bills (ADMIN)
GET    /admin/bills/:id         → Bill details (ADMIN)
PUT    /admin/bills/:id/status  → Update status (ADMIN)
DELETE /admin/bills/:id         → Delete bill (ADMIN)
```

### Complaints
```
POST   /complaints              → Raise complaint
GET    /complaints              → Get complaints
GET    /complaints/:id          → Complaint details
GET    /complaints/admin        → All complaints (ADMIN)
GET    /complaints/customer/:id → Customer complaints
PUT    /complaints/:id/status   → Update status (ADMIN)
PUT    /complaints/admin/:id/resolve → Resolve (ADMIN)
```

---

## 📡 ANGULAR SERVICE TEMPLATE

```typescript
import { Injectable } from '@angular/core';
import { HttpClient, HttpParams } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private baseUrl = 'http://localhost:8080/api';

  constructor(private http: HttpClient) { }

  // Authentication
  loginCustomer(credentials: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/auth/login`, credentials);
  }

  loginAdmin(credentials: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/auth/admin/login`, credentials);
  }

  // Rooms
  getAllRooms(): Observable<any[]> {
    return this.http.get<any[]>(`${this.baseUrl}/rooms`);
  }

  getRoomById(id: number): Observable<any> {
    return this.http.get(`${this.baseUrl}/rooms/${id}`);
  }

  searchRooms(params: any): Observable<any[]> {
    let httpParams = new HttpParams();
    for (let key in params) {
      if (params[key]) {
        httpParams = httpParams.set(key, params[key]);
      }
    }
    return this.http.get<any[]>(`${this.baseUrl}/rooms/search`, { params: httpParams });
  }

  // Bookings
  createBooking(booking: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/bookings`, booking);
  }

  getMyBookings(customerId: number): Observable<any[]> {
    return this.http.get<any[]>(`${this.baseUrl}/bookings/customer/${customerId}`);
  }

  confirmBooking(bookingId: number): Observable<any> {
    return this.http.put(`${this.baseUrl}/bookings/${bookingId}/confirm`, {});
  }

  cancelBooking(bookingId: number): Observable<any> {
    return this.http.put(`${this.baseUrl}/bookings/${bookingId}/cancel`, {});
  }

  // Customers
  registerCustomer(customer: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/customers/register`, customer);
  }

  updateProfile(profile: any): Observable<any> {
    return this.http.put(`${this.baseUrl}/customers/profile`, profile);
  }

  // Complaints
  raiseComplaint(complaint: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/complaints`, complaint);
  }

  getMyComplaints(customerId: number): Observable<any[]> {
    return this.http.get<any[]>(`${this.baseUrl}/complaints/customer/${customerId}`);
  }

  // Payments
  processPayment(payment: any): Observable<any> {
    return this.http.post(`${this.baseUrl}/payments/pay`, payment);
  }

  // Add more methods as needed...
}
```

---

## 🔑 INTERCEPTOR TEMPLATE

```typescript
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = localStorage.getItem('token');

    if (token) {
      const clonedReq = req.clone({
        headers: req.headers.set('Authorization', `Bearer ${token}`)
      });
      return next.handle(clonedReq);
    }

    return next.handle(req);
  }
}
```

---

## 🧪 TESTING REQUESTS

### Using cURL

**Login:**
```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"user","password":"pass"}'
```

**Get Rooms:**
```bash
curl -X GET http://localhost:8080/api/rooms
```

**Create Booking:**
```bash
curl -X POST http://localhost:8080/api/bookings \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN_HERE" \
  -d '{
    "customerId":1,
    "roomId":5,
    "checkinDate":"2024-02-01",
    "checkoutDate":"2024-02-05"
  }'
```

**Search Rooms:**
```bash
curl -X GET "http://localhost:8080/api/rooms/search?checkInDate=2024-02-01&checkOutDate=2024-02-05&type=DELUXE&maxPrice=5000"
```

---

## 📋 COMMON REQUEST BODIES

### Customer Registration
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

### Create Booking
```json
{
  "customerId": 1,
  "roomId": 5,
  "checkinDate": "2024-02-01",
  "checkoutDate": "2024-02-05"
}
```

### Process Payment
```json
{
  "billId": 10,
  "paymentMode": "CREDIT_CARD"
}
```

### Raise Complaint
```json
{
  "customerId": 1,
  "description": "Room was not clean"
}
```

### Create Room
```json
{
  "roomNumber": "101",
  "type": "DELUXE",
  "price": 4500,
  "amenities": ["WiFi", "AC", "TV"],
  "occupancy": 2
}
```

---

## ✅ TOTAL ENDPOINTS: 51

- Authentication: 2
- User Management: 4
- Customer: 2
- Rooms: 9
- Bookings: 9
- Payments: 6
- Bills: 5
- Complaints: 7
- Admin Booking: 2

---

**Status:** ✅ All APIs Ready  
**Last Updated:** January 25, 2026
