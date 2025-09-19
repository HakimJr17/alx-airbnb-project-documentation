# Backend Requirements Specification

* This document details the technical requirements for the Airbnb clone backend. It outlines the API endpoints, data validation rules, and performance criteria for each core functionality, serving as a guide for development and testing.

## 1. User Management

### A. User Registration

* API Endpoint: POST /api/users/register

* Description: Allows a new user to register as a guest or a host.

* Request Body:

  * firstName (string, required)

  * lastName (string, required)

  * email (string, required)

  * password (string, required)

  * phoneNumber (string, optional)

  * role (string, required, enum: guest, host)

* Response (Success):

  * Status Code: 201 Created

  * Body: { "user_id": "uuid", "email": "string", "role": "string" }

* Response (Error):

  * Status Code: 409 Conflict (if email already exists)

  * Status Code: 400 Bad Request (for validation errors)

* Validation Rules:

 * email must be a valid email format.

 * password must be at least 8 characters long.

 * role must be either guest or host.

 * firstName and lastName cannot be empty.

* Performance: Response time must be under 200ms.

### B. User Login

* API Endpoint: POST /api/users/login

* Description: Authenticates a user and returns a JWT for subsequent requests.

* Request Body:

  * email (string, required)

  * password (string, required)

* Response (Success):

  * Status Code: 200 OK

  * Body: { "user_id": "uuid", "token": "jwt_token" }

* Response (Error):

  * Status Code: 401 Unauthorized (for invalid credentials)

* Validation Rules:

  * email and password are required.

* Performance: Response time must be under 150ms.

## 2. Property Listings Management

### A. Add Listing

* API Endpoint: POST /api/properties

* Authentication: Requires a host JWT.

* Description: Allows a host to create a new property listing.

* Request Body:

  * name (string, required)

  * description (string, optional)

  * location (string, required)

  * pricePerNight (decimal, required)

  * amenities (array of strings, optional)

  * images (array of file uploads/URLs)

* Response (Success):

  * Status Code: 201 Created

  * Body: { "property_id": "uuid", "message": "Property created successfully" }

* Validation Rules:

  * name and location cannot be empty.

  * pricePerNight must be a positive number.

* Performance: Response time must be under 500ms (to account for image uploads).

### B. Get All Listings
* API Endpoint: GET /api/properties

* Description: Retrieves a list of all active property listings.

* Response (Success):

  * Status Code: 200 OK

  * Body: [ { "property_id": "uuid", "name": "string", "location": "string", "pricePerNight": "decimal", ... }, ... ]

* Performance: Response time must be under 300ms.

## 3. Booking System

### A. Create Booking

* API Endpoint: POST /api/bookings

* Authentication: Requires a guest JWT.

* Description: Allows a guest to book a property for specific dates.

* Request Body:

  * property_id (uuid, required)

  * startDate (date, required, format: YYYY-MM-DD)

  * endDate (date, required, format: YYYY-MM-DD)

* Response (Success):

  * Status Code: 201 Created

  * Body: { "booking_id": "uuid", "status": "pending" }

* Validation Rules:

  * startDate must be before endDate.

  * Dates cannot be in the past.

  * Check for date conflicts to prevent double-bookings.

* Performance: Response time must be under 250ms.

### B. Get User's Bookings

* API Endpoint: GET /api/users/{user_id}/bookings

* Authentication: Requires a guest or host JWT.

* Description: Retrieves all bookings associated with a specific user.

* Response (Success):

  * Status Code: 200 OK

  * Body: [ { "booking_id": "uuid", "property_id": "uuid", "startDate": "date", "status": "string", ... }, ... ]

* Performance: Response time must be under 300ms.

## 4. Payments

### A. Process Payment

* API Endpoint: POST /api/payments

* Authentication: Requires a guest JWT.

* Description: Initiates a payment for a booking via a payment gateway.

* Request Body:

  * booking_id (uuid, required)

  * amount (decimal, required)

  * paymentMethod (string, required, e.g., "credit_card", "paypal")

* Response (Success):

  * Status Code: 200 OK

  * Body: { "payment_id": "uuid", "message": "Payment successful" }

* Response (Error):

  * Status Code: 400 Bad Request (invalid input)

  * Status Code: 500 Internal Server Error (payment gateway failure)

* Validation Rules:

  * booking_id must be a valid, existing booking.

  * amount must match the booking's total_price.

* Performance: Response time must be under 1 second (due to external service call).

## 5. Reviews and Ratings

### A. Leave a Review

* API Endpoint: POST /api/properties/{property_id}/reviews

* Authentication: Requires a guest JWT.

* Description: Allows a guest to leave a review and rating for a property they have booked.

* Request Body:

  * rating (integer, required)

  * comment (string, required)

* Response (Success):

  * Status Code: 201 Created

  * Body: { "review_id": "uuid", "message": "Review submitted successfully" }

* Validation Rules:

  * rating must be an integer between 1 and 5.

  * comment cannot be empty.

  * The user must have a completed booking for the property to leave a review.

* Performance: Response time must be under 200ms.