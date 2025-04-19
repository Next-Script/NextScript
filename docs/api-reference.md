# API Reference

## Overview

NextScript provides a comprehensive RESTful API that enables programmatic access to all platform features. This document details the available endpoints, authentication methods, and usage examples.

## Authentication

All API requests require authentication using JWT tokens.

### Authentication Headers
```http
Authorization: Bearer <your_jwt_token>
```

## API Endpoints

### Projects

#### List Projects
```http
GET /api/v1/projects
```

**Query Parameters:**
- `page` (optional): Page number for pagination
- `limit` (optional): Items per page
- `sort` (optional): Sort field
- `order` (optional): Sort order (asc/desc)

**Response:**
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 100
  }
}
```

#### Create Project
```http
POST /api/v1/projects
```

**Request Body:**
```json
{
  "name": "string",
  "description": "string",
  "template": "string"
}
```

### Components

#### List Components
```http
GET /api/v1/components
```

#### Create Component
```http
POST /api/v1/components
```

**Request Body:**
```json
{
  "name": "string",
  "type": "string",
  "properties": {}
}
```

### Workflows

#### List Workflows
```http
GET /api/v1/workflows
```

#### Create Workflow
```http
POST /api/v1/workflows
```

**Request Body:**
```json
{
  "name": "string",
  "triggers": [],
  "actions": []
}
```

### Users

#### User Profile
```http
GET /api/v1/users/me
```

#### Update Profile
```http
PATCH /api/v1/users/me
```

### AI Services

#### Generate Code
```http
POST /api/v1/ai/generate
```

**Request Body:**
```json
{
  "prompt": "string",
  "language": "string",
  "context": {}
}
```

## WebSocket API

### Connection
```javascript
const ws = new WebSocket('wss://api.nextscript.dev/ws');
```

### Events

#### Project Updates
```json
{
  "type": "project.update",
  "data": {
    "projectId": "string",
    "changes": []
  }
}
```

## Error Handling

### Error Response Format
```json
{
  "error": {
    "code": "string",
    "message": "string",
    "details": {}
  }
}
```

### Common Error Codes
- `400`: Bad Request
- `401`: Unauthorized
- `403`: Forbidden
- `404`: Not Found
- `429`: Too Many Requests
- `500`: Internal Server Error

## Rate Limiting

API requests are limited to:
- 1000 requests per hour per API key
- 10 concurrent requests per API key

Rate limit headers:
```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1619550000
```

## Versioning

The API uses semantic versioning in the URL path:
- `/api/v1/`: Current stable version
- `/api/v2-beta/`: Beta version features

## SDK Examples

### JavaScript/TypeScript
```typescript
import { NextScriptClient } from '@nextscript/sdk';

const client = new NextScriptClient({
  apiKey: 'your-api-key'
});

const projects = await client.projects.list();
```

### Python
```python
from nextscript import NextScriptClient

client = NextScriptClient(api_key='your-api-key')
projects = client.projects.list()
```

## Webhooks

### Configuring Webhooks
```http
POST /api/v1/webhooks
```

**Request Body:**
```json
{
  "url": "string",
  "events": ["project.update", "workflow.complete"],
  "secret": "string"
}
```

### Webhook Payload
```json
{
  "event": "string",
  "timestamp": "string",
  "data": {}
}
```

## Best Practices

1. **Authentication**
   - Store API keys securely
   - Rotate keys regularly
   - Use environment variables

2. **Rate Limiting**
   - Implement exponential backoff
   - Cache responses when possible
   - Monitor rate limit headers

3. **Error Handling**
   - Implement retry logic
   - Log errors appropriately
   - Handle edge cases

4. **Performance**
   - Use pagination
   - Request only needed fields
   - Batch operations when possible
