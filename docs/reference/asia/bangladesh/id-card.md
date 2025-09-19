---
title: "Bangladesh ID Card"
description: "Complete API documentation for Bangladesh ID Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "bangladesh"
documentType: "bd_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Bangladesh ID Card

Extract data from Bangladesh ID Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `bd_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "idNumber": "1234567890123",
  "name": "MD. RAHIM UDDIN",
  "birthday": "1990-01-01"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `idNumber` | string | National ID number | 1234567890123 |
| `name` | string | Full name | MD. RAHIM UDDIN |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@bangladesh_id.jpg" \\
  -F "documentType=bd_id_card"
```

### JavaScript (Browser)

```javascript
async function processBangladeshIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'bd_id_card');

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
    console.error('Error processing Bangladesh ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('bangladesh-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processBangladeshIDCard(file, 'YOUR_API_KEY');
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

def extract_bangladesh_id_data(image_path, api_key):
    """Extract data from Bangladesh ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'bd_id_card'}

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
result = extract_bangladesh_id_data('bangladesh_id.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['idNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract Bangladesh ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processBangladeshIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'bd_id_card');

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
processBangladeshIDCard('./bangladesh_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Bangladesh Documents](../../../supported-documents#asia) - Other Bangladeshi documents