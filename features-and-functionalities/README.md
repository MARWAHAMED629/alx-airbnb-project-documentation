# 📄 Software Requirements Specification (SRS)

## Project: Airbnb Clone - Backend System

---

## 1. Introduction

### 1.1 Purpose
This document specifies the software requirements for the **Airbnb Clone Backend System**. It defines the functional requirements, system features, and technical constraints to guide the development process.

### 1.2 Scope
The system is designed to simulate the core functionalities of an Airbnb-like platform, focusing on backend services including user management, property listings, bookings, payments, reviews, and administrative controls.

### 1.3 Intended Audience
- Backend Developers  
- Frontend Developers  
- QA Engineers  
- Project Managers  
- Academic Evaluators

### 1.4 Definitions and Acronyms
- **API**: Application Programming Interface  
- **CRUD**: Create, Read, Update, Delete  
- **JWT**: JSON Web Token  
- **SRS**: Software Requirements Specification

---

## 2. Overall Description

### 2.1 Product Perspective
This backend will expose a RESTful API, to be consumed by a frontend web/mobile interface. It is modular in design, separating concerns by domain (users, listings, bookings, etc.).

### 2.2 Product Functions
- User registration and authentication
- Property listing management
- Booking and availability management
- Secure payment integration
- User profile customization
- Review and rating submission
- Administrative controls and logs

### 2.3 User Classes and Characteristics

| User Type | Description |
|-----------|-------------|
| Guest | Can search listings and book properties |
| Host  | Can create and manage listings |
| Admin | Can manage users, listings, and logs |

### 2.4 Operating Environment
- **Backend**: Django / Django REST Framework  
- **Database**: PostgreSQL / MySQL  
- **Auth**: JWT-based authentication  
- **Hosting**: Heroku, AWS, or similar

---

## 3. Functional Requirements

| ID    | Requirement Name        | Description                                                            | Priority | Dependency        |
|-------|--------------------------|------------------------------------------------------------------------|----------|-------------------|
| FR-1  | User Registration        | Allow users to sign up using email and password                        | High     | None              |
| FR-2  | User Login/Logout        | Allow users to login/logout using valid credentials                    | High     | FR-1              |
| FR-3  | Password Reset           | Reset password via email                                               | Medium   | FR-1              |
| FR-4  | Create Listing           | Hosts can add property listings                                        | High     | FR-2              |
| FR-5  | Update/Delete Listing    | Modify or remove their listings                                        | High     | FR-4              |
| FR-6  | View Listings            | Browse available properties                                            | High     | None              |
| FR-7  | Search Properties        | Filter listings by location, price, type, etc.                         | High     | FR-6              |
| FR-8  | Check Availability       | Check if property is available in a date range                         | High     | FR-6              |
| FR-9  | Make Booking             | Book available property                                                | High     | FR-2, FR-8        |
| FR-10 | Cancel Booking           | Cancel upcoming or past bookings                                       | Medium   | FR-9              |
| FR-11 | View Bookings            | See user's booking history                                             | High     | FR-9              |
| FR-12 | Add Payment Method       | Save a payment method (e.g. credit card)                               | High     | FR-2              |
| FR-13 | Process Payment          | Handle payment using external processor                                | High     | FR-12, FR-9       |
| FR-14 | View Payment History     | Review past payments                                                   | Medium   | FR-13             |
| FR-15 | Request Refund           | Request a refund when eligible                                         | Medium   | FR-13             |
| FR-16 | View/Edit Profile        | Manage profile info (name, bio, etc.)                                  | High     | FR-2              |
| FR-17 | Upload Avatar            | Upload profile picture                                                 | Medium   | FR-16             |
| FR-18 | Leave Review             | Submit a review after booking                                          | High     | FR-9              |
| FR-19 | Edit/Delete Review       | Manage previously submitted reviews                                    | Medium   | FR-18             |
| FR-20 | View Property Reviews    | Read reviews on listings                                               | High     | FR-6              |
| FR-21 | Admin: Manage Users      | Admins can promote, deactivate, or remove users                        | High     | FR-1, FR-2        |
| FR-22 | Admin: Manage Listings   | Admins can manage all listings                                         | High     | FR-4, FR-5        |
| FR-23 | Admin: View Logs         | View user actions, logs, and errors                                    | Medium   | All modules       |

---

## 4. Non-Functional Requirements

| ID     | Description                                                                 |
|--------|-----------------------------------------------------------------------------|
| NFR-1  | System shall support at least 100 concurrent users                          |
| NFR-2  | All APIs shall respond within 500ms under normal load                       |
| NFR-3  | Sensitive data shall be stored encrypted and never exposed in plaintext     |
| NFR-4  | All endpoints shall be protected via token-based authentication (JWT)       |
| NFR-5  | System shall have logging for error tracking and debugging                  |

---

## 5. Assumptions and Constraints
- Frontend is developed separately and will consume REST APIs.
- Payment processing is handled via Stripe or PayPal APIs.
- Image uploads use a third-party service (e.g., Cloudinary or AWS S3).
- Emails are sent via SMTP or transactional email services.

---

## 6. Appendices
- ER diagrams, API documentation, and sequence diagrams available upon request.
- Swagger UI will be used for documenting and testing the API.

---
