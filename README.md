# Global Hotel Booking System (v2)

A comprehensive, full-featured API built with FastAPI and PostgreSQL, designed for managing hotel networks, guest registrations, and bookings. Features secure JWT-based authentication with role-based access control (guest/admin), and is thoroughly tested using Postman collections.

## Features

- **Authentication & Authorization**: Secure JWT token-based authentication with distinct guest and administrator roles.
- **Role-Based Access Control**: Different permissions and endpoints accessible based on user roles (e.g., guests can book, admins manage hotels).
- **Database**: Robust PostgreSQL backend for data persistence and integrity.
- **Booking Management**: Comprehensive system to handle room bookings, preventing conflicts (e.g., double-booking the same room or guest booking multiple rooms at overlapping times).
- **Hotel & Room Management**: APIs for managing hotel locations, room types, availability, and details.
- **Guest Management**: APIs for guest registration, profile management, and booking history.
- **API Testing**: Thoroughly tested endpoints using Postman, including authentication flows, role-based access, and booking conflict scenarios.
- **RESTful Design**: Clean, intuitive API endpoints following REST principles.

## Core Endpoints

### Authentication
- `POST /auth/register` - Register a new guest user.
- `POST /auth/login` - Authenticate user and return JWT access token.
- `POST /auth/refresh` - Refresh the access token using a refresh token.
- `POST /auth/logout` - Logout the user (invalidate tokens).

### Users (Guests & Admins)
- `GET /users/me` - Get current user profile (requires authentication).
- `PUT /users/me` - Update current user profile (requires authentication).
- `GET /users/{user_id}` - Get details of a specific user (admin only).

### Hotels
- `GET /hotels` - List all available hotels.
- `GET /hotels/{hotel_id}` - Get details of a specific hotel.
- `POST /hotels` - Create a new hotel (admin only).
- `PUT /hotels/{hotel_id}` - Update a specific hotel (admin only).
- `DELETE /hotels/{hotel_id}` - Delete a specific hotel (admin only).

### Rooms
- `GET /hotels/{hotel_id}/rooms` - List all rooms for a specific hotel.
- `GET /rooms/{room_id}` - Get details of a specific room.
- `POST /hotels/{hotel_id}/rooms` - Add a new room to a hotel (admin only).
- `PUT /rooms/{room_id}` - Update a specific room (admin only).
- `DELETE /rooms/{room_id}` - Remove a specific room (admin only).

### Bookings
- `GET /bookings` - List all bookings for the authenticated user (guest) or all bookings (admin).
- `GET /bookings/{booking_id}` - Get details of a specific booking.
- `POST /bookings` - Create a new booking (requires authentication). **Includes validation to prevent:**
    - **Double-booking the same room** for overlapping dates.
    - **A guest booking multiple rooms** simultaneously (if business rule requires it).
    - **Booking a room that is not available** (e.g., maintenance, already booked).
- `PUT /bookings/{booking_id}` - Update a specific booking (admin only or guest for their own booking within cancellation window).
- `DELETE /bookings/{booking_id}` - Cancel a specific booking (admin only or guest for their own booking within cancellation window).

### Availability (Helper Endpoint)
- `GET /rooms/{room_id}/availability` - Check the availability of a specific room for given dates.

## Potential Project Ideas & Extensions

- **Payment Integration**: Integrate with payment gateways (e.g., Stripe, PayPal) for handling booking payments.
- **Notifications**: Implement email/SMS notifications for booking confirmations, cancellations, and reminders.
- **Reviews & Ratings**: Allow guests to leave reviews and ratings for hotels and rooms.
- **Multi-Language Support**: Add internationalization (i18n) for different languages.
- **Analytics Dashboard**: Create an admin dashboard to view booking trends, revenue, and occupancy rates.
- **Microservices Architecture**: Break down the monolithic API into smaller, independent microservices (e.g., Auth Service, Booking Service, Payment Service).
- **Real-time Features**: Implement WebSocket connections for real-time updates (e.g., room availability changes).
- **Reporting**: Generate reports on bookings, revenue, guest demographics, etc.
- **File Upload**: Allow admins to upload hotel/room images.
- **Search & Filters**: Advanced search functionality for finding hotels/rooms based on location, price, amenities, etc.
- **Admin Panel (Frontend)**: Develop a web-based admin panel using HTML, CSS, JavaScript, and Tailwind CSS to interact with the API.

## Technologies Used

- **Backend Framework**: FastAPI
- **Database**: PostgreSQL
- **Authentication**: JWT (JSON Web Tokens)
- **API Documentation**: FastAPI's built-in Swagger UI and ReDoc
- **API Testing**: Postman
- **Database Interaction**: SQLAlchemy (or async alternatives like Tortoise ORM)
- **HTTP Client (for testing)**: HTTPX (for internal requests/tests)
