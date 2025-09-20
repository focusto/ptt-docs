---
title: "Philippines TinID"
description: "Complete API documentation for Philippines TinID (Tax Identification Number ID) OCR with examples and field reference"
category: "reference"
region: "asia"
country: "philippines"
documentType: "ph_tinid"
language: "en"
order: 3
showInSidebar: true
---

# Philippines TinID

Extract data from Philippines TinID (Tax Identification Number ID) with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | TinID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ph_tinid` |


## Response Format

### Success Response (200 OK)

```json
{
  "fullName": "JUAN M. DELA CRUZ",
  "licenseNumber": "123-456-789-000",
  "birthday": "1990-01-01",
  "issueDate": "2020-01-01",
  "address": "123 MAIN STREET, QUEZON CITY"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `fullName` | string | Full name | JUAN M. DELA CRUZ |
| `licenseNumber` | string | TIN number | 123-456-789-000 |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `issueDate` | string | Issue date (YYYY-MM-DD) | 2020-01-01 |
| `address` | string | Registered address | 123 MAIN STREET, QUEZON CITY |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@ph_tinid.jpg" \
  -F "documentType=ph_tinid"
```

### JavaScript (Browser)

```javascript
async function processPHTinID(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ph_tinid');

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
    console.error('Error processing Philippines TinID:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('ph-tinid-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processPHTinID(file, 'YOUR_API_KEY');
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

def extract_ph_tinid_data(image_path, api_key):
    """Extract data from Philippines TinID image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ph_tinid'}

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
result = extract_ph_tinid_data('ph_tinid.jpg', 'YOUR_API_KEY')
if result:
    print("TIN Number:", result['licenseNumber'])
    print("Name:", result['fullName'])
    print("Full response:", result)
else:
    print("Failed to extract Philippines TinID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processPHTinID(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ph_tinid');

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
processPHTinID('./ph_tinid.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Philippines Documents](../../../supported-documents.md#asia) - Other Philippine documents
