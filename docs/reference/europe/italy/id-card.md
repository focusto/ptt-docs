---
title: "Italy Electronic ID Card"
description: "Complete API documentation for Italy Electronic ID Card (CIE) OCR with examples and field reference"
category: "reference"
region: "europe"
country: "italy"
documentType: "it_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Italy Electronic ID Card

Extract data from Italy Electronic ID Card (CIE) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `it_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "ROSSI",
  "firstName": "MARIO",
  "documentNumber": "CA1234567",
  "dateOfBirth": "1990-01-01",
  "placeOfBirth": "ROMA",
  "expiryDate": "2030-01-01",
  "issueDate": "2020-01-01",
  "gender": "M",
  "height": "175",
  "nationality": "ITALIANA",
  "taxCode": "RSSMRA90A01H501A",
  "address": "VIA DEL CORSO 1, 00100 ROMA",
  "mrz": "CITA1234567<...\nROSSI<<MARIO<<<<<<<<<<<<<<<<<<<<<<"
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
| `height` | string | Height in cm |
| `nationality` | string | Nationality |
| `taxCode` | string | Fiscal code (Codice Fiscale) |
| `address` | string | Full address |
| `mrz` | string | Machine Readable Zone. Preserve line breaks as `\n` exactly as printed. |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@italy_id.jpg" \
  -F "documentType=it_id_card"
```

### JavaScript (Browser)

```javascript
async function processItalianIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'it_id_card');

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

def extract_italian_id_data(image_path, api_key):
    """Extract data from Italian ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'it_id_card'}

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
  formData.append('documentType', 'it_id_card');

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
- [All Italy Documents](../../../supported-documents.md#europe) - Other Italian documents
