---
title: "Error Reference"
description: "Complete reference for API errors and troubleshooting"
category: "guide"
language: "en"
order: 3
showInSidebar: true
---

# Error Reference

Complete reference for handling PicToText API errors with the error codes currently returned by the live OCR endpoints.

## Error Format

OCR API errors generally follow this JSON structure:

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
    "message": "Unsupported image MIME type: text/plain. Supported types: image/jpeg, image/jpg, image/png, image/webp, image/heic, image/heif.",
    "status": "Bad Request",
    "details": [{
      "reason": "INVALID_IMAGE_TYPE",
      "metadata": {
        "received": "text/plain",
        "supported": ["image/jpeg", "image/jpg", "image/png", "image/webp", "image/heic", "image/heif"]
      }
    }]
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
Insufficient credits when no included quota is available.

**Example:**
```json
{
  "error": {
    "code": 402,
    "message": "You have no remaining included quota or credits. Please purchase credits or upgrade your plan to continue.",
    "status": "Payment Required",
    "details": [{ "reason": "INSUFFICIENT_CREDITS" }]
  }
}
```

### 403 Forbidden
Access denied due to verification or access control requirements.

**Common Causes:**
- Email verification required

**Example:**
```json
{
  "error": {
    "code": 403,
    "message": "Email verification required before using the API.",
    "status": "Forbidden",
    "details": [{ "reason": "EMAIL_NOT_VERIFIED" }]
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

## Error Codes Reference

### Authentication Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `INVALID_AUTH_HEADER` | Missing or malformed Authorization header | Use format: `Bearer YOUR_API_KEY` |
| `INVALID_API_KEY` | API key not found or inactive | Check key in dashboard |
| `EMAIL_NOT_VERIFIED` | Email verification is required before using the OCR API | Verify your account email, then retry |

### Request Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `MISSING_IMAGE_FILE` | No image file provided | Include image in form data |
| `INVALID_DOCUMENT_TYPE` | Unsupported or missing document type | Check [supported documents](https://pictotext.io/docs/supported-documents) |
| `INVALID_IMAGE_TYPE` | Uploaded file MIME type is not supported | Use `multipart/form-data` and one of: `image/jpeg`, `image/jpg`, `image/png`, `image/webp`, `image/heic`, `image/heif` |
| `IMAGE_TOO_LARGE` | Image exceeds 10MB limit | Resize or compress image |

### Processing Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `AI_SERVICE_ERROR` | AI processing failed | Retry request, contact support if persists |
| `INTERNAL_ERROR` | An unhandled server error occurred before the OCR endpoint could return a normal result | Retry the request. If it persists, contact support |

### Account & Plan Errors

| Reason Code | Description | Solution |
|-------------|-------------|----------|
| `INSUFFICIENT_CREDITS` | No remaining included quota or credits for the account | Purchase more credits or upgrade your plan |

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
    'EMAIL_NOT_VERIFIED': 'Please verify your email address before using the API.',
    'MISSING_IMAGE_FILE': 'Please select an image file to upload.',
    'INVALID_DOCUMENT_TYPE': 'Please select a valid document type.',
    'INVALID_IMAGE_TYPE': 'Please upload a supported image file and ensure the request uses the correct image MIME type.',
    'AI_SERVICE_ERROR': 'Processing failed. Please try again or contact support.',
    'INSUFFICIENT_CREDITS': 'You have run out of credits. Please top up your account.',
    'IMAGE_TOO_LARGE': 'Image is too large. Please use a smaller file (max 10MB).',
    'INTERNAL_ERROR': 'An internal server error occurred. Please try again later.'
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

### "Insufficient Credits" Error

**Problem**: Getting 402 Payment Required with INSUFFICIENT_CREDITS

**Solutions:**
1. Purchase additional credits
2. Upgrade to a plan with included quota
3. Verify that your account still has available API credit

### "Invalid Document Type" Error

**Problem**: Getting 400 Bad Request with INVALID_DOCUMENT_TYPE

**Solutions:**
1. Use exact document type string (case-sensitive)
2. Check [supported documents](./supported-documents.md) list
3. Avoid using "auto" for production
4. Verify no typos in document type

### "Invalid Image Type" Error

**Problem**: Getting 400 Bad Request with INVALID_IMAGE_TYPE

**Solutions:**
1. Send the request as `multipart/form-data`
2. Upload the image in the `image` field as a real file part
3. Use one of these MIME types: `image/jpeg`, `image/jpg`, `image/png`, `image/webp`, `image/heic`, `image/heif`
4. Do not send base64 text, file paths, or plain strings as the `image` field
5. If using Python, open the file in binary mode and pass it via `files=...`

### "Image Too Large" Error

**Problem**: Getting 400 Bad Request with IMAGE_TOO_LARGE

**Solutions:**
1. Keep the upload at or below 10MB
2. Resize or compress the image before uploading
3. If possible, crop large empty regions before sending the file

### "Email Not Verified" Error

**Problem**: Getting 403 Forbidden with EMAIL_NOT_VERIFIED

**Solutions:**
1. Verify the email address on the account that owns the API key
2. Retry the request after verification is complete

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

1. **Review Request**: Compare with [code examples](./quickstart.md)
2. **Test in Dashboard**: Use web interface to isolate issues
3. **Contact Support**: Include error details

**Support Contact:**
- Email: support@pictotext.io
- Include: Error code, reason, timestamp, request details (sanitized)
- Response time: Within 24 hours (business days)

## Related Documentation

- [Authentication](./authentication.md) - API key management
- [Usage and Limits](./limits.md) - Usage limits and quotas
- [Quickstart Guide](./quickstart.md) - Getting started
- [Supported Documents](./supported-documents.md) - Complete list of supported document types
