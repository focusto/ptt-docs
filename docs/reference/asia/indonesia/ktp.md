---
title: "Indonesia KTP"
description: "Complete API documentation for Indonesia KTP (Kartu Tanda Penduduk) OCR with examples and field reference"
category: "reference"
region: "asia"
country: "indonesia"
documentType: "id_ktp"
language: "en"
order: 1
showInSidebar: true
---

# Indonesia KTP

Extract data from Indonesian KTP (Identity Card) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | KTP card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `id_ktp` |


## Response Format

### Success Response (200 OK)

```json
{
  "name": "BUDI SANTOSO",
  "id": "1234567890123456",
  "placeOfBirth": "JAKARTA",
  "dateOfBirth": "1990-01-01",
  "gender": "Male",
  "address": "JL. MERDEKA NO. 123",
  "rt": "001",
  "rw": "002",
  "village": "KEBON SIRIH",
  "district": "MENTENG",
  "religion": "ISLAM",
  "maritalStatus": "Single",
  "work": "EMPLOYEE",
  "nationality": "INDONESIAN",
  "city": "JAKARTA PUSAT",
  "province": "DKI JAKARTA"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `name` | string | Full name | BUDI SANTOSO |
| `id` | string | 16-digit ID number | 1234567890123456 |
| `placeOfBirth` | string | Place of birth | JAKARTA |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `gender` | string | Gender | Male |
| `address` | string | Full address | JL. MERDEKA NO. 123 |
| `rt` | string | Neighborhood unit (RT) | 001 |
| `rw` | string | Community unit (RW) | 002 |
| `village` | string | Village name | KEBON SIRIH |
| `district` | string | District name | MENTENG |
| `religion` | string | Religion | ISLAM |
| `maritalStatus` | string | Marital status | Single |
| `work` | string | Occupation | EMPLOYEE |
| `nationality` | string | Nationality | INDONESIAN |
| `city` | string | City name | JAKARTA PUSAT |
| `province` | string | Province name | DKI JAKARTA |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@ktp.jpg" \\
  -F "documentType=id_ktp"
```

### JavaScript (Browser)

```javascript
async function processKTP(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'id_ktp');

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
    console.error('Error processing KTP:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('ktp-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processKTP(file, 'YOUR_API_KEY');
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

def extract_ktp_data(image_path, api_key):
    """Extract data from KTP card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'id_ktp'}

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
result = extract_ktp_data('ktp.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['id'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract KTP data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processKTP(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'id_ktp');

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
processKTP('./ktp.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Indonesia Documents](../../../supported-documents#asia) - Other Indonesian documents