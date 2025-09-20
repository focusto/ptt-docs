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
const response = await fetch('https://pictotext.io/api/v1/ocr', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer sk_live_123456789abcdef',
    'Content-Type': 'multipart/form-data'
  },
  body: formData
});
```

### Python Example
```python
import requests

headers = {
    'Authorization': 'Bearer sk_live_123456789abcdef'
}

response = requests.post('https://pictotext.io/api/v1/ocr',
                        headers=headers,
                        files=files,
                        data=data)
```

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
| 401 | `API_KEY_DISABLED` | API key has been disabled | Contact support |
| 403 | `SUBSCRIPTION_REQUIRED` | Active subscription needed | Upgrade to paid plan |

### Error Response Format

```json
{
  "error": {
    "code": 401,
    "message": "Invalid or inactive API key",
    "status": "Unauthorized",
    "details": [
      {
        "reason": "INVALID_API_KEY"
      }
    ]
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

### Support Contact

If authentication issues persist:

- Email: support@pictotext.io
- Include: Last 4 characters of API key
- Provide: Error message and timestamp
- Share: Request details (sanitized)

## Related Documentation

- [Quickstart Guide](/docs/quickstart.md) - Getting started with API
- [Error Reference](/docs/reference/errors.md) - Complete error codes
- [Rate Limits](/docs/reference/limits.md) - Usage limits and quotas
