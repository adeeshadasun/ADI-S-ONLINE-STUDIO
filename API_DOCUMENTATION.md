# API Documentation

## Base URL
```
http://localhost:5000/api
```

Production:
```
https://your-backend-url.com/api
```

## Authentication

All protected endpoints require JWT token in header:
```
Authorization: Bearer your_jwt_token
```

## Response Format

### Success (2xx)
```json
{
  "success": true,
  "message": "Operation successful",
  "data": { ... }
}
```

### Error (4xx, 5xx)
```json
{
  "success": false,
  "message": "Error description"
}
```

---

## Authentication Endpoints

### Register User
```
POST /auth/register
```

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "confirmPassword": "password123"
}
```

**Response:**
```json
{
  "success": true,
  "message": "User registered successfully",
  "token": "eyJhbGc...",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

---

### Login User
```
POST /auth/login
```

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Login successful",
  "token": "eyJhbGc...",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

---

### Get Current User
```
GET /auth/me
```

**Headers:**
```
Authorization: Bearer token
```

**Response:**
```json
{
  "success": true,
  "data": {
    "_id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

---

## Photo Endpoints

### Upload Photo
```
POST /photos/upload
```

**Headers:**
```
Authorization: Bearer token
Content-Type: multipart/form-data
```

**Form Data:**
```
image: [file]        // Required
title: "My Photo"    // Required
description: "..."   // Optional
category: "portrait" // Optional
```

**Valid Categories:**
- portrait
- landscape
- product
- wedding
- event
- other

**Response:**
```json
{
  "success": true,
  "message": "Photo uploaded successfully",
  "data": {
    "_id": "photo_id",
    "title": "My Photo",
    "imageUrl": "/uploads/photo-123.jpg",
    "userId": "user_id",
    "category": "portrait",
    "downloadCount": 0,
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

---

### Get All Photos
```
GET /photos
```

**Response:**
```json
{
  "success": true,
  "count": 10,
  "data": [
    {
      "_id": "photo_id",
      "title": "Photo 1",
      "imageUrl": "/uploads/photo-1.jpg",
      "category": "portrait",
      "downloadCount": 5
    }
  ]
}
```

---

### Get User Photos
```
GET /photos/user/:userId
```

**Headers:**
```
Authorization: Bearer token
```

**Parameters:**
- `userId` - User ID

**Response:**
```json
{
  "success": true,
  "count": 5,
  "data": [
    {
      "_id": "photo_id",
      "title": "My Photo",
      "category": "portrait"
    }
  ]
}
```

---

### Get Single Photo
```
GET /photos/:id
```

**Headers:**
```
Authorization: Bearer token
```

**Parameters:**
- `id` - Photo ID

---

### Download Photo
```
GET /photos/:id/download
```

**Headers:**
```
Authorization: Bearer token
```

**Response:**
- Downloads the image file
- Increments download count

---

### Delete Photo
```
DELETE /photos/:id
```

**Headers:**
```
Authorization: Bearer token
```

**Authorization:**
- Own photo: User
- Any photo: Admin

---

## Booking Endpoints

### Create Booking
```
POST /bookings
```

**Headers:**
```
Authorization: Bearer token
```

**Request Body:**
```json
{
  "serviceType": "photography",
  "eventDate": "2024-03-15T10:00:00Z",
  "eventLocation": "New York, NY",
  "budget": 1500,
  "description": "Wedding photography"
}
```

**Service Types:**
- photography
- videography
- graphic-design
- photo-editing

**Response:**
```json
{
  "success": true,
  "message": "Booking created successfully",
  "data": {
    "_id": "booking_id",
    "userId": "user_id",
    "serviceType": "photography",
    "eventDate": "2024-03-15T10:00:00Z",
    "status": "pending",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

---

### Get User Bookings
```
GET /bookings/user/:userId
```

**Headers:**
```
Authorization: Bearer token
```

---

### Get Booking Details
```
GET /bookings/:id
```

**Headers:**
```
Authorization: Bearer token
```

---

### Update Booking
```
PUT /bookings/:id
```

**Headers:**
```
Authorization: Bearer token
```

**Request Body:**
```json
{
  "status": "confirmed",
  "notes": "Additional notes"
}
```

**Valid Status Values:**
- pending
- confirmed
- completed
- cancelled

---

### Delete Booking
```
DELETE /bookings/:id
```

**Headers:**
```
Authorization: Bearer token
```

---

## Admin Endpoints

**All admin endpoints require:**
- JWT token
- User role = "admin"

---

### Get Dashboard Stats
```
GET /admin/dashboard
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
```

**Response:**
```json
{
  "success": true,
  "data": {
    "totalUsers": 50,
    "totalPhotos": 150,
    "totalBookings": 20,
    "admins": 2,
    "recentUsers": [...],
    "recentPhotos": [...]
  }
}
```

---

### Get All Users
```
GET /admin/users
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
```

**Response:**
```json
{
  "success": true,
  "count": 50,
  "data": [
    {
      "_id": "user_id",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user",
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ]
}
```

---

### Delete User
```
DELETE /admin/users/:id
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
```

**Note:** Deletes user and all their photos

---

### Update User Role
```
PUT /admin/users/:id/role
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
```

**Request Body:**
```json
{
  "role": "admin"
}
```

**Valid Roles:**
- user
- admin

---

### Upload Photo for User
```
POST /admin/photos/upload/:userId
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
Content-Type: multipart/form-data
```

**Parameters:**
- `userId` - Target user ID

**Form Data:**
```
image: [file]       // Required
title: "Photo"      // Required
category: "other"   // Optional
```

---

### Delete Photo (Admin)
```
DELETE /admin/photos/:id
```

**Headers:**
```
Authorization: Bearer token
(User must be admin)
```

---

## Error Codes

| Code | Meaning | Solution |
|------|---------|----------|
| 400 | Bad Request | Check request format |
| 401 | Unauthorized | Login required |
| 403 | Forbidden | Not enough permissions |
| 404 | Not Found | Resource doesn't exist |
| 500 | Server Error | Contact support |

---

## Rate Limiting

Currently: No rate limiting (add in production)

Recommended:
- 100 requests per minute per IP
- 10 uploads per hour per user

---

## Testing with cURL

### Register User
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "confirmPassword": "password123"
  }'
```

### Login
```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'
```

### Get Current User
```bash
curl -X GET http://localhost:5000/api/auth/me \
  -H "Authorization: Bearer YOUR_TOKEN"
```

### Upload Photo
```bash
curl -X POST http://localhost:5000/api/photos/upload \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -F "image=@photo.jpg" \
  -F "title=My Photo" \
  -F "category=portrait"
```

---

## Testing with Postman

1. Import the API collection
2. Set `{{baseUrl}}` to `http://localhost:5000/api`
3. Set `{{token}}` after login
4. Use variables: `{{baseUrl}}`, `{{token}}`

---

## Best Practices

1. **Always send Content-Type header**
2. **Store JWT token securely** (localStorage for web)
3. **Refresh token before expiry** (every 7 days)
4. **Handle errors gracefully**
5. **Validate file uploads** on frontend
6. **Use HTTPS in production**
7. **Never expose JWT secret**
8. **Test endpoints thoroughly**

---

## Pagination (Future)

Currently no pagination. Photos limit to system performance.

For large image collections, add:
```
GET /photos?page=1&limit=20
```

---

## Filtering (Future)

Currently no advanced filtering. To add:
```
GET /photos?category=portrait&sortBy=date
```

---

## Version

API Version: 1.0
Last Updated: 2024

---

## Support

For API issues:
1. Check this documentation
2. Review error response
3. Check console logs
4. Test with cURL/Postman
5. Contact support
