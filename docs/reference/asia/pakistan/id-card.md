---
title: "Pakistan ID Card"
description: "Complete API documentation for Pakistan ID Card (CNIC) OCR with examples and field reference"
category: "reference"
region: "asia"
country: "pakistan"
documentType: "pk_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Pakistan ID Card

Extract data from Pakistan ID Card (CNIC - Computerized National Identity Card) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `pk_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "idNumber": "12345-6789012-3",
  "name": "MUHAMMAD ALI",
  "fatherName": "ABDUL RAHMAN",
  "gender": "Male",
  "country": "PAKISTAN",
  "birthDay": "1990-01-01",
  "issueDay": "2020-01-01",
  "expiryDay": "2030-01-01"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `idNumber` | string | CNIC number (format: 12345-6789012-3) | 12345-6789012-3 |
| `name` | string | Full name | MUHAMMAD ALI |
| `fatherName` | string | Father's name | ABDUL RAHMAN |
| `gender` | string | Gender | Male |
| `country` | string | Country | PAKISTAN |
| `birthDay` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `issueDay` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `expiryDay` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@pakistan_id.jpg" \
  -F "documentType=pk_id_card"
```

### JavaScript (Browser)

```javascript
async function processPakistanIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'pk_id_card');

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
    console.error('Error processing Pakistan ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('pakistan-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPakistanIDCard(file, 'YOUR_API_KEY');
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

def extract_pakistan_id_data(image_path, api_key):
    """Extract data from Pakistan ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'pk_id_card'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_forStatus()

            return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        if hasattr(e, 'response') and e.response is not None:
            print(f"Status code: {e.response.status_code}")
            print(f"Error response: {e.response.text}")
        return None

# Usage
result = extract_pakistan_id_data('pakistan_id.jpg', 'YOUR_API_KEY')
if result:
    print("CNIC Number:", result['idNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract Pakistan ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPakistanIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'pk_id_card');

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
processPakistanIDCard('./pakistan_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Pakistan Documents](../../../supported-documents.md#asia) - Other Pakistani documents
