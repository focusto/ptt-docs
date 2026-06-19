---
title: "France National ID Card"
description: "Complete API documentation for France National ID Card (CNIe) OCR with examples and field reference"
category: "reference"
region: "europe"
country: "france"
documentType: "fr_id_card"
language: "en"
order: 1
showInSidebar: true
---

# France National ID Card

Extract data from France National ID Card (CNIe) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `fr_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "MARTIN",
  "firstName": "MARIE",
  "documentNumber": "200123456789",
  "dateOfBirth": "1990-01-01",
  "placeOfBirth": "PARIS",
  "expiryDate": "2030-01-01",
  "issueDate": "2020-01-01",
  "gender": "F",
  "height": "1.70",
  "nationality": "FRANÇAISE",
  "address": "1 RUE DE LA PAIX, 75001 PARIS",
  "issuingAuthority": "PRÉFECTURE DE POLICE",
  "mrz": "IDFRMARTIN<<MARIE<<<<<<<<<<<<<<<<<<<<<<<\n1234567890123FRA9001018F3001012<<<"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `lastName` | string | Last name |
| `firstName` | string | First name |
| `documentNumber` | string | Document number |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `placeOfBirth` | string | Place of birth |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `gender` | string | Gender (M/F) |
| `height` | string | Height in meters |
| `nationality` | string | Nationality |
| `address` | string | Full address |
| `issuingAuthority` | string | Issuing authority |
| `mrz` | string | Machine Readable Zone. Preserve line breaks as `\n` exactly as printed. |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@france_id.jpg" \
  -F "documentType=fr_id_card"
```

### JavaScript (Browser)

```javascript
async function processFrenchIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'fr_id_card');

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

def extract_french_id_data(image_path, api_key):
    """Extract data from French ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'fr_id_card'}

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
  formData.append('documentType', 'fr_id_card');

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
- [All France Documents](../../../supported-documents.md#europe) - Other French documents
