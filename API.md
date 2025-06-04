---
layout: default
title: API Documentation - DataLoud
---

<div class="content-wrapper">
    <div class="page-header">
        <h1 class="page-title">📡 API Documentation</h1>
        <p class="page-description">Complete API reference for developers integrating with DataLoud</p>
    </div>

# 📡 API Documentation

## Overview

The backend provides a comprehensive RESTful API for document processing, chat functionality, and user feedback management.

## Base URL

```
Production: https://your-app.render.com
Development: http://localhost:5000
```

## Authentication

All API endpoints require proper authentication headers:

```http
Content-Type: application/json
Authorization: Bearer <jwt_token>
```

## Endpoints

### 🔄 Health & Status

#### `GET /health`

System health check endpoint.

**Response:**

```json
{
  "status": "healthy",
  "timestamp": "2024-01-01T12:00:00Z",
  "services": {
    "database": "connected",
    "ai_models": "loaded",
    "storage": "available"
  }
}
```

### 📄 Document Management

#### `POST /upload`

Upload and process documents for chat analysis.

**Request:**

```http
POST /upload
Content-Type: multipart/form-data

file: [PDF/CSV/JSON file]
```

**Response:**

```json
{
  "success": true,
  "document_id": "doc_123",
  "filename": "document.pdf",
  "pages": 15,
  "chunks_created": 45,
  "processing_time": "12.5s"
}
```

#### `GET /documents`

Retrieve list of uploaded documents.

**Response:**

```json
{
  "documents": [
    {
      "id": "doc_123",
      "filename": "document.pdf",
      "upload_date": "2024-01-01T12:00:00Z",
      "status": "processed",
      "chunk_count": 45
    }
  ]
}
```

### 💬 Chat System

#### `POST /chat`

Send a message and receive AI-generated response.

**Request:**

```json
{
  "message": "What is the main topic of the document?",
  "session_id": "session_456",
  "document_id": "doc_123",
  "context_limit": 5
}
```

**Response:**

```json
{
  "response": "Based on the document analysis, the main topic is...",
  "message_id": "msg_789",
  "sources": [
    {
      "chunk_id": "chunk_1",
      "content": "Relevant text excerpt...",
      "page": 3,
      "confidence": 0.85
    }
  ],
  "processing_time": "2.3s"
}
```

#### `GET /chat/history`

Retrieve chat history for a session.

**Parameters:**

- `session_id` (required): Chat session identifier
- `limit` (optional): Number of messages to retrieve (default: 50)

**Response:**

```json
{
  "messages": [
    {
      "id": "msg_789",
      "role": "user",
      "content": "What is the main topic?",
      "timestamp": "2024-01-01T12:00:00Z"
    },
    {
      "id": "msg_790",
      "role": "assistant",
      "content": "The main topic is...",
      "timestamp": "2024-01-01T12:00:01Z",
      "sources": [...]
    }
  ]
}
```

#### `POST /chat/session`

Create a new chat session.

**Request:**

```json
{
  "document_id": "doc_123",
  "session_name": "Document Analysis Session"
}
```

**Response:**

```json
{
  "session_id": "session_456",
  "created_at": "2024-01-01T12:00:00Z"
}
```

### 👍 Feedback System

#### `POST /feedback`

Submit feedback for AI responses.

**Request:**

```json
{
  "message_id": "msg_789",
  "rating": "positive",
  "comment": "Very helpful response!",
  "categories": ["accuracy", "relevance"]
}
```

**Response:**

```json
{
  "success": true,
  "feedback_id": "fb_101"
}
```

#### `GET /feedback/analytics`

Retrieve feedback analytics (admin only).

**Response:**

```json
{
  "total_feedback": 150,
  "positive_ratio": 0.78,
  "categories": {
    "accuracy": 0.82,
    "relevance": 0.75,
    "clarity": 0.80
  },
  "recent_trends": [...]
}
```

### 🔍 Search & Analysis

#### `POST /search`

Perform semantic search across document content.

**Request:**

```json
{
  "query": "machine learning algorithms",
  "document_id": "doc_123",
  "limit": 10,
  "threshold": 0.7
}
```

**Response:**

```json
{
  "results": [
    {
      "chunk_id": "chunk_5",
      "content": "Machine learning algorithms are...",
      "similarity_score": 0.89,
      "page": 7,
      "document_section": "Chapter 2"
    }
  ]
}
```

## Error Handling

### Standard Error Format

```json
{
  "error": true,
  "code": "INVALID_REQUEST",
  "message": "The provided document format is not supported",
  "details": {
    "supported_formats": ["pdf", "csv", "json"],
    "received_format": "docx"
  }
}
```

### Error Codes

| Code                     | Description                       | HTTP Status |
| ------------------------ | --------------------------------- | ----------- |
| `INVALID_REQUEST`        | Malformed request data            | 400         |
| `UNAUTHORIZED`           | Missing or invalid authentication | 401         |
| `NOT_FOUND`              | Resource not found                | 404         |
| `RATE_LIMIT_EXCEEDED`    | Too many requests                 | 429         |
| `PROCESSING_ERROR`       | Document processing failed        | 500         |
| `AI_SERVICE_UNAVAILABLE` | AI model service down             | 503         |

## Rate Limiting

API endpoints are rate-limited to ensure fair usage:

- **Chat endpoints**: 30 requests per minute
- **Upload endpoints**: 5 requests per minute
- **Search endpoints**: 60 requests per minute

## WebSocket Support

### Real-time Chat Updates

```javascript
// WebSocket connection for live chat updates
const ws = new WebSocket("wss://your-app.render.com/ws");

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  // Handle real-time chat updates
};
```

## SDK Examples

### JavaScript/TypeScript

```typescript
import { ChatbotAPI } from "./chatbot-sdk";

const api = new ChatbotAPI({
  baseURL: "https://your-app.render.com",
  apiKey: "your-api-key",
});

// Upload document
const upload = await api.uploadDocument(file);

// Send chat message
const response = await api.sendMessage({
  message: "Tell me about this document",
  sessionId: "session_123",
  documentId: upload.document_id,
});
```

### Python

```python
from chatbot_client import ChatbotClient

client = ChatbotClient(
    base_url='https://your-app.render.com',
    api_key='your-api-key'
)

# Upload and process document
result = client.upload_document('document.pdf')

# Start chat session
response = client.chat(
    message='What are the key findings?',
    document_id=result['document_id']
)
```
