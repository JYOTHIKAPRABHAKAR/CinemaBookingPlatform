# Cinema Booking Platform - Backend Assignment

A backend API for a cinema booking platform similar to PVR Cinemas. The system includes modules for user accounts, movie listings, theater and screen management, seat selection, real-time show bookings, food orders, and integrated payments.

## 🎬 Overview

This is a comprehensive Node.js/Express.js backend API that powers a cinema booking platform with enterprise-grade features including JWT authentication, real-time seat booking, payment processing, and admin management capabilities. The system is designed to handle the complete booking lifecycle from movie discovery to payment confirmation.

## 🛠️ Tech Stack

- **Runtime**: Node.js + Express.js
- **Database**: SQLite (development)
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcrypt
- **Validation**: Joi + Express-validator
- **Logging**: Winston (structured logging)
- **Rate Limiting**: Express-rate-limit
- **CORS**: Cross-origin resource sharing enabled

## ✨ Key Features

### 🔐 Authentication & Authorization
- Secure user registration and login
- JWT-based authentication with token expiration
- Role-based access control (User/Admin)
- Password hashing with bcrypt
- Rate limiting on authentication endpoints

### 🎥 Movie Management
- Comprehensive movie CRUD operations
- Filtering by city, genre, language, and format
- Support for upcoming movies
- Movie metadata (cast, director, ratings, etc.)
- Multiple format support (2D, 3D, IMAX)

### 🎭 Show & Theater Management
- Dynamic show scheduling
- Theater and screen management
- Real-time seat availability
- Seat layout management with categories (Regular, Premium, Recliner)
- Show status tracking (active, cancelled, housefull)

### 🪑 Seat Booking System
- Real-time seat selection and booking
- Conflict prevention for concurrent bookings
- Seat hold functionality
- Dynamic seat pricing by category
- Seat layout visualization

### 🍿 Food & Beverage
- Comprehensive F&B menu management
- Category-based menu organization
- Order integration with bookings
- Pricing and availability tracking

### 💳 Payment Processing
- Payment initiation and confirmation
- Multiple payment method support
- Transaction tracking
- Integration with booking system

### 📊 Admin Dashboard
- Revenue reporting
- Booking management
- Show scheduling
- User management
- System analytics

## 🚀 Quick Start

### Prerequisites

- **Node.js** (v14 or higher)
- **npm** or **yarn**
- **SQLite3** (included with Node.js)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd cinemaBookingPlatform
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   # Create .env file in the root directory
   JWT_SECRET=your_super_secret_jwt_key_here
   PORT=3000
   NODE_ENV=development
   ```

4. **Initialize the database**
   ```bash
   npm run init-db
   ```

5. **Start the server**
   ```bash
   npm start
   ```

The API will be available at `http://localhost:3000`

### Development Mode

```bash
npm run dev
```

## 📁 Project Structure

```
cinemaBookingPlatform/
├── src/
│   ├── config/
│   │   └── database.js          # Database configuration
<<<<<<< HEAD
=======
│   ├── controllers/
>>>>>>> 8ca227fe0d1c6d0b9be36c56606025bc98946c1e
│   │   ├── adminController.js   # Admin operations
│   │   ├── authController.js    # Authentication
│   │   ├── bookingController.js # Booking management
│   │   ├── movieController.js   # Movie operations
│   │   ├── showController.js    # Show management
│   │   └── ...                  # Other controllers
│   ├── middleware/
│   │   ├── auth.js              # JWT authentication
│   │   ├── validation.js        # Input validation
│   │   └── errorHandler.js      # Error handling
│   ├── routes/
│   │   ├── authRoutes.js        # Auth endpoints
│   │   ├── movieRoutes.js       # Movie endpoints
│   │   ├── bookingRoutes.js     # Booking endpoints
│   │   └── ...                  # Other routes
│   ├── utils/
│   │   ├── logger.js            # Winston logging
│   │   ├── helpers.js           # Utility functions
│   │   └── ...                  # Other utilities
│   └── app.js                   # Main application file
├── database/
│   ├── cinema.db                # SQLite database
│   ├── schema.sql               # Database schema
│   └── seeds.sql                # Sample data
├── logs/                        # Application logs
├── package.json
└── README.md
```

## 🗄️ Database Design

### Entity Relationships

```
Users (1) ←→ (N) Bookings
Movies (1) ←→ (N) Shows
Theaters (1) ←→ (N) Screens
Screens (1) ←→ (N) Shows
Shows (1) ←→ (N) Bookings
Bookings (1) ←→ (N) Booked_Seats
Bookings (1) ←→ (N) Payments
Bookings (1) ←→ (N) Food_Orders
```

### Core Tables

- **users**: User accounts and authentication
- **movies**: Movie information and metadata
- **theaters**: Theater locations and facilities
- **screens**: Individual screens within theaters
- **shows**: Show scheduling and pricing
- **bookings**: Booking records and status
- **booked_seats**: Individual seat bookings
- **payments**: Payment transaction records
- **food_orders**: F&B order management
- **seat_layouts**: Dynamic seat configurations

## 📚 API Documentation

### Base URL
```
http://localhost:3000/api
```

### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/auth/register` | Register new user | No |
| POST | `/auth/login` | User/Admin login | No |

### Movie Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/movies` | Get movies with filters | No |
| GET | `/movies/:id` | Get movie details | No |
| GET | `/movies/upcoming` | Get upcoming movies | No |
| POST | `/movies` | Create new movie | Admin |
| PUT | `/movies/:id` | Update movie | Admin |
| DELETE | `/movies/:id` | Delete movie | Admin |

### Show Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/shows` | Get shows with filters | No |
| GET | `/shows/:showId` | Get show details | No |
| GET | `/shows/movie/:movieId` | Get shows by movie | No |
| POST | `/shows` | Create new show | Admin |
| PUT | `/shows/:showId` | Update show | Admin |
| DELETE | `/shows/:showId` | Delete show | Admin |

### Booking Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/bookings/create` | Create booking | User |
| GET | `/bookings` | Get user bookings | User |
| GET | `/bookings/:bookingId` | Get booking details | User |

### Seat Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/shows/:showId/seats` | Get seat layout | No |
| POST | `/shows/:showId/seats/block` | Block seats | User |

### Payment Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/payments/initiate` | Initiate payment | User |
| POST | `/payments/confirm` | Confirm payment | User |

### F&B Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/fnb/menu` | Get F&B menu | No |
| POST | `/fnb/order` | Place F&B order | User |

## 📝 Example API Requests

### User Registration
```bash
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword123",
  "mobile": "+919876543210",
  "dateOfBirth": "1990-01-01"
}
```

### User Login
```bash
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securePassword123"
}
```

### Create Movie (Admin)
```bash
POST /api/movies
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "title": "The Matrix Resurrections",
  "description": "Return to the world of The Matrix...",
  "duration_mins": 148,
  "genre": ["Action", "Sci-Fi", "Thriller"],
  "language": ["English"],
  "format": ["2D", "3D", "IMAX"],
  "release_date": "2021-12-22",
  "rating": "R",
  "cast": ["Keanu Reeves", "Carrie-Anne Moss"],
  "director": "Lana Wachowski",
  "producer": "James McTeigue",
  "poster_url": "https://example.com/poster.jpg",
  "trailer_url": "https://example.com/trailer.mp4",
  "imdb_rating": 7.2,
  "is_upcoming": false
}
```

### Create Show (Admin)
```bash
POST /api/shows
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "movieId": 1,
  "screenId": 1,
  "theaterId": 1,
  "showDate": "2024-01-20",
  "showTime": "14:30",
  "basePrice": 250,
  "format": "2D",
  "language": "English"
}
```

### Create Booking (User)
```bash
POST /api/bookings/create
Authorization: Bearer <user_token>
Content-Type: application/json

{
  "showId": 1,
  "seats": ["A1", "A2"],
  "userDetails": {
    "email": "john@example.com",
    "mobile": "+919876543210"
  }
}
```

## 🧪 Testing

### Postman Collection

1. Import `cinemaBookingPlatform.postman_collection.json` into Postman
2. Set up environment variables:
   - `base_url`: `http://localhost:3000`
   - `user_token`: (auto-populated after login)
   - `admin_token`: (auto-populated after admin login)

### Automated Testing

Run the PowerShell test script:
```powershell
.\test_apis.ps1
```

### Manual Testing Flow

1. **Register/Login**: Start with user registration or login
2. **Admin Login**: Login as admin for management operations
3. **Create Movie**: Use admin token to create a new movie
4. **Create Show**: Schedule shows for the movie
5. **Test Booking**: Create bookings as a regular user

## 🌟 Bonus Features Implemented

### 🪑 Advanced Seat Management
- **Dynamic Seat Layouts**: Configurable seat arrangements per screen
- **Seat Categories**: Regular, Premium, and Recliner seating
- **Dynamic Pricing**: Different pricing for each seat category
- **Seat Hold System**: Temporary seat reservation with timeout
- **Conflict Prevention**: Real-time seat availability checking

### 💰 Dynamic Pricing
- **Category-based Pricing**: Different prices for Regular, Premium, Recliner
- **Show-specific Pricing**: Custom pricing per show
- **Automatic Price Updates**: Bulk price updates for shows

### 🔒 Security Enhancements
- **Rate Limiting**: Prevents API abuse
- **Input Validation**: Comprehensive request validation
- **SQL Injection Prevention**: Parameterized queries
- **CORS Configuration**: Secure cross-origin requests

### 📊 Comprehensive Logging
- **Structured Logging**: Winston-based logging system
- **Multiple Log Files**: API, Error, Exception, and Combined logs
- **Request Tracking**: Full request/response logging
- **Performance Monitoring**: Response time tracking

## 🤔 Assumptions Made

1. **Database**: SQLite for development (easily switchable to PostgreSQL/MySQL)
2. **Authentication**: JWT tokens with configurable expiration
3. **Seat Booking**: First-come-first-served with real-time conflict prevention
4. **Payment**: Mock payment gateway (easily integrable with real gateways)
5. **Time Zones**: UTC timestamps for consistency
6. **File Storage**: URLs for movie posters and trailers
7. **Rate Limiting**: Per-IP rate limiting on authentication endpoints

## 🗃️ Database Seeding

The application automatically seeds the database with sample data:

### Sample Data Includes:
- **5 Cities**: Mumbai, Delhi, Bangalore, Chennai, Hyderabad
- **5 Theaters**: Major cinema chains across cities
- **6 Screens**: Mix of IMAX, 2D, and 3D screens
- **10 Movies**: Popular movies with metadata
- **10 Shows**: Scheduled shows across theaters
- **2 Users**: Admin and regular user accounts
- **F&B Menu**: Complete food and beverage menu

### Manual Seeding
```bash
npm run init-db
```

## 🚀 Deployment

### Environment Variables
```bash
JWT_SECRET=your_production_jwt_secret
PORT=3000
NODE_ENV=production
DB_PATH=/path/to/production/database.db
```
<<<<<<< HEAD

### Production Considerations
- Use a production database (MySQL)
- Set up proper logging and monitoring
- Use environment-specific JWT secrets
=======
>>>>>>> 8ca227fe0d1c6d0b9be36c56606025bc98946c1e

