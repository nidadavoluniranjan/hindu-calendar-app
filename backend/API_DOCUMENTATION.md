# Hindu Calendar API - Complete Documentation

## Base URL
```
https://localhost:5001/api
```

## Authentication
All protected endpoints require JWT Bearer token:
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 1. AUTHENTICATION ENDPOINTS

### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePassword123!",
  "firstName": "John",
  "lastName": "Doe",
  "preferredLanguage": "hi"
}

Response: 201 Created
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "preferredLanguage": "hi"
  }
}
```

### Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "SecurePassword123!"
}

Response: 200 OK
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 3600,
    "tokenType": "Bearer",
    "user": {
      "id": 1,
      "username": "john_doe",
      "email": "john@example.com",
      "preferredLanguage": "hi",
      "role": "User"
    }
  }
}
```

### Refresh Token
```http
POST /api/auth/refresh
Content-Type: application/json

{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}

Response: 200 OK
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 3600
  }
}
```

### Logout
```http
POST /api/auth/logout
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

## 2. CALENDAR ENDPOINTS

### Get Calendar for Month
```http
GET /api/calendar/month?year=2024&month=6
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "data": {
    "year": 2024,
    "month": 6,
    "monthName": "June",
    "days": [
      {
        "date": "2024-06-01",
        "day": 1,
        "gregorianDay": "Saturday",
        "lunarDay": "Shukla Tritiya",
        "festivals": ["Festival Name"],
        "isAuspicious": true,
        "rahuKalam": "16:00-17:30"
      }
    ]
  }
}
```

### Get Festivals for Date Range
```http
GET /api/calendar/festivals?startDate=2024-06-01&endDate=2024-06-30
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Diwali",
      "nameHi": "दिवाली",
      "nameTe": "దీపావళి",
      "nameTa": "தீபாவளி",
      "nameKn": "ದೀಪಾವಳಿ",
      "nameMl": "ദീപാവലി",
      "celebrationDate": "2024-11-01",
      "description": "Festival of lights",
      "isImportant": true,
      "imageUrl": "https://..."
    }
  ]
}
```

### Get Panchang Details for Date
```http
GET /api/calendar/panchang/2024-06-01
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "data": {
    "date": "2024-06-01",
    "tithi": "Shukla Tritiya",
    "tithiDescription": "Lunar day 3 (bright half)",
    "nakshatra": "Ashwini",
    "yoga": "Hari Yoga",
    "karana": "Bava",
    "vaar": 6,
    "vaarName": "Saturday",
    "sunrise": "05:30",
    "sunset": "18:45",
    "moonrise": "08:15",
    "moonset": "20:30",
    "rahuKalam": "16:00-17:30",
    "yamagandaTime": "14:30-16:00",
    "gulikaiKalam": "13:00-14:30",
    "isAuspicious": true,
    "notes": "Good for starting new ventures"
  }
}
```

---

## 3. EVENTS ENDPOINTS

### Get User Events
```http
GET /api/events?page=1&pageSize=20&startDate=2024-06-01&endDate=2024-06-30
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Birthday",
      "description": "My Birthday",
      "startDate": "2024-06-15T00:00:00",
      "endDate": "2024-06-15T23:59:59",
      "category": "Birthday",
      "reminderEnabled": true,
      "reminderMinutesBefore": 1440,
      "notes": "Family gathering",
      "createdAt": "2024-06-01T10:00:00"
    }
  ],
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "total": 5,
    "totalPages": 1
  }
}
```

### Create Event
```http
POST /api/events
Content-Type: application/json
Authorization: Bearer <token>

{
  "title": "Birthday",
  "description": "My Birthday",
  "startDate": "2024-06-15T00:00:00",
  "endDate": "2024-06-15T23:59:59",
  "category": "Birthday",
  "reminderEnabled": true,
  "reminderMinutesBefore": 1440,
  "notes": "Family gathering"
}

Response: 201 Created
{
  "success": true,
  "message": "Event created successfully",
  "data": {
    "id": 1,
    "title": "Birthday",
    "createdAt": "2024-06-01T10:00:00"
  }
}
```

### Update Event
```http
PUT /api/events/1
Content-Type: application/json
Authorization: Bearer <token>

{
  "title": "Birthday",
  "description": "My Birthday",
  "startDate": "2024-06-15T00:00:00",
  "endDate": "2024-06-15T23:59:59",
  "category": "Birthday",
  "reminderEnabled": true,
  "reminderMinutesBefore": 1440,
  "notes": "Family gathering"
}

Response: 200 OK
{
  "success": true,
  "message": "Event updated successfully"
}
```

### Delete Event
```http
DELETE /api/events/1
Authorization: Bearer <token>

Response: 200 OK
{
  "success": true,
  "message": "Event deleted successfully"
}
```

---

## 4. ADMIN - FESTIVAL MANAGEMENT

### Get All Festivals (Admin Only)
```http
GET /api/admin/festivals?page=1&pageSize=50
Authorization: Bearer <token>
X-Admin-Role: Admin

Response: 200 OK
{
  "success": true,
  "data": [...],
  "pagination": {...}
}
```

### Create Festival (Admin Only)
```http
POST /api/admin/festivals
Content-Type: application/json
Authorization: Bearer <token>
X-Admin-Role: Admin

{
  "name": "Diwali",
  "nameHi": "दिवाली",
  "nameTe": "దీపావళి",
  "nameTa": "தீபாவளி",
  "nameKn": "ದೀಪಾವಳಿ",
  "nameMl": "ദീപാവലി",
  "description": "Festival of lights",
  "descriptionHi": "रोशनी का त्योहार",
  "celebrationDate": "2024-11-01",
  "calendarType": "lunar",
  "lunarMonth": 8,
  "lunarDay": 15,
  "isImportant": true,
  "imageUrl": "https://example.com/diwali.jpg"
}

Response: 201 Created
```

### Update Festival (Admin Only)
```http
PUT /api/admin/festivals/1
Content-Type: application/json
Authorization: Bearer <token>
X-Admin-Role: Admin

Response: 200 OK
```

### Delete Festival (Admin Only)
```http
DELETE /api/admin/festivals/1
Authorization: Bearer <token>
X-Admin-Role: Admin

Response: 200 OK
```

---

## Error Responses

### 400 Bad Request
```json
{
  "success": false,
  "statusCode": 400,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

### 401 Unauthorized
```json
{
  "success": false,
  "statusCode": 401,
  "message": "Unauthorized - Missing or invalid token"
}
```

### 403 Forbidden
```json
{
  "success": false,
  "statusCode": 403,
  "message": "Forbidden - Admin role required"
}
```

### 404 Not Found
```json
{
  "success": false,
  "statusCode": 404,
  "message": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "success": false,
  "statusCode": 500,
  "message": "Internal server error",
  "details": "Error message (development only)"
}
```

---

## HTTP Status Codes
- `200 OK` - Successful GET/PUT/DELETE
- `201 Created` - Successful POST
- `204 No Content` - Successful DELETE (no response body)
- `400 Bad Request` - Invalid input
- `401 Unauthorized` - Missing/invalid authentication
- `403 Forbidden` - Insufficient permissions
- `404 Not Found` - Resource not found
- `500 Internal Server Error` - Server error

---

## Language Codes
- `hi` - Hindi (हिन्दी)
- `te` - Telugu (తెలుగు)
- `ta` - Tamil (தமிழ்)
- `kn` - Kannada (ಕನ್ನಡ)
- `ml` - Malayalam (മലയാളം)
