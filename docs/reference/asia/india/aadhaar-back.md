---
title: "India Aadhaar Back"
description: "Complete API documentation for India Aadhaar Back OCR with examples and field reference"
category: "reference"
region: "asia"
country: "india"
documentType: "in_aadhaar_back"
language: "en"
order: 2
showInSidebar: true
---

# India Aadhaar Back

Extract data from Indian Aadhaar card back side with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Aadhaar card back image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `in_aadhaar_back` |


## Response Format

### Success Response (200 OK)

```json
{
  "city": "New Delhi",
  "province": "Delhi",
  "postCode": "110001",
  "address": "123 Main Street, Connaught Place",
  "cardNumber": "123456789012",
  "vid": "112233445566"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `city` | string | City name | New Delhi |
| `province` | string | State or province | Delhi |
| `postCode` | string | Postal code | 110001 |
| `address` | string | Full residential address | 123 Main Street, Connaught Place |
| `cardNumber` | string | 12-digit Aadhaar card number | 123456789012 |
| `vid` | string | Virtual ID number | 112233445566 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@aadhaar_back.jpg" \
  -F "documentType=in_aadhaar_back"
```

### JavaScript (Browser)

```javascript
async function processAadhaarBack(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'in_aadhaar_back');

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
      const result = await processAadhaarBack(file, 'YOUR_API_KEY');
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

def extract_aadhaar_back_data(image_path, api_key):
    """Extract data from Aadhaar card back image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'in_aadhaar_back'}

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
result = extract_aadhaar_back_data('aadhaar_back.jpg', 'YOUR_API_KEY')
if result:
    print("Address:", result['address'])
    print("City:", result['city'])
    print("Full response:", result)
else:
    print("Failed to extract Aadhaar data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processAadhaarBack(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'in_aadhaar_back');

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
processAadhaarBack('./aadhaar_back.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All India Documents](../../../supported-documents.md#asia) - Other Indian documents
