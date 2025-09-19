---
title: "India PAN Card"
description: "Complete API documentation for India PAN Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "india"
documentType: "in_pan"
language: "en"
order: 3
showInSidebar: true
---

# India PAN Card

Extract data from Indian PAN (Permanent Account Number) card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | PAN card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `in_pan` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardNumber": "ABCDE1234F",
  "dateOfBirth": "1990-01-01",
  "fatherName": "RAMESH KUMAR",
  "name": "RAJESH KUMAR"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardNumber` | string | 10-character PAN number | ABCDE1234F |
| `dateOfBirth` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `fatherName` | string | Father's name | RAMESH KUMAR |
| `name` | string | Cardholder's full name | RAJESH KUMAR |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@pan_card.jpg" \\
  -F "documentType=in_pan"
```

### JavaScript (Browser)

```javascript
async function processPANCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'in_pan');

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
    console.error('Error processing PAN card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('pan-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPANCard(file, 'YOUR_API_KEY');
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

def extract_pan_data(image_path, api_key):
    """Extract data from PAN card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'in_pan'}

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
result = extract_pan_data('pan_card.jpg', 'YOUR_API_KEY')
if result:
    print("PAN Number:", result['cardNumber'])
    print("Name:", result['name'])
    print("Full response:", result)
else:
    print("Failed to extract PAN data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPANCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'in_pan');

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
processPANCard('./pan_card.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All India Documents](../../../supported-documents#asia) - Other Indian documents