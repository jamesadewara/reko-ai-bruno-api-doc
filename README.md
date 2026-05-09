# Reko AI - API Documentation

A comprehensive guide to the Reko AI platform APIs, covering Authentication, Profile Management, Knowledge Hub, and the powerful Recommendation Engine.

## 📂 API Collections Structure

This documentation is organized into three main API Collections (similar to folders in Postman/Bruno):

### 1. Auth System
Handles user identity and secure access.
- **`/auth/register`** - Register a new user.
- **`/auth/verify-otp`** - Verify OTP sent to email/phone.
- **`/auth/login`** - User login.
- **`/auth/refresh`** - Refresh access token.

### 2. Profile Service
Manages user data and personalization.
- **`/profiles/get`** - Get user profile by ID.
- **`/profiles/update`** - Update user profile.
- **`/profiles/delete`** - Delete user account.
- **`/profiles/avatar`** - Manage user profile picture.
- **`/profiles/preferences`** - Manage user preferences.

### 3. AI & Recommendation System
The core intelligence of Reko.
- **`/ai/chat`** - General conversation with the AI assistant.
- **`/ai/recommendations`** - Get product/content recommendations.
- **`/ai/learning`** - Track learning progress and achievements.
- **`/ai/knowledge/search`** - Search the knowledge base.

## 🚀 Authentication

### Prerequisites
All endpoints (except `/auth/register` and `/auth/login`) require a valid **Access Token**. Obtain this by using the **Refresh Token** obtained from the `/auth/login` response.

### Access Token Strategy
1. **Initial Login**: Use `/auth/login` to get `access_token` and `refresh_token`.
2. **Subsequent Requests**: Pass the `access_token` in the `Authorization` header:
   ```http
   Authorization: Bearer {your_access_token}
   ```
3. **Token Expiry**: If the token expires, use `/auth/refresh` with your `refresh_token` to get a new pair.

---

## 📋 API Details

### Auth System

#### Register User
**Endpoint**: `POST /api/v1/auth/register`
**Description**: Creates a new user account.
**Request Body**:
```json
{
    "username": "string",
    "email": "[EMAIL_ADDRESS]",
    "password": "securepassword123",
    "role": "user"
}
```
**Response**:
```json
{
    "success": true,
    "message": "User registered successfully",
    "data": { ... }
}
```

#### Verify OTP
**Endpoint**: `POST /api/v1/auth/verify-otp`
**Description**: Verifies the One-Time Password sent during registration or password reset.
**Request Body**:
```json
{
    "email": "[EMAIL_ADDRESS]",
    "otp": "123456"
}
```
**Response**:
```json
{
    "success": true,
    "message": "OTP Verified successfully"
}
```

#### Login
**Endpoint**: `POST /api/v1/auth/login`
**Description**: Authenticates user and issues tokens.
**Request Body**:
```json
{
    "email": "[EMAIL_ADDRESS]",
    "password": "securepassword123"
}
```
**Response**:
```json
{
    "success": true,
    "message": "User logged in successfully",
    "data": {
        "user": {
            "id": "uuid",
            "email": "...",
            "role": "user"
        },
        "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
        "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
        "expires_in": 3600
    }
}
```

#### Refresh Token
**Endpoint**: `POST /api/v1/auth/refresh`
**Description**: Refreshes the access token using a valid refresh token.
**Request Body**:
```json
{
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
**Response**:
```json
{
    "success": true,
    "message": "Token refreshed successfully",
    "data": {
        "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
        "expires_in": 3600
    }
}
```

---

### Profile Service

#### Get Profile
**Endpoint**: `GET /api/v1/profiles/get?user_id={user_id}`
**Description**: Retrieves a user's profile information.
**Response**:
```json
{
    "success": true,
    "data": {
        "profile": {
            "id": "uuid",
            "full_name": "John Doe",
            "email": "[EMAIL_ADDRESS]",
            "phone": "+2348000000000",
            "role": "user"
        }
    }
}
```

#### Update Profile
**Endpoint**: `PUT /api/v1/profiles/update?user_id={user_id}`
**Description**: Updates user profile details.
**Request Body**:
```json
{
    "full_name": "Jonathan Doe",
    "phone": "+2348000000001"
}
```
**Response**:
```json
{
    "success": true,
    "message": "Profile updated successfully",
    "data": { ... }
}
```

#### Delete Profile
**Endpoint**: `DELETE /api/v1/profiles/delete?user_id={user_id}`
**Description**: Deletes a user account and associated data.
**Response**:
```json
{
    "success": true,
    "message": "Profile deleted successfully"
}
```

#### Upload Avatar
**Endpoint**: `POST /api/v1/profiles/avatar?user_id={user_id}`
**Description**: Uploads a profile picture.
**Request**:
- Method: `POST`
- Headers: `Authorization: Bearer {token}`
- Body: `form-data` with key `image`
**Response**:
```json
{
    "success": true,
    "message": "Avatar uploaded successfully",
    "data": {
        "avatar_url": "https://cdn.reko.ai/avatars/user_uuid.jpg"
    }
}
```

#### Manage Preferences
**Endpoint**: `POST /api/v1/profiles/preferences?user_id={user_id}`
**Description**: Sets user preferences (e.g., topic interests).
**Request Body**:
```json
{
    "preferences": {
        "interests": ["Technology", "Finance", "Health"],
        "notification_level": "high"
    }
}
```
**Response**:
```json
{
    "success": true,
    "message": "Preferences updated successfully",
    "data": { ... }
}
```

---

### AI & Recommendation System

#### Chat with AI
**Endpoint**: `POST /api/v1/ai/chat`
**Description**: Converse with the Reko AI assistant.
**Request Body**:
```json
{
    "user_id": "uuid",
    "message": "Hello, how are you?"
}
```
**Response**:
```json
{
    "success": true,
    "data": {
        "ai_response": "Hello! I'm Reko AI. I can help you with recommendations, learning, and more. How can I assist you today?",
        "context_id": "uuid"
    }
}
```

#### Get Recommendations
**Endpoint**: `POST /api/v1/ai/recommendations`
**Description**: