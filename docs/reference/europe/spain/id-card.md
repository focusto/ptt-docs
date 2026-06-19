---
title: "Spain National ID Card"
description: "Complete API documentation for Spain National ID Card (DNIe) OCR with examples and field reference"
category: "reference"
region: "europe"
country: "spain"
documentType: "es_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Spain National ID Card

Extract data from Spain National ID Card (DNIe) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `es_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "GARCÍA",
  "firstName": "MARÍA",
  "documentNumber": "12345678Z",
  "dateOfBirth": "1990-01-01",
  "nationality": "ESPAÑOLA",
  "expiryDate": "2030-01-01",
  "gender": "F",
  "parentsNames": "JOSE Y CARMEN",
  "address": "CALLE MAYOR 1, 28001 MADRID",
  "placeOfIssue": "MADRID",
  "mrz": "IDESP12345678Z<...\nGARCIA<<MARIA<<<<<<<<<<<<<<<<<<<<"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `lastName` | string | Last name |
| `firstName` | string | First name |
| `documentNumber` | string | Document number |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `nationality` | string | Nationality |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |
| `gender` | string | Gender (M/F) |
| `parentsNames` | string | Names of the parents |
| `address` | string | Full address |
| `placeOfIssue` | string | Place of issue |
| `mrz` | string | Machine Readable Zone. Preserve line breaks as `\n` exactly as printed. |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@spain_id.jpg" \
  -F "documentType=es_id_card"
```

### JavaScript (Browser)

```javascript
async function processSpanishIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'es_id_card');

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

def extract_spanish_id_data(image_path, api_key):
    """Extract data from Spanish ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'es_id_card'}

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
  formData.append('documentType', 'es_id_card');

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
- [All Spain Documents](../../../supported-documents.md#europe) - Other Spanish documents
