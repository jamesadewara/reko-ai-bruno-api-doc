# Reko AI - API Documentation

A comprehensive guide to the Reko AI platform APIs, covering Authentication, AI-powered Recommendations, Digital Twin Analysis, and Chat Intelligence.

---

## 📂 API Collections Structure

This documentation is organized into two primary collections representing the distributed microservices:

### 1. Auth & Social Identity (REKO-AUTH)
Handles user lifecycle, social footprinting, and advertisement management.
- **`Authentication`**: Registration, OTP Verification, Login, Profile Updates, and Onboarding.
- **`Socials`**: Connecting social media handles for digital twin modeling.
- **`Sites`**: Registering external websites for the symbiotic ad ecosystem.
- **`Ads`**: Creating, managing, and tracking advertisements.

### 2. Recommendation Engine (REKO-AI-RECOMMENDATION)
The core intelligence engine responsible for analysis and content delivery.
- **`AI Chats`**: Stateful, multi-modal chat sessions with real-time feedback loops.
- **`AI Recommendations`**: Personalized content ranking using digital twin style fingerprints.
- **`Deep Search`**: Automated social footprint extraction (Tavily/Serper integration).
- **`Review Simulator`**: Hyper-personalized review generation and sentiment prediction.
- **`Ad Intelligence`**: Privacy-preserving behavioral ad scoring.

---

## 🚀 Authentication

### Prerequisites
Most endpoints require a valid **JWT Access Token**. 

### Access Token Strategy
1. **Initial Login**: Use `POST /api/v1/auth/login` to obtain `access_token` and `refresh_token`.
2. **Subsequent Requests**: Attach the token in the `Authorization` header:
   ```http
   Authorization: Bearer {{ACCESS_TOKEN}}
   ```
3. **Token Expiry**: Use `POST /api/v1/auth/token/refresh` with your `refresh_token` to renew access.

---

## 📋 Key API Highlights

### Digital Twin Analysis
**Endpoint**: `POST /api/v1/users/me/analyze`
Triggers the background extraction and analysis of the user's online style and interests.

**Endpoint**: `GET /api/v1/users/me/model`
Retrieves the user's "Digital Twin" profile, including style fingerprints (Nigerians markers, formality scores) and interest embeddings.

### Personalised AI Chat
**Endpoint**: `POST /api/v1/chats/`
Creates a stateful chat session where the AI models the user's personality to provide context-aware assistance.

**Endpoint**: `POST /api/v1/chats/{chatId}/message/{messageId}/feedback`
Allows the user to signal "Like" or "Dislike" on AI responses, which immediately fine-tunes the recommendation weights.

### Ad Symbiosis
**Endpoint**: `POST /api/v1/ads/serve`
Accepts a site key and anonymous behavioral scores to return the most relevant ads WITHOUT learning the visitor's identity.

---

## 🛠️ Tools
This documentation is optimized for [Bruno](https://usebruno.com), an open-source IDE for exploring APIs. Import the collection files located in the `collections/` directory to start testing immediately.