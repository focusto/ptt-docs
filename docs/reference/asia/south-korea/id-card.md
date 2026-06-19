---
title: "South Korea Resident Registration Card"
description: "Complete API documentation for South Korea Resident Registration Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "south-korea"
documentType: "kr_id_card"
language: "en"
order: 1
showInSidebar: true
---

# South Korea Resident Registration Card

Extract data from South Korea Resident Registration Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Resident registration card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `kr_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "name": "홍길동",
  "residentRegistrationNumber": "900101-1234567",
  "issueDate": "2020-01-01",
  "issuingAuthority": "서울특별시 종로구청장",
  "address": "서울특별시 종로구 세종대로 1",
  "fingerprint": "(Binary data or placeholder)"
}
```


### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Full name |
| `residentRegistrationNumber` | string | Resident registration number |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `issuingAuthority` | string | Issuing authority |
| `address` | string | Full address |
| `fingerprint` | string | Placeholder for fingerprint data |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@korea_id_card.jpg" \
  -F "documentType=kr_id_card"
```

### JavaScript (Browser)

```javascript
async function processKoreanIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'kr_id_card');

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
    console.error('Error processing ID card:', error);
    throw error;
  }
}
```

### Python

```python
import requests
import os

def extract_korean_id_data(image_path, api_key):
    """Extract data from South Korean ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'kr_id_card'}

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

async function processIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'kr_id_card');

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
- [All South Korea Documents](../../../supported-documents.md#asia) - Other South Korean documents
```