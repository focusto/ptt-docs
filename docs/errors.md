---
title: "Error Reference"
description: "Complete reference for API errors and troubleshooting"
category: "guide"
language: "en"
order: 3
showInSidebar: true
---

# Error Reference

Complete reference for handling PicToText API errors with detailed error codes, troubleshooting steps, and best practices.

## Error Format

All errors follow a consistent JSON structure:

```json
{
  "error": {
    "code": 400,
    "message": "Human-readable description",
    "status": "HTTP Status Text",
    "details": [
      {
        "reason": "ERROR_CODE",
        "metadata": {} // Optional additional data
      }
    ]
  }
}
```

## HTTP Status Codes

### 400 Bad Request
Invalid request parameters or missing required fields.

**Common Causes:**
- Missing image file
- Invalid document type
- Malformed request
- Invalid image format

**Example:**
```json
{
  "error": {
    "code": 400,
    "message": "Image file is required in form data.",
    "status": "Bad Request",
    "details": [{ "reason": "MISSING_IMAGE_FILE" }]
  }
}
```

### 401 Unauthorized
Authentication failed.

**Common Causes:**
- Missing Authorization header
- Invalid API key
- API key not found
- Inactive API key

**Example:**
```json
{
  "error": {
    "code": 401,
    "message": "Invalid or inactive API key",
    "status": "Unauthorized",
    "details": [{ "reason": "INVALID_API_KEY" }]
  }
}
```

### 402 Payment Required
Insufficient credits for enterprise users.

**Example:**
```json
{
  "error": {
    "code": 402,
    "message": "Insufficient credits. Please top up your account.",
    "status": "Payment Required",
    "details": [{ "reason": "INSUFFICIENT_CREDITS" }]
  }
}
```

### 403 Forbidden
Access denied due to subscription or account issues.

**Common Causes:**
- Inactive subscription
- API key disabled
- Account suspended
- Regional restrictions

**Example:**
```json
{
  "error": {
    "code": 403,
    "message": "A subscription is required to use this API key.",
    "status": "Forbidden",
    "details": [{ "reason": "SUBSCRIPTION_REQUIRED" }]
  }
}
```

### 500 Internal Server Error
Server-side processing error.

**Common Causes:**
- AI service failure
- Image processing error
- System maintenance
- Database issues

**Example:**
```json
{
  "error": {
    "code": 500,
    "message": "Failed to process image with AI service.",
    "status": "Internal Server Error",
    "details": [{ "reason": "AI_SERVICE_ERROR" }]
  }
}
```

### 503 Service Unavailable
Service temporarily unavailable.

**Common Causes:**
- Maintenance window
- High load
- Infrastructure issues

**Example:**
```json
{
  "error": {
    "code": 503,
    "message": "Service temporarily unavailable. Please try again later.",
    "status": "Service Unavailable",
    "details": [{ "reason": "SERVICE_UNAVAILABLE" }]
  }
}
```

## Error Codes Reference

### Authentication Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `INVALID_AUTH_HEADER` | Missing or malformed Authorization header | Use format: `Bearer YOUR_API_KEY` |
| `INVALID_API_KEY` | API key not found or inactive | Check key in dashboard |
| `SUBSCRIPTION_REQUIRED` | Active subscription needed | Upgrade to paid plan |
| `ACCOUNT_SUSPENDED` | Account access restricted | Contact support |

### Request Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `MISSING_IMAGE_FILE` | No image file provided | Include image in form data |
| `INVALID_DOCUMENT_TYPE` | Unsupported document type | Check [supported documents](/docs/supported-documents.md) |
| `INVALID_IMAGE_FORMAT` | Unsupported image format | Use JPG, PNG, GIF, or WebP |
| `IMAGE_TOO_LARGE` | Image exceeds 10MB limit | Resize or compress image |
| `IMAGE_TOO_SMALL` | Image too small to process | Use higher resolution image |
| `IMAGE_CORRUPTED` | Image file is corrupted | Re-upload the image |
| `INVALID_JSON` | Malformed JSON in request | Check request format |

### Processing Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `AI_SERVICE_ERROR` | AI processing failed | Retry request, contact support if persists |
| `IMAGE_PROCESSING_ERROR` | Cannot analyze image | Check image quality |
| `TEXT_EXTRACTION_FAILED` | Cannot extract text | Ensure document is clear |
| `STRUCTURED_DATA_ERROR` | Cannot parse document structure | Verify document type |
| `DOCUMENT_RECOGNITION_FAILED` | Cannot identify document type | Use specific document type |
| `LOW_CONFIDENCE_RESULT` | Low confidence in extracted data | Check image quality |

### Account Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `INSUFFICIENT_CREDITS` | Enterprise user out of credits | Purchase more credits |
| `BILLING_ISSUE` | Payment method issue | Update payment method |

### System Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `DATABASE_ERROR` | Database operation failed | Retry, contact support if persists |
| `EXTERNAL_SERVICE_ERROR` | Dependent service failure | Retry, check status page |
| `MAINTENANCE_MODE` | System under maintenance | Check status page for ETA |
| `CONFIGURATION_ERROR` | System configuration issue | Contact support |

## Error Handling Best Practices

### 1. Implement Retry Logic

```javascript
async function callOcrApi(formData, maxRetries = 3) {
  for (let attempt = 1; attempt <= maxRetries; attempt++) {
    try {
      const response = await fetch('/api/v1/ocr', {
        method: 'POST',
        headers: {
          'Authorization': 'Bearer YOUR_API_KEY'
        },
        body: formData
      });

      if (response.ok) {
        return await response.json();
      }

      const error = await response.json();

      // Don't retry client errors (4xx)
      if (response.status >= 400 && response.status < 500) {
        throw new Error(error.error.message);
      }

      // Retry server errors (5xx) with exponential backoff
      if (attempt < maxRetries) {
        const delay = Math.pow(2, attempt) * 1000;
        await new Promise(resolve => setTimeout(resolve, delay));
      }
    } catch (error) {
      if (attempt === maxRetries) throw error;
    }
  }
}
```

### 2. User-Friendly Error Messages

```javascript
function getUserFriendlyError(apiError) {
  const errorMap = {
    'INVALID_API_KEY': 'Please check your API key and try again.',
    'SUBSCRIPTION_REQUIRED': 'A paid subscription is required. Please upgrade your account.',
    'MISSING_IMAGE_FILE': 'Please select an image file to upload.',
    'INVALID_DOCUMENT_TYPE': 'Please select a valid document type.',
    'AI_SERVICE_ERROR': 'Processing failed. Please try again or contact support.',
    'INSUFFICIENT_CREDITS': 'You have run out of credits. Please top up your account.',
    'RATE_LIMIT_EXCEEDED': 'Too many requests. Please wait a moment and try again.',
    'IMAGE_TOO_LARGE': 'Image is too large. Please use a smaller file (max 10MB).'
  };

  const reason = apiError.error.details?.[0]?.reason;
  return errorMap[reason] || 'An unexpected error occurred. Please try again.';
}
```

### 3. Comprehensive Error Logging

```javascript
function logApiError(error, context = {}) {
  const errorData = {
    timestamp: new Date().toISOString(),
    code: error.error.code,
    message: error.error.message,
    reason: error.error.details?.[0]?.reason,
    endpoint: context.endpoint,
    documentType: context.documentType,
    userAgent: navigator.userAgent,
    // Don't log sensitive data like API keys
  };

  console.error('API Error:', errorData);

  // Send to your error tracking service
  if (window.errorTracker) {
    window.errorTracker.log(errorData);
  }
}
```

### 4. Rate Limit Handling

```javascript
async function handleRateLimit(response) {
  const remaining = response.headers.get('X-RateLimit-Remaining');
  const reset = response.headers.get('X-RateLimit-Reset');

  if (remaining && parseInt(remaining) < 5) {
    console.warn(`Rate limit warning: ${remaining} requests remaining`);
  }

  if (response.status === 429) {
    const resetTime = new Date(parseInt(reset) * 1000);
    const waitTime = resetTime - new Date();

    throw new Error(`Rate limit exceeded. Try again at ${resetTime.toLocaleTimeString()}`);
  }
}
```

## Common Issues & Solutions

### "Invalid API Key" Error

**Problem**: Getting 401 Unauthorized with INVALID_API_KEY

**Solutions:**
1. Verify API key format: `Bearer sk_live_...`
2. Check key is active in dashboard
3. Ensure no extra spaces in header
4. Try regenerating API key
5. Check subscription status

### "AI Service Error" Error

**Problem**: Getting 500 Internal Server Error with AI_SERVICE_ERROR

**Solutions:**
1. Retry request (transient error)
2. Check image quality and clarity
3. Verify document type selection
4. Contact support if persistent
5. Check [status page](https://status.pictotext.io)

### "Invalid Document Type" Error

**Problem**: Getting 400 Bad Request with INVALID_DOCUMENT_TYPE

**Solutions:**
1. Use exact document type string (case-sensitive)
2. Check [supported documents](/docs/supported-documents.md) list
3. Avoid using "auto" for production
4. Verify no typos in document type

### Rate Limit Issues

**Problem**: Getting 429 Too Many Requests

**Solutions:**
1. Check rate limit headers in responses
2. Implement request queuing
3. Upgrade to higher plan
4. Contact support for custom limits
5. Implement exponential backoff

### Image Quality Issues

**Problem**: Low accuracy or processing errors

**Solutions:**
1. Ensure proper lighting and focus
2. Check image resolution (min 300 DPI)
3. Avoid shadows and glare
4. Ensure document is fully visible
5. Use supported image formats

### Field Extraction Issues

**Problem**: Some fields are missing from the result or are incorrect.

**Solutions:**
1. Ensure the specific field is not physically obscured, blurry, or affected by glare on the document.
2. For documents with multiple languages or complex layouts, the AI may occasionally misinterpret a field.
3. Address formatting can vary by region. Check the raw text to see if the address was extracted correctly but not parsed as expected.
4. Name parsing may differ for non-standard or minority names.

## Getting Help

If you encounter persistent errors:

1. **Check Status**: [Status page](https://status.pictotext.io)
2. **Review Request**: Compare with code examples
3. **Test in Dashboard**: Use web interface to isolate issues
4. **Contact Support**: Include error details

**Support Contact:**
- Email: support@pictotext.io
- Include: Error code, reason, timestamp, request details (sanitized)
- Response time: Within 24 hours (business days)

## Related Documentation

- [Authentication](./authentication.md) - API key management
- [Rate Limits](./limits.md) - Usage limits and quotas
- [Quickstart Guide](./quickstart.md) - Getting started
- [Supported Documents](./supported-documents.md) - Complete list of supported document types