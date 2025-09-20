---
title: "Passport"
description: "Complete API documentation for Passport OCR with examples and field reference"
category: "reference"
region: "international"
country: "international"
documentType: "passport"
language: "en"
order: 1
showInSidebar: true
---

# Passport

Extract data from passports with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Passport image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `passport` |


## Response Format

### Success Response (200 OK)

```json
{
  "passportNumber": "P12345678",
  "name": "JOHN MICHAEL DOE",
  "gender": "Male",
  "birthDay": "1990-01-01",
  "birthPlace": "NEW YORK, USA",
  "issueDay": "2020-01-01",
  "expiryDay": "2030-01-01",
  "issuePlace": "WASHINGTON D.C.",
  "nationality": "UNITED STATES OF AMERICA"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `passportNumber` | string | Passport number | P12345678 |
| `name` | string | Full name as in passport | JOHN MICHAEL DOE |
| `gender` | string | Gender | Male |
| `birthDay` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `birthPlace` | string | Place of birth | NEW YORK, USA |
| `issueDay` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `expiryDay` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |
| `issuePlace` | string | Place of issue | WASHINGTON D.C. |
| `nationality` | string | Nationality | UNITED STATES OF AMERICA |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@passport.jpg" \
  -F "documentType=passport"
```

### JavaScript (Browser)

```javascript
async function processPassport(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'passport');

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
    console.error('Error processing passport:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('passport-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPassport(file, 'YOUR_API_KEY');
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

def extract_passport_data(image_path, api_key):
    """Extract data from passport image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'passport'}

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
result = extract_passport_data('passport.jpg', 'YOUR_API_KEY')
if result:
    print("Passport Number:", result['passportNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract passport data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPassport(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'passport');

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
processPassport('./passport.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../authentication.md) - API key management
- [Error Reference](../../errors.md) - Complete error codes
- [Rate Limits](../../limits.md) - Usage limits and quotas
- [All International Documents](../../supported-documents.md#international) - Other international documents
