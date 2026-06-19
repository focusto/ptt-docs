---
title: "Vietnam Citizen Identity Card"
description: "Complete API documentation for Vietnam Citizen Identity Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "vietnam"
documentType: "vn_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Vietnam Citizen Identity Card

Extract data from Vietnam Citizen Identity Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Citizen identity card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `vn_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "idNumber": "012345678901",
  "name": "NGUYỄN VĂN A",
  "dateOfBirth": "1990-01-01",
  "gender": "Nam",
  "nationality": "Việt Nam",
  "placeOfOrigin": "Hà Nội",
  "placeOfResidence": "Thành phố Hồ Chí Minh",
  "expiryDate": "2030-01-01",
  "mrz": "IDVNM012345678901<<<<<<<<<<<<<<\nNGUYEN<<VAN<A<<<<<<<<<<<<<<<<<<<<"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `idNumber` | string | ID number |
| `name` | string | Full name |
| `dateOfBirth` | string | Date of birth (DD/MM/YYYY) |
| `gender` | string | Gender |
| `nationality` | string | Nationality |
| `placeOfOrigin` | string | Place of origin |
| `placeOfResidence` | string | Place of residence |
| `expiryDate` | string | Expiry date (DD/MM/YYYY) |
| `mrz` | string | Machine Readable Zone. Preserve line breaks as `\n` exactly as printed. |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@vietnam_id_card.jpg" \
  -F "documentType=vn_id_card"
```

### JavaScript (Browser)

```javascript
async function processVietnamIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'vn_id_card');

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
    console.error('Error processing ID card:', error);
    throw error;
  }
}
```

### Python

```python
import requests
import os

def extract_vietnam_id_data(image_path, api_key):
    """Extract data from Vietnam ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'vn_id_card'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()

            return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        if hasattr(e, 'response') and e.response is not None:
            print(f"Status code: {e.response.status_code}")
            print(f"Error response: {e.response.text}")
        return None
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'vn_id_card');

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
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Usage and Limits](../../../limits.md) - Usage limits and quotas
- [All Vietnam Documents](../../../supported-documents.md#asia) - Other Vietnamese documents
