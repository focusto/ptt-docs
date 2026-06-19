---
title: "Egypt National ID Card"
description: "Complete API documentation for Egypt National ID Card OCR with examples and field reference"
category: "reference"
region: "africa"
country: "egypt"
documentType: "eg_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Egypt National ID Card

Extract data from Egypt National ID Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | National ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `eg_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "nationalNumber": "29001010112345",
  "name": "محمد علي",
  "dateOfBirth": "1990-01-01",
  "gender": "ذكر",
  "religion": "مسلم",
  "address": "1 شارع التحرير، القاهرة",
  "issuingOffice": "القاهرة",
  "profession": "مهندس",
  "issueDate": "2020-01-01",
  "expiryDate": "2027-01-01"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `nationalNumber` | string | National number |
| `name` | string | Full name |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `gender` | string | Gender |
| `religion` | string | Religion |
| `address` | string | Full address |
| `issuingOffice` | string | Issuing office |
| `profession` | string | Profession |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@egypt_id_card.jpg" \
  -F "documentType=eg_id_card"
```

### JavaScript (Browser)

```javascript
async function processEgyptIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'eg_id_card');

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

def extract_egypt_id_data(image_path, api_key):
    """Extract data from Egypt ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'eg_id_card'}

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
  formData.append('documentType', 'eg_id_card');

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
- [All Egypt Documents](../../../supported-documents.md#africa) - Other Egyptian documents

