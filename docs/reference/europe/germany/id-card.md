---
title: "Germany National ID Card"
description: "Complete API documentation for Germany National ID Card (Personalausweis) OCR with examples and field reference"
category: "reference"
region: "europe"
country: "germany"
documentType: "de_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Germany National ID Card

Extract data from Germany National ID Card (Personalausweis) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `de_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "MÜLLER",
  "firstName": "ERIKA",
  "documentNumber": "L01X00T28",
  "dateOfBirth": "1990-01-01",
  "nationality": "DEUTSCH",
  "placeOfBirth": "BERLIN",
  "expiryDate": "2030-01-01",
  "issueDate": "2020-01-01",
  "issuingAuthority": "STADT BERLIN",
  "address": "PLATZ DER REPUBLIK 1, 11011 BERLIN",
  "eyeColor": "BLAU",
  "height": "170",
  "mrz": "IDD<<L01X00T28<...\n6408125<1010318D<<<<<<<<<<<<<<04"
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
| `placeOfBirth` | string | Place of birth |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `issuingAuthority` | string | Issuing authority |
| `address` | string | Full address |
| `eyeColor` | string | Eye color |
| `height` | string | Height in cm |
| `mrz` | string | Machine Readable Zone. Preserve line breaks as `\n` exactly as printed. |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@germany_id.jpg" \
  -F "documentType=de_id_card"
```

### JavaScript (Browser)

```javascript
async function processGermanIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'de_id_card');

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

def extract_german_id_data(image_path, api_key):
    """Extract data from German ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'de_id_card'}

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
  formData.append('documentType', 'de_id_card');

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
- [All Germany Documents](../../../supported-documents.md#europe) - Other German documents

### Python

```python
import requests
import os

def extract_german_id_data(image_path, api_key):
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f)}
            data = {'documentType': 'de_id_card'}
            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()
            return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return None
```
