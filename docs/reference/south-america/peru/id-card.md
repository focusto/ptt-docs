---
title: "Peru ID Card"
description: "Complete API documentation for Peru ID Card (DNI) OCR with examples and field reference"
category: "reference"
region: "south-america"
country: "peru"
documentType: "pe_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Peru ID Card

Extract data from Peruvian ID Card (DNI) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `pe_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardNumber": "12345678",
  "dateOfBirth": "1990-01-01",
  "foreNames": "JUAN CARLOS",
  "placeOfBirthNo": "150101",
  "secondSurname": "GARCIA",
  "surname": "PEREZ",
  "dateOfExpiry": "2030-01-01",
  "dateOfIssue": "2020-01-01",
  "dateOfRegister": "2020-01-01",
  "gender": "Male",
  "maritalStatus": "Single",
  "nationality": "PERUVIAN"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardNumber` | string | DNI number | 12345678 |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `foreNames` | string | Given names | JUAN CARLOS |
| `placeOfBirthNo` | string | Place of birth code | 150101 |
| `secondSurname` | string | Mother's last name | GARCIA |
| `surname` | string | Father's last name | PEREZ |
| `dateOfExpiry` | string | Expiry date (YYYY-MM-DD) | 2030-01-01 |
| `dateOfIssue` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `dateOfRegister` | string | Registration date (YYYY-MM-DD) | 2020-01-01 |
| `gender` | string | Gender | Male |
| `maritalStatus` | string | Marital status | Single |
| `nationality` | string | Nationality | PERUVIAN |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@peru_id.jpg" \\
  -F "documentType=pe_id_card"
```

### JavaScript (Browser)

```javascript
async function processPeruIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'pe_id_card');

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
    console.error('Error processing Peru ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('peru-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPeruIDCard(file, 'YOUR_API_KEY');
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

def extract_peru_id_data(image_path, api_key):
    """Extract data from Peru ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'pe_id_card'}

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
result = extract_peru_id_data('peru_id.jpg', 'YOUR_API_KEY')
if result:
    print("DNI Number:", result['cardNumber'])
    print("Name:", result['foreNames'], result['surname'], result['secondSurname'])
    print("Full response:", result)
else:
    print("Failed to extract Peru ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPeruIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'pe_id_card');

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
processPeruIDCard('./peru_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Peru Documents](../../../supported-documents#south-america) - Other Peruvian documents