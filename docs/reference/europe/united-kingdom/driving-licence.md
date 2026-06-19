---
title: "United Kingdom Driving Licence"
description: "Complete API documentation for United Kingdom Driving Licence OCR with examples and field reference"
category: "reference"
region: "europe"
country: "united-kingdom"
documentType: "gb_drivers_license"
language: "en"
order: 1
showInSidebar: true
---

# United Kingdom Driving Licence

Extract data from United Kingdom Driving Licence with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Driving licence image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `gb_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "SMITH",
  "firstName": "JOHN",
  "driverNumber": "SMITH1234567A99A",
  "dateOfBirth": "1990-01-01",
  "placeOfBirth": "LONDON",
  "issueDate": "2020-01-01",
  "expiryDate": "2030-01-01",
  "issuingAuthority": "DVLA",
  "address": "1 ANY STREET, ANYTOWN, AB12 3CD",
  "vehicleCategories": "B, B1"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `lastName` | string | Last name |
| `firstName` | string | First name |
| `driverNumber` | string | Driver number |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `placeOfBirth` | string | Place of birth |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |
| `issuingAuthority` | string | Issuing authority (e.g., DVLA) |
| `address` | string | Full address |
| `vehicleCategories` | string | Vehicle categories |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@uk_driving_licence.jpg" \
  -F "documentType=gb_drivers_license"
```

### JavaScript (Browser)

```javascript
async function processUKDrivingLicence(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'gb_drivers_license');

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
    console.error('Error processing driving licence:', error);
    throw error;
  }
}
```

### Python

```python
import requests
import os

def extract_uk_driving_licence_data(image_path, api_key):
    """Extract data from UK Driving Licence image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'gb_drivers_license'}

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

async function processDrivingLicence(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'gb_drivers_license');

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
- [All United Kingdom Documents](../../../supported-documents.md#europe) - Other UK documents
```