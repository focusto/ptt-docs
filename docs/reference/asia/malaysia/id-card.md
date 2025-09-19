---
title: "Malaysia ID Card"
description: "Complete API documentation for Malaysia ID Card (MyKad) OCR with examples and field reference"
category: "reference"
region: "asia"
country: "malaysia"
documentType: "my_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Malaysia ID Card

Extract data from Malaysian ID Card (MyKad) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `my_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardNumber": "901231086123",
  "dateOfBirth": "1990-12-31",
  "gender": "Male",
  "name": "AHMAD BIN ISMAIL",
  "address": "NO. 123, JALAN TUANKU ABDUL RAHMAN, 50100 KUALA LUMPUR"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardNumber` | string | 12-digit ID card number | 901231086123 |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-12-31 |
| `gender` | string | Gender | Male |
| `name` | string | Full name | AHMAD BIN ISMAIL |
| `address` | string | Full residential address | NO. 123, JALAN TUANKU ABDUL RAHMAN, 50100 KUALA LUMPUR |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@mykad.jpg" \\
  -F "documentType=my_id_card"
```

### JavaScript (Browser)

```javascript
async function processMyKad(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'my_id_card');

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
    console.error('Error processing MyKad:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('mykad-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processMyKad(file, 'YOUR_API_KEY');
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

def extract_mykad_data(image_path, api_key):
    """Extract data from MyKad image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'my_id_card'}

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
result = extract_mykad_data('mykad.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['cardNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract MyKad data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processMyKad(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'my_id_card');

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
processMyKad('./mykad.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Malaysia Documents](../../../supported-documents#asia) - Other Malaysian documents