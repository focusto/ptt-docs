---
title: "Philippines UMID"
description: "Complete API documentation for Philippines UMID (Unified Multi-Purpose ID) OCR with examples and field reference"
category: "reference"
region: "asia"
country: "philippines"
documentType: "ph_umid"
language: "en"
order: 4
showInSidebar: true
---

# Philippines UMID

Extract data from Philippines UMID (Unified Multi-Purpose ID) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | UMID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ph_umid` |


## Response Format

### Success Response (200 OK)

```json
{
  "crn": "123456789012",
  "surname": "DELA CRUZ",
  "givenName": "JUAN",
  "middleName": "M",
  "birthday": "1990-01-01",
  "sex": "Male",
  "address": "123 MAIN STREET, QUEZON CITY"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `crn` | string | Common Reference Number | 123456789012 |
| `surname` | string | Last name | DELA CRUZ |
| `givenName` | string | First name | JUAN |
| `middleName` | string | Middle name | M |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `sex` | string | Gender | Male |
| `address` | string | Complete address | 123 MAIN STREET, QUEZON CITY |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@ph_umid.jpg" \
  -F "documentType=ph_umid"
```

### JavaScript (Browser)

```javascript
async function processPHUMID(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ph_umid');

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
    console.error('Error processing Philippines UMID:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('ph-umid-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPHUMID(file, 'YOUR_API_KEY');
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

def extract_ph_umid_data(image_path, api_key):
    """Extract data from Philippines UMID image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ph_umid'}

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
result = extract_ph_umid_data('ph_umid.jpg', 'YOUR_API_KEY')
if result:
    print("CRN:", result['crn'])
    print("Name:", result['givenName'], result['middleName'], result['surname'])
    print("Full response:", result)
else:
    print("Failed to extract Philippines UMID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPHUMID(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ph_umid');

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
processPHUMID('./ph_umid.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Philippines Documents](../../../supported-documents.md#asia) - Other Philippine documents
