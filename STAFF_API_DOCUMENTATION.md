# Staff Management API Documentation

## Overview
This document describes all available API endpoints for staff management in the Hotel Management System.

## 🔐 Staff Registration & Authentication

### Important Security Rules
- ✅ **Staff can ONLY be registered by admin** through `/api/admin/users` endpoint
- ❌ **Staff CANNOT self-register** through public endpoints
- ✅ Public registration endpoints automatically block "STAFF" role
- ✅ Designation is mandatory when creating staff users

---

## Authentication Endpoints

### 1. Staff Login
**Endpoint:** `POST /api/auth/staff/login`  
**Description:** Dedicated login endpoint for staff members that returns complete staff information.  
**Request Body:**
```json
{
  "username": "johndoe",
  "password": "password123"
}
```

**Response:**
```json
{
  "userId": 5,
  "name": "John Doe",
  "email": "john.doe@hotel.com",
  "username": "johndoe",
  "role": "STAFF",
  "status": "ACTIVE",
  "staffId": 1,
  "designation": "Front Desk Manager"
}
```

### 2. Admin Login (Staff can also use this)
**Endpoint:** `POST /api/auth/admin/login`  
**Description:** General admin/staff login endpoint.  
**Request/Response:** Returns basic User object

---

## Staff Registration (Admin Only)

### Create Staff User
**Endpoint:** `POST /api/admin/users`  
**Description:** Admin creates a new staff member. This is the ONLY way to register staff.  
**Request Body:**
```json
{
  "name": "Jane Smith",
  "email": "jane.smith@hotel.com",
  "username": "janesmith",
  "password": "securepass123",
  "role": "STAFF",
  "designation": "Front Desk Manager"
}
```

**Important:** 
- `role` must be "STAFF"
- `designation` is **required** when role is STAFF
- Email and username must be unique

**Response:**
```json
{
  "message": "User created successfully"
}
```

---

## Staff Endpoints (General Access)

### 1. Get All Staff
**Endpoint:** `GET /api/staff`  
**Description:** Retrieve a list of all staff members with their user details.  
**Response:**
```json
[
  {
    "id": 1,
    "userId": 5,
    "designation": "Front Desk Manager",
    "name": "John Doe",
    "email": "john.doe@hotel.com",
    "username": "johndoe",
    "status": "ACTIVE"
  }
]
```

### 2. Get Staff by ID
**Endpoint:** `GET /api/staff/{id}`  
**Description:** Retrieve specific staff member details by staff ID.  
**Path Parameter:**
- `id` (integer) - Staff ID

**Response:**
```json
{
  "id": 1,
  "userId": 5,
  "designation": "Front Desk Manager",
  "name": "John Doe",
  "email": "john.doe@hotel.com",
  "username": "johndoe",
  "status": "ACTIVE"
}
```

### 3. Get Staff by User ID
**Endpoint:** `GET /api/staff/user/{userId}`  
**Description:** Retrieve staff details by user ID.  
**Path Parameter:**
- `userId` (integer) - User ID

**Response:** Same as Get Staff by ID

### 4. Update Staff Designation
**Endpoint:** `PUT /api/staff/{id}`  
**Description:** Update the designation of a staff member.  
**Path Parameter:**
- `id` (integer) - Staff ID

**Request Body:**
```json
{
  "designation": "Senior Front Desk Manager"
}
```

**Response:**
```json
{
  "message": "Staff designation updated successfully"
}
```

### 5. Delete Staff
**Endpoint:** `DELETE /api/staff/{id}`  
**Description:** Delete a staff member record.  
**Path Parameter:**
- `id` (integer) - Staff ID

**Response:**
```json
{
  "message": "Staff deleted successfully",
  "deletedStaffId": "1"
}
```

---

## Admin Staff Endpoints (Admin Access Only)

### 1. Get All Staff (Admin)
**Endpoint:** `GET /api/admin/staff`  
**Description:** Admin view of all staff members.  
**Response:** Same as general GET /api/staff

### 2. Get Staff by ID (Admin)
**Endpoint:** `GET /api/admin/staff/{id}`  
**Description:** Admin view of specific staff member.  
**Response:** Same as general GET /api/staff/{id}

### 3. Update Staff Designation (Admin)
**Endpoint:** `PUT /api/admin/staff/{id}`  
**Description:** Admin-only endpoint to update staff designation.  
**Request/Response:** Same as general PUT /api/staff/{id}

### 4. Delete Staff (Admin)
**Endpoint:** `DELETE /api/admin/staff/{id}`  
**Description:** Admin-only endpoint to delete staff.  
**Request/Response:** Same as general DELETE /api/staff/{id}

### 5. Get Staff Statistics
**Endpoint:** `GET /api/admin/staff/statistics`  
**Description:** Retrieve statistical information about staff members.  
**Response:**
```json
{
  "totalStaff": 10,
  "activeStaff": 8,
  "inactiveStaff": 2,
  "designationCounts": {
    "Front Desk Manager": 3,
    "Housekeeping Supervisor": 2,
    "Concierge": 2,
    "Maintenance Staff": 3
  }
}
```

---

## Common Designations

Examples of staff designations in a hotel:
- Front Desk Manager
- Receptionist
- Housekeeping Supervisor
- Housekeeper
- Concierge
- Bellhop
- Maintenance Staff
- Security Officer
- Restaurant Manager
- Chef
- Waiter/Waitress

---

## Error Responses

All endpoints may return the following error responses:

### Staff Not Found
```json
{
  "message": "Staff not found with id: 1"
}
```

### User Not Found
```json
{
  "message": "User not found for staff"
}
```

### Invalid Designation
```json
{
  "message": "Designation is required"
}
```

### Staff Self-Registration Blocked
```json
{
  "message": "Staff registration must be done by admin"
}
```

### Designation Required
```json
{
  "message": "Designation is required for staff members"
}
```

### Invalid Staff Credentials
```json
{
  "message": "Invalid credentials for staff login"
}
```

---

## Security Features

### 1. Staff Registration Protection
- Public registration endpoints (`/api/user/register`, `/api/customer/register`) automatically reject any request with role "STAFF"
- Only admin endpoint `/api/admin/users` can create staff users
- Designation validation ensures all staff have proper designation

### 2. Staff Login Validation
- `/api/auth/staff/login` verifies user has "STAFF" role
- Returns comprehensive staff information including designation
- Passwords are hashed using secure encryption

### 3. Database Constraints
- `USER_ID` is UNIQUE and NOT NULL in STAFF table
- `DESIGNATION` is NOT NULL
- Foreign key with CASCADE DELETE automatically removes staff when user is deleted

---

## Workflow Examples

### Complete Staff Onboarding Workflow

1. **Admin creates staff account:**
```bash
POST /api/admin/users
{
  "name": "John Doe",
  "email": "john@hotel.com",
  "username": "johndoe",
  "password": "pass123",
  "role": "STAFF",
  "designation": "Front Desk Manager"
}
```

2. **Staff logs in:**
```bash
POST /api/auth/staff/login
{
  "username": "johndoe",
  "password": "pass123"
}
```

3. **Get staff profile:**
```bash
GET /api/staff/user/5
```

4. **Update designation (if promoted):**
```bash
PUT /api/admin/staff/1
{
  "designation": "Senior Front Desk Manager"
}
```

---

## Notes

1. **Creating Staff**: Staff members can ONLY be created through the admin user creation endpoint. Public endpoints will reject staff role.

2. **Authentication**: Staff should use `/api/auth/staff/login` for login to get complete staff information including designation.

3. **CORS**: All endpoints have CORS enabled with `@CrossOrigin` annotation.

4. **Data Relationships**: Each staff record is linked to a user record via `userId`. The staff endpoints automatically fetch and include user details in the response.

5. **Cascade Deletion**: When a user is deleted, the associated staff record is automatically deleted due to `ON DELETE CASCADE` constraint.

6. **Designation Management**: Designation can be updated through the staff update endpoints without affecting user information.
