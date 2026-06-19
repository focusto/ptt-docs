---
title: "Canada Provincial Driver's License"
description: "Complete API documentation for Canada Provincial Driver's License OCR with examples and field reference"
category: "reference"
region: "north-america"
country: "canada"
documentType: "ca_drivers_license"
language: "en"
order: 1
showInSidebar: true
---

# Canada Provincial Driver's License

Extract data from Canada Provincial Driver's License with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Driver's license image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `ca_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "firstName": "JAMES",
  "lastName": "SMITH",
  "licenseNumber": "S1234-56789-01234",
  "licenseClass": "G",
  "dateOfBirth": "1990-01-01",
  "issueDate": "2020-01-01",
  "expiryDate": "2025-01-01",
  "address": "123 YONGE ST, TORONTO, ON M5B 2H1",
  "gender": "M",
  "height": "180 cm",
  "eyeColor": "BLU",
  "hairColor": "BRN",
  "weight": "82 kg",
  "restrictions": "Corrective lenses",
  "organDonorStatus": "Yes",
  "documentDiscriminator": "1234567890"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `firstName` | string | First name |
| `lastName` | string | Last name |
| `licenseNumber` | string | License number |
| `licenseClass` | string | License class (e.g., G, 5) |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) |
| `issueDate` | string | Issue date (YYYY-MM-DD) |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) |
| `address` | string | Full address |
| `gender` | string | Gender (M/F) |
| `height` | string | Height |
| `eyeColor` | string | Eye color |
| `hairColor` | string | Hair color |
| `weight` | string | Weight |
| `restrictions` | string | Restrictions noted on the license |
| `organDonorStatus` | string | Organ donor status |
| `documentDiscriminator` | string | Document discriminator identifier |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@canada_drivers_license.jpg" \
  -F "documentType=ca_drivers_license"
```

### JavaScript (Browser)

```javascript
async function processCanadaDriversLicense(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ca_drivers_license');

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
    console.error('Error processing driver\'s license:', error);
    throw error;
  }
}
```

### Python

```python
import requests
import os

def extract_canada_drivers_license_data(image_path, api_key):
    """Extract data from Canada Provincial Driver's License image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ca_drivers_license'}

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

async function processDriversLicense(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ca_drivers_license');

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
- [All Canada Documents](../../../supported-documents.md#north-america) - Other Canadian documents
