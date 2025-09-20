---
title: "Romania ID Card"
description: "Complete API documentation for Romania ID Card (Carte de Identitate) OCR with examples and field reference"
category: "reference"
region: "europe"
country: "romania"
documentType: "ro_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Romania ID Card

Extract data from Romanian ID Card (Carte de Identitate) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ro_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "series": "AX",
  "idNumber": "123456",
  "lastName": "POPESCU",
  "firstName": "ION",
  "nationality": "ROMANIAN",
  "placeOfBirth": "BUCURESTI",
  "address": "STRADA PRINCIPALA NR. 123",
  "issuedBy": "DIRECTIA GENERALA DE PASAPOARTE BUCURESTI",
  "validity": "2030-01-01"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `series` | string | ID card series | AX |
| `idNumber` | string | ID card number | 123456 |
| `lastName` | string | Last name | POPESCU |
| `firstName` | string | First name | ION |
| `nationality` | string | Nationality | ROMANIAN |
| `placeOfBirth` | string | Place of birth | BUCURESTI |
| `address` | string | Complete address | STRADA PRINCIPALA NR. 123 |
| `issuedBy` | string | Issuing authority | DIRECTIA GENERALA DE PASAPOARTE BUCURESTI |
| `validity` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@romania_id.jpg" \
  -F "documentType=ro_id_card"
```

### JavaScript (Browser)

```javascript
async function processRomaniaIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ro_id_card');

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
    console.error('Error processing Romania ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('romania-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processRomaniaIDCard(file, 'YOUR_API_KEY');
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

def extract_romania_id_data(image_path, api_key):
    """Extract data from Romania ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ro_id_card'}

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
result = extract_romania_id_data('romania_id.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['series'], result['idNumber'])
    print("Name:", result['firstName'], result['lastName'])
    print("Full response:", result)
else:
    print("Failed to extract Romania ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processRomaniaIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ro_id_card');

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
processRomaniaIDCard('./romania_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Romania Documents](../../../supported-documents.md#europe) - Other Romanian documents
