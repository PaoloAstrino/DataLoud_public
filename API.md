---
layout: default
title: API Documentation - DataLoud
---

<div class="content-wrapper">
    <div class="page-header">
        <h1 class="page-title">📡 API Documentation</h1>
        <p class="page-description">Complete API reference for developers integrating with DataLoud</p>
    </div>

    <div class="privacy-content">
        <h2>Overview</h2>
        <p>The backend provides a comprehensive RESTful API for document processing, chat functionality, and user feedback management.</p>

        <h2>Base URL</h2>
        <pre><code>Production: https://your-app.render.com
Development: http://localhost:5000</code></pre>

        <h2>Authentication</h2>
        <p>All API endpoints require proper authentication headers:</p>
        <pre><code>Content-Type: application/json
Authorization: Bearer &lt;jwt_token&gt;</code></pre>

        <h2>Endpoints</h2>

        <h3>🔄 Health & Status</h3>

        <h4><code>GET /health</code></h4>
        <p>System health check endpoint.</p>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "status": "healthy",
  "timestamp": "2024-01-01T12:00:00Z",
  "services": {
    "database": "connected",
    "ai_models": "loaded",
    "storage": "available"
  }
}</code></pre>

        <h3>📄 Document Management</h3>

        <h4><code>POST /upload</code></h4>
        <p>Upload and process a document for chat interactions.</p>

        <p><strong>Request:</strong></p>
        <pre><code>POST /upload
Content-Type: multipart/form-data

file: [PDF/CSV/JSON file]</code></pre>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "success": true,
  "document_id": "doc_123",
  "filename": "document.pdf",
  "pages": 15,
  "chunks_created": 45,
  "processing_time": "12.5s"
}</code></pre>

        <h4><code>GET /documents</code></h4>
        <p>Retrieve list of uploaded documents.</p>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "documents": [
    {
      "id": "doc_123",
      "filename": "document.pdf",
      "upload_date": "2024-01-01T12:00:00Z",
      "status": "processed",
      "chunk_count": 45
    }
  ]
}</code></pre>

        <h3>💬 Chat System</h3>

        <h4><code>POST /chat</code></h4>
        <p>Send a message and receive AI-generated response.</p>

        <p><strong>Request:</strong></p>
        <pre><code>{
  "message": "What is the main topic of the document?",
  "session_id": "session_456",
  "document_id": "doc_123",
  "context_limit": 5
}</code></pre>

        <p><strong>Response:</strong></p>
        <pre><code>{
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
}</code></pre>

        <h4><code>GET /chat/history</code></h4>
        <p>Retrieve chat history for a session.</p>

        <p><strong>Parameters:</strong></p>
        <ul>
            <li><code>session_id</code> (required): Chat session identifier</li>
            <li><code>limit</code> (optional): Number of messages to retrieve (default: 50)</li>
        </ul>

        <p><strong>Response:</strong></p>
        <pre><code>{
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
}</code></pre>

        <h4><code>POST /chat/session</code></h4>
        <p>Create a new chat session.</p>

        <p><strong>Request:</strong></p>
        <pre><code>{
  "document_id": "doc_123",
  "session_name": "Document Analysis Session"
}</code></pre>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "session_id": "session_456",
  "created_at": "2024-01-01T12:00:00Z"
}</code></pre>

        <h3>👍 Feedback System</h3>

        <h4><code>POST /feedback</code></h4>
        <p>Submit feedback for AI responses.</p>

        <p><strong>Request:</strong></p>
        <pre><code>{
  "message_id": "msg_789",
  "rating": "positive",
  "comment": "Very helpful response!",
  "categories": ["accuracy", "relevance"]
}</code></pre>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "success": true,
  "feedback_id": "fb_101"
}</code></pre>

        <h4><code>GET /feedback/analytics</code></h4>
        <p>Retrieve feedback analytics (admin only).</p>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "total_feedback": 150,
  "positive_ratio": 0.78,
  "categories": {
    "accuracy": 0.82,
    "relevance": 0.75,
    "clarity": 0.80
  },
  "recent_trends": [...]
}</code></pre>

        <h3>🔍 Search & Analysis</h3>

        <h4><code>POST /search</code></h4>
        <p>Perform semantic search across document content.</p>

        <p><strong>Request:</strong></p>
        <pre><code>{
  "query": "machine learning algorithms",
  "document_id": "doc_123",
  "limit": 10,
  "threshold": 0.7
}</code></pre>

        <p><strong>Response:</strong></p>
        <pre><code>{
  "results": [
    {
      "chunk_id": "chunk_5",
      "content": "Machine learning algorithms are...",
      "similarity_score": 0.89,
      "page": 7,
      "document_section": "Chapter 2"
    }
  ]
}</code></pre>

        <h2>Error Handling</h2>

        <h3>Standard Error Format</h3>
        <pre><code>{
  "error": true,
  "code": "INVALID_REQUEST",
  "message": "The provided document format is not supported",
  "details": {
    "supported_formats": ["pdf", "csv", "json"],
    "received_format": "docx"
  }
}</code></pre>

        <h3>Error Codes</h3>
        <table>
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Description</th>
                    <th>HTTP Status</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><code>INVALID_REQUEST</code></td>
                    <td>Malformed request data</td>
                    <td>400</td>
                </tr>
                <tr>
                    <td><code>UNAUTHORIZED</code></td>
                    <td>Missing or invalid authentication</td>
                    <td>401</td>
                </tr>
                <tr>
                    <td><code>NOT_FOUND</code></td>
                    <td>Resource not found</td>
                    <td>404</td>
                </tr>
                <tr>
                    <td><code>RATE_LIMIT_EXCEEDED</code></td>
                    <td>Too many requests</td>
                    <td>429</td>
                </tr>
                <tr>
                    <td><code>PROCESSING_ERROR</code></td>
                    <td>Document processing failed</td>
                    <td>500</td>
                </tr>
                <tr>
                    <td><code>AI_SERVICE_UNAVAILABLE</code></td>
                    <td>AI model service down</td>
                    <td>503</td>
                </tr>
            </tbody>
        </table>

        <h2>Rate Limiting</h2>
        <p>API endpoints are rate-limited to ensure fair usage:</p>
        <ul>
            <li><strong>Chat endpoints</strong>: 30 requests per minute</li>
            <li><strong>Upload endpoints</strong>: 5 requests per minute</li>
            <li><strong>Search endpoints</strong>: 60 requests per minute</li>
        </ul>

        <h2>WebSocket Support</h2>

        <h3>Real-time Chat Updates</h3>
        <pre><code>// WebSocket connection for live chat updates
const ws = new WebSocket("wss://your-app.render.com/ws");

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  // Handle real-time chat updates
};</code></pre>

        <h2>SDK Examples</h2>

        <h3>JavaScript/TypeScript</h3>
        <pre><code>import { ChatbotAPI } from "./chatbot-sdk";

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
});</code></pre>

        <h3>Python</h3>
        <pre><code>from chatbot_client import ChatbotClient

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
)</code></pre>

    </div>
</div>
