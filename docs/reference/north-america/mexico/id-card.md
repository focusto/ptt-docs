---
title: "Mexican ID Card"
description: "Complete API documentation for Mexican ID Card (INE/IFE) OCR with examples and field reference"
category: "reference"
region: "north-america"
country: "mexico"
documentType: "mx_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Mexican ID Card

Extract data from Mexican ID Card (INE/IFE) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `mx_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "fullName": "JUAN PEREZ GARCIA",
  "fatherLastName": "PEREZ",
  "motherLastName": "GARCIA",
  "name": "JUAN",
  "birthday": "1990-01-01",
  "gender": "Male",
  "idNumber": "ABCDEFGHIJKLMNOP",
  "voterId": "ABCD123456789012",
  "addressAll": "AVENIDA REFORMA 123, COLONIA CENTRO, CIUDAD DE MEXICO",
  "state": "CIUDAD DE MEXICO",
  "district": "DISTRITO FEDERAL",
  "subDistrict": "SUB DISTRITO 01",
  "postalCode": "06000",
  "issueYear": "2020",
  "expiryYear": "2030",
  "registrationYearAndMonth": "202001",
  "municipalNumber": "001",
  "placeNumber": "123",
  "stateNumber": "09"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `fullName` | string | Complete full name | JUAN PEREZ GARCIA |
| `fatherLastName` | string | Father's last name | PEREZ |
| `motherLastName` | string | Mother's last name | GARCIA |
| `name` | string | First name | JUAN |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `gender` | string | Gender | Male |
| `idNumber` | string | ID card number | ABCDEFGHIJKLMNOP |
| `voterId` | string | Voter ID number | ABCD123456789012 |
| `addressAll` | string | Complete address | AVENIDA REFORMA 123, COLONIA CENTRO, CIUDAD DE MEXICO |
| `state` | string | State name | CIUDAD DE MEXICO |
| `district` | string | Electoral district | DISTRITO FEDERAL |
| `subDistrict` | string | Sub-district | SUB DISTRITO 01 |
| `postalCode` | string | Postal code | 06000 |
| `issueYear` | string | Issue year | 2020 |
| `expiryYear` | string | Expiry year | 2030 |
| `registrationYearAndMonth` | string | Registration year and month | 202001 |
| `municipalNumber` | string | Municipal number | 001 |
| `placeNumber` | string | Place number | 123 |
| `stateNumber` | string | State number | 09 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@mexican_id.jpg" \
  -F "documentType=mx_id_card"
```

### JavaScript (Browser)

```javascript
async function processMexicanIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'mx_id_card');

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
    console.error('Error processing Mexican ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('mexican-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processMexicanIDCard(file, 'YOUR_API_KEY');
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

def extract_mexican_id_data(image_path, api_key):
    """Extract data from Mexican ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'mx_id_card'}

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
result = extract_mexican_id_data('mexican_id.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['idNumber'])
    print("Full Name:", result['fullName'])
    print("Full response:", result)
else:
    print("Failed to extract Mexican ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processMexicanIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'mx_id_card');

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
processMexicanIDCard('./mexican_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Mexico Documents](../../../supported-documents.md#north-america) - Other Mexican documents
