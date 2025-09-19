# Data Flow Diagram (DFD) for the Airbnb Clone Backend

This diagram illustrates the flow of data between external entities, processes, and data stores within the backend system.

## 1. External Entities

* Guest: An unauthenticated or authenticated user browsing and booking properties.

* Host: An authenticated user who owns and manages property listings.

* Admin: An authenticated user with system-wide management privileges.

* Payment Gateway: An external service (e.g., Stripe, PayPal) that handles all payment transactions.

## 2. Processes (The System)

* P1: User Authentication & Profile Management: Handles user registration, login, and profile updates.

* P2: Property Listings Management: Manages the creation, editing, and deletion of property listings.

* P3: Search & Booking: Processes property search queries and manages booking requests.

* P4: Payment Processing: Manages secure payment transactions and payouts.

* P5: Reviews & Messages: Handles all communication and feedback between users.

* P6: Notifications & Reporting: Sends notifications to users and generates reports for the Admin.

## 3. Data Stores

* DS1: Users Database: Stores all user-related information.

* DS2: Properties Database: Stores all property listings and their details.

* DS3: Bookings Database: Stores all booking-related information.

* DS4: Payments Database: Stores payment transaction records.

* DS5: Reviews & Messages Database: Stores all reviews and user-to-user messages.

## 4. Data Flow
### A. User Authentication & Profile Management

* Guest/Host → P1: Login/Registration Data

* P1 → DS1: Store User Data

* DS1 → P1: User Profile Data

* P1 → Guest/Host: Login Confirmation/Profile Status

* Guest/Host → P1: Profile Update Request

* P1 → DS1: Update User Data

### B. Property Management

* Host → P2: Property Listing Details (e.g., title, description, price)

* P2 → DS2: Store Property Data

* DS2 → P2: Property Data (for editing/deleting)

* P2 → Host: Listing Confirmation

### C. Search & Booking

* Guest → P3: Search Query (location, dates, amenities)

* P3 → DS2: Retrieve Property Data

* DS2 → P3: Filtered Property Listings

* P3 → Guest: Search Results

* Guest → P3: Booking Request (property ID, dates)

* P3 → DS3: Store Booking Data

* P3 → Guest: Booking Confirmation

* P3 → Host: Booking Notification

### D. Payment Processing

* P3 → P4: Payment Request (amount, booking details)

* P4 → Payment Gateway: Charge Request

* Payment Gateway → P4: Transaction Status (success/failure)

* P4 → DS4: Store Payment Record

* P4 → P3: Payment Confirmation

* P4 → Host: Payout Request

### E. Reviews & Messages

* Guest/Host → P5: Review/Message Content

* P5 → DS5: Store Content

* P5 → Guest/Host: Content Submission Confirmation

* DS5 → P5: Retrieve Messages/Reviews

* P5 → Guest/Host: Display Messages/Reviews

### F. Notifications & Admin

* P3/P4/P5 → P6: Notification Trigger (e.g., new booking, payment)

* P6 → Guest/Host: Send Notification

* Admin → P6: Reporting Request

* P6 → DS1/DS2/DS3/DS4: Retrieve All Data

* DS1/DS2/DS3/DS4 → P6: Raw Data

* P6 → Admin: System Reports