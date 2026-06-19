---
title: "Authentication"
description: "Complete guide to API authentication and security"
category: "guide"
language: "en"
order: 2
showInSidebar: true
---

# Authentication

All PicToText API requests require authentication using Bearer tokens. This guide covers API key management, security best practices, and troubleshooting authentication issues.

## API Key Format

API keys are 32-character strings that start with a prefix like `sk_`.

```
Bearer sk_123456789abcdef123456789abcdef
```

## Getting Your API Key

### 1. Create Account
1. Sign up at [pictotext.io](https://pictotext.io)
2. Verify your email address
3. Log in to your dashboard

### 2. Generate API Key
1. Navigate to **API Keys** section
2. Click **Generate New Key**
3. Name your key (e.g., "Production", "Development")
4. Copy the key immediately (won't be shown again)

### 3. Test Your Key
```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "image=@test-image.jpg" \
  -F "documentType=cn_id_card"
```

## Request Format

All OCR requests must be sent as `multipart/form-data`.

### HTTP Header
```http
Authorization: Bearer sk_live_123456789abcdef
```

### cURL Example
```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@document.jpg" \
  -F "documentType=cn_id_card"
```

### JavaScript Example
```javascript
const formData = new FormData();
formData.append('image', fileInput.files[0]);
formData.append('documentType', 'cn_id_card');

const response = await fetch('https://pictotext.io/api/v1/ocr', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer sk_live_123456789abcdef'
  },
  body: formData
});
```

### Python Example
```python
import os
import requests

headers = {
    'Authorization': 'Bearer sk_live_123456789abcdef'
}

with open('document.jpg', 'rb') as f:
    files = {
        'image': (os.path.basename('document.jpg'), f, 'image/jpeg')
    }
    data = {
        'documentType': 'cn_id_card'
    }

    response = requests.post(
        'https://pictotext.io/api/v1/ocr',
        headers=headers,
        files=files,
        data=data
    )
```

### Supported Image MIME Types

- `image/jpeg`
- `image/jpg`
- `image/png`
- `image/webp`
- `image/heic`
- `image/heif`

### Upload Rules

- Send the image in the `image` form field as a real file part
- Do not send the image via `data=...` as plain text
- Do not manually set the `multipart/form-data` `Content-Type` header; let your HTTP client add the boundary automatically
- If you preprocess an image in memory, re-encode it as JPEG, PNG, WebP, HEIC, or HEIF before uploading

## Security Best Practices

### 🔒 Key Storage

**Never commit API keys to code repositories.**

### 🔑 Key Management

- **Rotation**: Rotate keys every 90 days
- **Separation**: Use different keys for different environments
- **Monitoring**: Regularly check key usage in dashboard
- **Revocation**: Immediately revoke compromised keys

### 🛡️ Security Measures

- Enable HTTPS for all API calls
- Validate and sanitize all inputs
- Implement rate limiting on your end
- Monitor for suspicious activity
- Use web application firewalls (WAF)

## Error Handling

### Common Authentication Errors

| Status Code | Error Code | Description | Solution |
|-------------|------------|-------------|----------|
| 401 | `INVALID_AUTH_HEADER` | Missing or malformed Authorization header | Use format: `Bearer YOUR_API_KEY` |
| 401 | `INVALID_API_KEY` | API key not found or inactive | Check key in dashboard |
| 403 | `EMAIL_NOT_VERIFIED` | The account email must be verified before the API can be used | Verify your email address and retry |
| 402 | `INSUFFICIENT_CREDITS` | The account has no included quota or remaining API credit | Purchase credits or upgrade your plan |

### Error Response Format

```json
{
  "error": {
    "code": 401,
    "message": "Invalid or inactive API key",
    "status": "Unauthorized",
    "details": [{
      "reason": "INVALID_API_KEY"
    }]
  }
}
```

## Key Rotation

### Manual Rotation
1. Generate new API key in dashboard
2. Update your application with new key
3. Test the new key
4. Revoke the old key

### Automated Rotation (Recommended)

```javascript
// Example: Key rotation with fallback
async function getApiKey() {
  // Try primary key first
  let apiKey = process.env.PICTOTEXT_API_KEY_PRIMARY;

  // If primary fails, try secondary
  if (await testApiKey(apiKey) === false) {
    apiKey = process.env.PICTOTEXT_API_KEY_SECONDARY;
    console.warn('Falling back to secondary API key');
  }

  return apiKey;
}

async function testApiKey(apiKey) {
  try {
    const response = await fetch('https://pictotext.io/api/v1/ocr', {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${apiKey}` },
      body: new FormData() // Empty test
    });

    // 401 means invalid key, other errors might be temporary
    return response.status !== 401;
  } catch {
    return false;
  }
}
```

## Troubleshooting

### Common Issues

**"Invalid API Key" Error**
- Verify key format: `Bearer sk_live_...`
- Check key is active in dashboard
- Ensure no extra spaces in header
- Try regenerating API key

**"Missing Authorization Header"**
- Check header name is exactly "Authorization"
- Verify header value starts with "Bearer "
- Ensure no typos in header name

**Key Not Working**
- Check subscription status
- Verify account email is verified
- Ensure no outstanding payments

**"Invalid Image Type"**
- Ensure the uploaded `image` part uses one of the supported MIME types
- Open files in binary mode (`rb`)
- If using Python `requests`, pass the file via `files=...` and include the MIME type explicitly when possible
- Do not send base64 text, file paths, or plain strings as the `image` field

### Support Contact

If authentication issues persist:

- Email: support@pictotext.io
- Include: Last 4 characters of API key
- Provide: Error message and timestamp
- Share: Request details (sanitized)

## Related Documentation

- [Quickstart Guide](https://pictotext.io/docs/quickstart) - Getting started with API
- [Error Reference](./errors.md) - Complete error codes
- [Usage and Limits](./limits.md) - Usage limits and quotas
- [API Reference](./supported-documents.md) - Endpoint documentation
