# 📘 Backend Requirements Specification - Airbnb Clone

This document outlines the functional and technical requirements for key backend features in the Airbnb Clone project.

---

## 🔐 1. User Authentication

### ✅ Functional Requirements
- Allow users to register with a unique email and secure password.
- Provide login/logout functionality using JWT-based sessions.
- Enable password reset via email.

### 🔁 API Endpoints

| Method | Endpoint           | Description            |
|--------|--------------------|------------------------|
| POST   | `/api/auth/signup` | Register a new user    |
| POST   | `/api/auth/login`  | Authenticate user      |
| POST   | `/api/auth/logout` | Log out authenticated user |
| POST   | `/api/auth/reset-password` | Send password reset link |
| POST   | `/api/auth/new-password`   | Submit new password |

### 📥 Input Specifications
- **Email**: Valid email format.
- **Password**: Min. 8 characters, 1 uppercase, 1 lowercase, 1 number.

### 📤 Output
- Success: 200 OK with user info and JWT token.
- Failure: 400 with validation error or 401 for authentication failure.

### 🧪 Validation Rules
- Check for existing email.
- Hash passwords using bcrypt.
- Use rate limiting on login attempts.

### ⚙️ Performance Criteria
- Registration and login responses within 500ms.
- JWT expiration: 24 hours.

---

## 🏘️ 2. Property Management

### ✅ Functional Requirements
- Hosts can create, update, or delete property listings.
- Guests can browse all available listings.

### 🔁 API Endpoints

| Method | Endpoint              | Description              |
|--------|-----------------------|--------------------------|
| POST   | `/api/properties`     | Create a property        |
| GET    | `/api/properties`     | List all properties      |
| GET    | `/api/properties/:id` | View specific property   |
| PUT    | `/api/properties/:id` | Update property info     |
| DELETE | `/api/properties/:id` | Delete a property listing |

### 📥 Input Specifications
- **Title**, **description**, **location**, **price**, **images[]**, **amenities[]**, **availability_dates[]**

### 📤 Output
- Success: 200 with JSON property object.
- Failure: 400 (validation) or 403 (unauthorized access).

### 🧪 Validation Rules
- Title and description are required.
- Price must be a positive number.
- Only authenticated users can create or edit.

### ⚙️ Performance Criteria
- Listings endpoint must support pagination and filtering.
- Average response time under 800ms.

---

## 📆 3. Booking System

### ✅ Functional Requirements
- Users can book available properties for a specific date range.
- Users can cancel their bookings.
- Prevent double-booking of the same property.

### 🔁 API Endpoints

| Method | Endpoint             | Description             |
|--------|----------------------|-------------------------|
| POST   | `/api/bookings`      | Make a new booking      |
| GET    | `/api/bookings`      | View user bookings      |
| GET    | `/api/bookings/:id`  | View single booking     |
| DELETE | `/api/bookings/:id`  | Cancel a booking        |

### 📥 Input Specifications
- **property_id**, **start_date**, **end_date**, **number_of_guests**

### 📤 Output
- Success: 200 with booking confirmation.
- Failure: 409 (date conflict), 400 (validation), or 401 (unauthenticated).

### 🧪 Validation Rules
- Date range must not overlap existing bookings.
- Start date must be in the future.
- Only the booking user can cancel.

### ⚙️ Performance Criteria
- Prevent race conditions with atomic transactions.
- Bookings processed within 1 second.

---

## 📦 Notes

- All endpoints follow RESTful conventions.
- Responses are in JSON.
- Authentication is required for protected endpoints using bearer tokens.
