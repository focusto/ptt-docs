---
title: "Ghana ID Card"
description: "Complete API documentation for Ghana ID Card (Ghana Card) OCR with examples and field reference"
category: "reference"
region: "africa"
country: "ghana"
documentType: "gh_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Ghana ID Card

Extract data from Ghana ID Card (Ghana Card) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `gh_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "dateOfBirth": "1990-01-01",
  "dateOfExpiry": "2030-01-01",
  "dateOfIssue": "2020-01-01",
  "documentId": "GHA-123456789-0",
  "firstname": "KWAME",
  "gender": "Male",
  "nationality": "GHANAIAN",
  "personalId": "1234567890",
  "placeOfIssue": "ACCRA",
  "surname": "MENSAH"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `dateOfExpiry` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |
| `dateOfIssue` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `documentId` | string | Document ID | GHA-123456789-0 |
| `firstname` | string | First name | KWAME |
| `gender` | string | Gender | Male |
| `nationality` | string | Nationality | GHANAIAN |
| `personalId` | string | Personal ID number | 1234567890 |
| `placeOfIssue` | string | Place of issue | ACCRA |
| `surname` | string | Surname | MENSAH |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@ghana_id.jpg" \
  -F "documentType=gh_id_card"
```

### JavaScript (Browser)

```javascript
async function processGhanaIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'gh_id_card');

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
    console.error('Error processing Ghana ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('ghana-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processGhanaIDCard(file, 'YOUR_API_KEY');
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

def extract_ghana_id_data(image_path, api_key):
    """Extract data from Ghana ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'gh_id_card'}

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
result = extract_ghana_id_data('ghana_id.jpg', 'YOUR_API_KEY')
if result:
    print("Personal ID:", result['personalId'])
    print("Name:", result['firstname'], result['surname'])
    print("Full response:", result)
else:
    print("Failed to extract Ghana ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processGhanaIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'gh_id_card');

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
processGhanaIDCard('./ghana_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Ghana Documents](../../../supported-documents.md#africa) - Other Ghanaian documents
