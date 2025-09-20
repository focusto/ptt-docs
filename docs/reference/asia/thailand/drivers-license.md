---
title: "Thailand Driver's License"
description: "Complete API documentation for Thailand Driver's License OCR with examples and field reference"
category: "reference"
region: "asia"
country: "thailand"
documentType: "th_drivers_license"
language: "en"
order: 2
showInSidebar: true
---

# Thailand Driver's License

Extract data from Thai Driver's License with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Driver's license image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `th_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardTypeTh": "ใบอนุญาตขับรถ",
  "cardTypeEn": "Driver's License",
  "licenseNumber": "DL123456789",
  "idNumber": "1234567890123",
  "nameTh": "สมชาย ใจดี",
  "nameEn": "SOMCHAI JAIDEE",
  "birthTh": "๑ มกราคม ๒๕๓๓",
  "birthEn": "1990-01-01",
  "issueDate": "2020-01-01",
  "expiryDate": "2025-01-01"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardTypeTh` | string | Card type in Thai | ใบอนุญาตขับรถ |
| `cardTypeEn` | string | Card type in English | Driver's License |
| `licenseNumber` | string | Driver's license number | DL123456789 |
| `idNumber` | string | 13-digit ID number | 1234567890123 |
| `nameTh` | string | Full name in Thai | สมชาย ใจดี |
| `nameEn` | string | Full name in English | SOMCHAI JAIDEE |
| `birthTh` | string | Birth date in Thai | ๑ มกราคม ๒๕๓๓ |
| `birthEn` | string | Birth date in English (YYYY-MM-DD) | 1990-01-01 |
| `issueDate` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `expiryDate` | string | Expiry date (YYYY-MM-DD) | 2025-01-01 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@thai_drivers_license.jpg" \
  -F "documentType=th_drivers_license"
```

### JavaScript (Browser)

```javascript
async function processThaiDriversLicense(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'th_drivers_license');

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
    console.error('Error processing Thai driver\'s license:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('thai-license-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processThaiDriversLicense(file, 'YOUR_API_KEY');
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

def extract_thai_license_data(image_path, api_key):
    """Extract data from Thai driver's license image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'th_drivers_license'}

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
result = extract_thai_license_data('thai_drivers_license.jpg', 'YOUR_API_KEY')
if result:
    print("License Number:", result['licenseNumber'])
    print("Name (English):", result['nameEn'])
    print("Full response:", result)
else:
    print("Failed to extract Thai driver's license data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processThaiDriversLicense(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'th_drivers_license');

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
processThaiDriversLicense('./thai_drivers_license.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Thailand Documents](../../../supported-documents.md#asia) - Other Thai documents
