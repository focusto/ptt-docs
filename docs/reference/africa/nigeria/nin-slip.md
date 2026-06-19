---
title: "Nigeria NIN Slip"
description: "Complete API documentation for Nigeria NIN Slip OCR with examples and field reference"
category: "reference"
region: "africa"
country: "nigeria"
documentType: "ng_nin_slip"
language: "en"
order: 1
showInSidebar: true
---

# Nigeria NIN Slip

Extract data from Nigeria NIN Slip with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | NIN slip image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `ng_nin_slip` |


## Response Format

### Success Response (200 OK)

```json
{
  "firstName": "CHINEDU",
  "lastName": "EZE",
  "middleName": "OBI",
  "nationalIdentificationNumber": "12345678901",
  "dateOfBirth": "1990-01-01",
  "gender": "M",
  "issueDate": "2020-01-01",
  "trackingId": "ABC-123456789-XYZ"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `firstName` | string | First name |
| `lastName` | string | Last name |
| `middleName` | string | Middle name |
| `nationalIdentificationNumber` | string | National Identification Number |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `gender` | string | Gender (M/F) |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `trackingId` | string | Tracking ID |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@nigeria_nin_slip.jpg" \
  -F "documentType=ng_nin_slip"
```

### JavaScript (Browser)

```javascript
async function processNigeriaNINSlip(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ng_nin_slip');

  try {
    const response = await fetch('https://pictotext.io/api/v1/ocr', {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${apiKey}`
      },
      body: formData
    });

    if (!response.ok) {
      const error = await response.json();
      throw new Error(error.error.message);
    }

    return await response.json();
  } catch (error) {
    console.error('Error processing NIN slip:', error);
    throw error;
  }
}
```

### Python

```python
import requests
import os

def extract_nigeria_nin_slip_data(image_path, api_key):
    """Extract data from Nigeria NIN Slip image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ng_nin_slip'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()

            return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        if hasattr(e, 'response') and e.response is not None:
            print(f"Status code: {e.response.status_code}")
            print(f"Error response: {e.response.text}")
        return None
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processNINSlip(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ng_nin_slip');

  try {
    const response = await axios.post('https://pictotext.io/api/v1/ocr', formData, {
      headers: {
        ...formData.getHeaders(),
        'Authorization': `Bearer ${apiKey}`
      }
    });

    return response.data;
  } catch (error) {
    if (error.response) {
      console.error('API Error:', error.response.data);
    }
    throw error;
  }
}
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Usage and Limits](../../../limits.md) - Usage limits and quotas
- [All Nigeria Documents](../../../supported-documents.md#africa) - Other Nigerian documents
