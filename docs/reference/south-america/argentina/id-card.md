---
title: "Argentina ID Card"
description: "Complete API documentation for Argentina ID Card OCR with examples and field reference"
category: "reference"
region: "south-america"
country: "argentina"
documentType: "ar_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Argentina ID Card

Extract data from Argentine ID Card (DNI) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ar_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "dateOfBirth": "1990-01-01",
  "dateOfExpiry": "2030-01-01",
  "dateOfIssue": "2020-01-01",
  "documentNumber": "12345678",
  "gender": "Male",
  "givenName": "JUAN",
  "surname": "PEREZ",
  "nationality": "ARGENTINE"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `dateOfExpiry` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |
| `dateOfIssue` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `documentNumber` | string | Document number | 12345678 |
| `gender` | string | Gender | Male |
| `givenName` | string | Given name | JUAN |
| `surname` | string | Surname | PEREZ |
| `nationality` | string | Nationality | ARGENTINE |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@argentina_id.jpg" \\
  -F "documentType=ar_id_card"
```

### JavaScript (Browser)

```javascript
async function processArgentinaIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ar_id_card');

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
    console.error('Error processing Argentina ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('argentina-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processArgentinaIDCard(file, 'YOUR_API_KEY');
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

def extract_argentina_id_data(image_path, api_key):
    """Extract data from Argentina ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ar_id_card'}

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
result = extract_argentina_id_data('argentina_id.jpg', 'YOUR_API_KEY')
if result:
    print("Document Number:", result['documentNumber'])
    print("Name:", result['givenName'], result['surname'])
    print("Full response:", result)
else:
    print("Failed to extract Argentina ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processArgentinaIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ar_id_card');

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
processArgentinaIDCard('./argentina_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Argentina Documents](../../../supported-documents#south-america) - Other Argentine documents