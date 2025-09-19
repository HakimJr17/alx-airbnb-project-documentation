# Airbnb Clone Backend
This repository contains the backend for an Airbnb clone, built to handle all server-side logic, database management, and API integrations for a robust and scalable web application.

## 🚀 Core Functionalities
The backend is designed to support the following key features:

1. User Management
User Registration: Allows users to sign up as either admin, guests or hosts, with secure password handling.

User Authentication: Implements secure login using JWT (JSON Web Tokens) for user sessions.

Profile Management: Enables users to view and update their profile information.

2. Property Listings Management
Add Listings: Provides an API for hosts to create new property listings, including details like title, description, location, price, and availability.

Edit/Delete Listings: Allows hosts to modify or remove their existing property listings.

3. Search and Filtering
Advanced Search: Supports searching for properties by location, price range, number of guests, and amenities.

Pagination: Implements pagination to handle large datasets efficiently.

4. Booking Management
Booking Creation: Enables guests to book properties for specific dates, with logic to prevent double bookings.

Booking Cancellation: Supports the cancellation of bookings by either guests or hosts.

Booking Status: Manages and tracks the status of each booking (e.g., pending, confirmed, canceled).

5. Payments
Secure Payment Gateway: Integrates with a payment service to handle upfront payments from guests and payouts to hosts.

6. Reviews and Ratings
Review Submission: Allows guests to leave reviews and ratings for properties they have booked.

Review Moderation: Ensures reviews are linked to specific, completed bookings to prevent abuse.

7. Notifications
Automated Notifications: Sends email and in-app notifications for important events like booking confirmations, cancellations, and payment updates.

8. Admin Dashboard
Administrative Interface: Provides an API for an admin dashboard to monitor and manage users, listings, and bookings.

## 🛠️ Technical Implementation
### Database Schema
The backend uses a relational database (MySQL) with the following key tables. The schema is defined in the schema.sql file.

   1.  users: Stores user information (guests, hosts, admins).

   2.  properties: Stores details for each property listing.

   3.  bookings: Manages property bookings, linking to users and properties.

   4.  payments: Records all payment transactions.

   5.  reviews: Stores user reviews and ratings for properties.

   6.  messages: Handles in-app messaging between users.

### API
The API follows the RESTful API design principles, using standard HTTP methods for all endpoints (GET, POST, PUT/PATCH, DELETE).

### Authentication and Authorization
JWT is used for secure, stateless user sessions. Role-based access control (RBAC) is implemented to ensure that users (guests, hosts, and admins) have the correct permissions.

### File Storage
Property images and user profile photos are stored securely in a dedicated cloud storage solution (e.g., AWS S3 or Cloudinary) to prevent a bloated database.

# ⚙️ Non-Functional Requirements
## Scalability and Performance
The application is designed with a modular architecture to allow for easy scaling. We use techniques like database query optimization and caching to ensure high performance and low latency.

## Security
Sensitive data like passwords are never stored in plain text; they are secured using hashing and encryption. The system is also protected with firewalls and rate limiting to prevent malicious activities.

## Testing
The backend is rigorously tested to ensure functionality and reliability. This includes unit tests for individual components and integration tests for API endpoints.