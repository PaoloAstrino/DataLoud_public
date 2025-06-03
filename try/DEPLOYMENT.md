# 🚀 Deployment Guide

## Overview

This guide covers deployment strategies for both frontend and backend components of the AI-Powered Document Chatbot.

## Production Architecture

### Frontend Deployment (Vercel)

The Next.js frontend is optimized for deployment on Vercel with edge computing capabilities.

#### Features:

- **Edge Functions**: Global distribution for low latency
- **Automatic HTTPS**: SSL certificates and security headers
- **Build Optimization**: Static generation and code splitting
- **Environment Management**: Secure environment variable handling

#### Deployment Configuration:

```json
{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "nodejs": "18.x"
}
```

### Backend Deployment (Render.com)

The Python Flask backend runs on Render.com with auto-scaling capabilities.

#### Features:

- **Auto-scaling**: Dynamic resource allocation based on load
- **Health Monitoring**: Automatic restart on failure
- **SSL/TLS**: End-to-end encryption
- **Environment Isolation**: Secure secrets management

#### Deployment Configuration:

```yaml
services:
  - type: web
    name: chatbot-backend
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn unified_server:app
    healthCheckPath: /health
```

### Database (Supabase)

Managed PostgreSQL with built-in scaling and backup.

#### Features:

- **Auto-backup**: Daily automated backups
- **Connection Pooling**: Optimized database connections
- **Real-time**: WebSocket support for live updates
- **Extensions**: pgvector for vector similarity search

## Environment Configuration

### Frontend Environment Variables

```bash
# Next.js Configuration
NEXT_PUBLIC_API_URL=https://your-backend.render.com
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key

# Analytics (Optional)
NEXT_PUBLIC_GA_ID=GA_MEASUREMENT_ID
VERCEL_URL=your-app.vercel.app
```

### Backend Environment Variables

```bash
# Flask Configuration
FLASK_ENV=production
FLASK_DEBUG=False
PORT=5000

# Database
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your_service_role_key
DATABASE_URL=postgresql://user:pass@host:port/db

# AI Services
HUGGINGFACE_API_KEY=your_hf_token
OPENAI_API_KEY=your_openai_key

# Security
JWT_SECRET_KEY=your_secret_key
CORS_ORIGINS=https://your-frontend.vercel.app
```

## Deployment Steps

### 1. Database Setup (Supabase)

```sql
-- Enable required extensions
CREATE EXTENSION IF NOT EXISTS vector;
CREATE EXTENSION IF NOT EXISTS uuid-ossp;

-- Create main tables
CREATE TABLE documents (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    filename TEXT NOT NULL,
    file_path TEXT,
    upload_date TIMESTAMP DEFAULT NOW(),
    processed BOOLEAN DEFAULT FALSE,
    chunk_count INTEGER DEFAULT 0
);

CREATE TABLE chat_sessions (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    document_id UUID REFERENCES documents(id),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE chat_messages (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    session_id UUID REFERENCES chat_sessions(id),
    role TEXT CHECK (role IN ('user', 'assistant')),
    content TEXT NOT NULL,
    timestamp TIMESTAMP DEFAULT NOW(),
    message_id TEXT UNIQUE
);

-- Enable Row Level Security
ALTER TABLE documents ENABLE ROW LEVEL SECURITY;
ALTER TABLE chat_sessions ENABLE ROW LEVEL SECURITY;
ALTER TABLE chat_messages ENABLE ROW LEVEL SECURITY;
```

### 2. Backend Deployment

#### Requirements File

```txt
flask==2.3.3
gunicorn==21.2.0
supabase==1.0.4
transformers==4.35.0
torch==2.1.0
numpy==1.24.3
pandas==2.0.3
python-dotenv==1.0.0
requests==2.31.0
PyPDF2==3.0.1
sentence-transformers==2.2.2
```

#### Gunicorn Configuration

```python
# gunicorn.conf.py
bind = "0.0.0.0:5000"
workers = 4
worker_class = "sync"
worker_connections = 1000
timeout = 120
max_requests = 1000
max_requests_jitter = 50
preload_app = True
```

#### Health Check Implementation

```python
# health_check.py
@app.route('/health')
def health_check():
    return {
        'status': 'healthy',
        'timestamp': datetime.utcnow().isoformat(),
        'services': check_services()
    }
```

### 3. Frontend Deployment

#### Next.js Configuration

```javascript
// next.config.mjs
const nextConfig = {
  output: "standalone",
  experimental: {
    serverComponentsExternalPackages: ["@supabase/supabase-js"],
  },
  env: {
    CUSTOM_KEY: process.env.CUSTOM_KEY,
  },
};
```

#### Build Optimization

```json
{
  "scripts": {
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit"
  }
}
```

## Monitoring & Observability

### Health Checks

```bash
# Backend health check
curl https://your-backend.render.com/health

# Frontend health check
curl https://your-frontend.vercel.app/api/health
```

### Logging Configuration

```python
import logging
from logging.handlers import RotatingFileHandler

# Configure structured logging
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s %(levelname)s %(name)s %(message)s',
    handlers=[
        RotatingFileHandler('app.log', maxBytes=10000000, backupCount=10),
        logging.StreamHandler()
    ]
)
```

### Performance Monitoring

```javascript
// Frontend performance tracking
export function reportWebVitals(metric) {
  if (metric.label === "web-vital") {
    // Send to analytics service
    analytics.track("Web Vital", {
      name: metric.name,
      value: metric.value,
      id: metric.id,
    });
  }
}
```

## Scaling Considerations

### Horizontal Scaling

- **Frontend**: Edge deployment across multiple regions
- **Backend**: Auto-scaling based on CPU/memory usage
- **Database**: Read replicas for improved performance

### Caching Strategy

```python
# Redis cache for embeddings
import redis

cache = redis.Redis(
    host='redis-server',
    port=6379,
    decode_responses=True
)

def get_cached_embedding(text_hash):
    return cache.get(f"embedding:{text_hash}")
```

### Load Balancing

```nginx
# nginx.conf for backend load balancing
upstream backend {
    server backend-1:5000;
    server backend-2:5000;
    server backend-3:5000;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## Security Hardening

### HTTPS Configuration

```python
# Force HTTPS in production
from flask_talisman import Talisman

Talisman(app, force_https=True)
```

### CORS Configuration

```python
from flask_cors import CORS

CORS(app, origins=[
    'https://your-frontend.vercel.app',
    'https://your-custom-domain.com'
])
```

### Rate Limiting

```python
from flask_limiter import Limiter
from flask_limiter.util import get_remote_address

limiter = Limiter(
    app,
    key_func=get_remote_address,
    default_limits=["100 per hour"]
)

@app.route('/chat')
@limiter.limit("30 per minute")
def chat():
    # Chat endpoint logic
    pass
```

## Backup & Recovery

### Database Backup

```bash
# Automated backup script
#!/bin/bash
BACKUP_NAME="chatbot_backup_$(date +%Y%m%d_%H%M%S)"
pg_dump $DATABASE_URL > "/backups/${BACKUP_NAME}.sql"
```

### File Storage Backup

```python
# S3 backup for uploaded documents
import boto3

s3 = boto3.client('s3')

def backup_files():
    for file in local_files:
        s3.upload_file(
            file['path'],
            'backup-bucket',
            f"backups/{file['name']}"
        )
```

## Troubleshooting

### Common Issues

1. **Memory Issues**: Increase worker memory limits
2. **Timeout Errors**: Adjust request timeout settings
3. **Database Connections**: Configure connection pooling
4. **API Rate Limits**: Implement exponential backoff

### Debug Mode

```python
# Enable debug logging
import os
if os.getenv('DEBUG') == 'true':
    app.logger.setLevel(logging.DEBUG)
```
