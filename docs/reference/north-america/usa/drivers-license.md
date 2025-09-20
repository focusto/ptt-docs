---
title: "US Driver's License"
description: "Complete API documentation for US Driver's License OCR with examples and field reference"
category: "reference"
region: "north-america"
country: "usa"
documentType: "us_drivers_license"
language: "en"
order: 1
showInSidebar: true
---

# US Driver's License

Extract data from US Driver's License with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Driver's license image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `us_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "firstName": "JOHN",
  "lastName": "DOE",
  "licenseNumber": "D123456789012",
  "dateOfBirth": "1990-01-01",
  "issueDate": "2020-01-01",
  "expiryDate": "2025-01-01",
  "address": "123 MAIN STREET",
  "city": "LOS ANGELES",
  "state": "CA",
  "zipCode": "90001"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `firstName` | string | First name | JOHN |
| `lastName` | string | Last name | DOE |
| `licenseNumber` | string | Driver's license number | D123456789012 |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `issueDate` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) | 2025-01-01 |
| `address` | string | Street address | 123 MAIN STREET |
| `city` | string | City name | LOS ANGELES |
| `state` | string | State abbreviation | CA |
| `zipCode` | string | ZIP code | 90001 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@us_drivers_license.jpg" \
  -F "documentType=us_drivers_license"
```

### JavaScript (Browser)

```javascript
async function processUSDriversLicense(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'us_drivers_license');

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
    console.error('Error processing US driver\'s license:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('us-license-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processUSDriversLicense(file, 'YOUR_API_KEY');
      console.log('Extracted data:', result);
    } catch (error) {
      alert('Processing failed: ' + error.message);
    }
  }
});
```

### Python

```python
import requests
import os

def extract_us_license_data(image_path, api_key):
    """Extract data from US driver\'s license image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'us_drivers_license'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()

            return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        if hasattr(e, 'response') and e.response is not None:
            print(f"Status code: {e.response.status_code}")
            print(f"Error response: {e.response.text}")
        return None

# Usage
result = extract_us_license_data('us_drivers_license.jpg', 'YOUR_API_KEY')
if result:
    print("License Number:", result['licenseNumber'])
    print("Name:", result['firstName'], result['lastName'])
    print("Full response:", result)
else:
    print("Failed to extract US driver's license data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processUSDriversLicense(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'us_drivers_license');

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

// Usage
processUSDriversLicense('./us_drivers_license.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All USA Documents](../../../supported-documents.md#north-america) - Other US documents
