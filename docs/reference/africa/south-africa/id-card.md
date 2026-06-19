---
title: "South Africa Smart ID Card"
description: "Complete API documentation for South Africa Smart ID Card OCR with examples and field reference"
category: "reference"
region: "africa"
country: "south-africa"
documentType: "za_id_card"
language: "en"
order: 1
showInSidebar: true
---

# South Africa Smart ID Card

Extract data from South Africa Smart ID Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Smart ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `za_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "BOTHA",
  "firstName": "JOHAN",
  "identityNumber": "9001011234081",
  "dateOfBirth": "1990-01-01",
  "countryOfBirth": "SOUTH AFRICA",
  "nationality": "SOUTH AFRICAN",
  "gender": "MALE",
  "citizenshipStatus": "CITIZEN",
  "issueDate": "2020-01-01",
  "pdf417BarcodeData": "(Binary data or placeholder)"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `lastName` | string | Last name |
| `firstName` | string | First name |
| `identityNumber` | string | Identity number |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `countryOfBirth` | string | Country of birth |
| `nationality` | string | Nationality |
| `gender` | string | Gender |
| `citizenshipStatus` | string | Citizenship status |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `pdf417BarcodeData` | string | Placeholder for PDF417 barcode data |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@safrica_id_card.jpg" \
  -F "documentType=za_id_card"
```

### JavaScript (Browser)

```javascript
async function processSouthAfricaIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'za_id_card');

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

def extract_south_africa_id_data(image_path, api_key):
    """Extract data from South Africa Smart ID Card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'za_id_card'}

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
  formData.append('documentType', 'za_id_card');

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
- [All South Africa Documents](../../../supported-documents.md#africa) - Other South African documents
```