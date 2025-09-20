---
title: "India Aadhaar Front"
description: "Complete API documentation for India Aadhaar Front OCR with examples and field reference"
category: "reference"
region: "asia"
country: "india"
documentType: "in_aadhaar_front"
language: "en"
order: 1
showInSidebar: true
---

# India Aadhaar Front

Extract data from Indian Aadhaar card front side with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Aadhaar card front image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `in_aadhaar_front` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardNumber": "123456789012",
  "dateOfBirth": "1990-01-01",
  "downloadDate": "2023-01-01",
  "gender": "Male",
  "issueDate": "2020-01-01",
  "mobileNumber": "+919876543210",
  "name": "RAJESH KUMAR",
  "vid": "112233445566"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardNumber` | string | 12-digit Aadhaar card number | 123456789012 |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `downloadDate` | string | Date when Aadhaar was downloaded | 2023-01-01 |
| `gender` | string | Gender | Male |
| `issueDate` | string | Issue date of Aadhaar card | 2020-01-01 |
| `mobileNumber` | string | Registered mobile number | +919876543210 |
| `name` | string | Full name as on Aadhaar card | RAJESH KUMAR |
| `vid` | string | Virtual ID number | 112233445566 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@aadhaar_front.jpg" \
  -F "documentType=in_aadhaar_front"
```

### JavaScript (Browser)

```javascript
async function processAadhaarFront(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'in_aadhaar_front');

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
    console.error('Error processing Aadhaar card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('aadhaar-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processAadhaarFront(file, 'YOUR_API_KEY');
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

def extract_aadhaar_front_data(image_path, api_key):
    """Extract data from Aadhaar card front image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'in_aadhaar_front'}

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
result = extract_aadhaar_front_data('aadhaar_front.jpg', 'YOUR_API_KEY')
if result:
    print("Aadhaar Number:", result['cardNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract Aadhaar data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processAadhaarFront(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'in_aadhaar_front');

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
processAadhaarFront('./aadhaar_front.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All India Documents](../../../supported-documents.md#asia) - Other Indian documents
