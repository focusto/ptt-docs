---
title: "Philippines Driver's License"
description: "Complete API documentation for Philippines Driver's License OCR with examples and field reference"
category: "reference"
region: "asia"
country: "philippines"
documentType: "ph_drivers_license"
language: "en"
order: 2
showInSidebar: true
---

# Philippines Driver's License

Extract data from Philippines Driver's License with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Driver's license image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ph_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "name": "JUAN M. DELA CRUZ",
  "lastName": "DELA CRUZ",
  "firstName": "JUAN",
  "middleName": "M",
  "nationality": "FILIPINO",
  "sex": "Male",
  "address": "123 MAIN STREET, QUEZON CITY",
  "licenseNo": "N01-23-456789",
  "expiresDate": "2025-01-01",
  "agencyCode": "LTO",
  "birthday": "1990-01-01"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `name` | string | Full name | JUAN M. DELA CRUZ |
| `lastName` | string | Last name | DELA CRUZ |
| `firstName` | string | First name | JUAN |
| `middleName` | string | Middle name | M |
| `nationality` | string | Nationality | FILIPINO |
| `sex` | string | Gender | Male |
| `address` | string | Complete address | 123 MAIN STREET, QUEZON CITY |
| `licenseNo` | string | License number | N01-23-456789 |
| `expiresDate` | string | Expiry date (YYYY-MM-DD) | 2025-01-01 |
| `agencyCode` | string | Issuing agency code | LTO |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@ph_drivers_license.jpg" \\
  -F "documentType=ph_drivers_license"
```

### JavaScript (Browser)

```javascript
async function processPHDriversLicense(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ph_drivers_license');

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
    console.error('Error processing Philippines driver\'s license:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('ph-license-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPHDriversLicense(file, 'YOUR_API_KEY');
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

def extract_ph_license_data(image_path, api_key):
    """Extract data from Philippines driver's license image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ph_drivers_license'}

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
result = extract_ph_license_data('ph_drivers_license.jpg', 'YOUR_API_KEY')
if result:
    print("License Number:", result['licenseNo'])
    print("Name:", result['firstName'], result['middleName'], result['lastName'])
    print("Full response:", result)
else:
    print("Failed to extract Philippines driver's license data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPHDriversLicense(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ph_drivers_license');

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
processPHDriversLicense('./ph_drivers_license.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Philippines Documents](../../../supported-documents#asia) - Other Philippine documents