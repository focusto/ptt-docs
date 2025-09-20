---
title: "Thailand ID Card"
description: "Complete API documentation for Thailand ID Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "thailand"
documentType: "th_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Thailand ID Card

Extract data from Thai ID Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `th_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "cardTypeTh": "บัตรประจำตัวประชาชน",
  "cardTypeEn": "Identification Card",
  "idNumber": "1234567890123",
  "serialNumber": "TH123456789",
  "nameTh": "สมชาย ใจดี",
  "nameEn": "SOMCHAI JAIDEE",
  "lastNameEn": "JAIDEE",
  "birthTh": "๑ มกราคม ๒๕๓๓",
  "birthEn": "1990-01-01",
  "issueDateEN": "2020-01-01",
  "issueDateTH": "๑ มกราคม ๒๕๖๓",
  "expiryDateEN": "2030-01-01",
  "expiryDateTH": "๑ มกราคม ๒๕๗๓",
  "religion": "พุทธ",
  "address": "123/456 หมู่ 1 ถ.สุขุมวิท เขตคลองเตย กรุงเทพฯ 10110"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `cardTypeTh` | string | Card type in Thai | บัตรประจำตัวประชาชน |
| `cardTypeEn` | string | Card type in English | Identification Card |
| `idNumber` | string | 13-digit ID number | 1234567890123 |
| `serialNumber` | string | Card serial number | TH123456789 |
| `nameTh` | string | Full name in Thai | สมชาย ใจดี |
| `nameEn` | string | Full name in English | SOMCHAI JAIDEE |
| `lastNameEn` | string | Last name in English | JAIDEE |
| `birthTh` | string | Birth date in Thai | ๑ มกราคม ๒๕๓๓ |
| `birthEn` | string | Birth date in English (YYYY-MM-DD) | 1990-01-01 |
| `issueDateEN` | string | Issue date in English (YYYY-MM-DD) | 2020-01-01 |
| `issueDateTH` | string | Issue date in Thai | ๑ มกราคม ๒๕๖๓ |
| `expiryDateEN` | string | Expiry date in English (YYYY-MM-DD) | 2030-01-01 |
| `expiryDateTH` | string | Expiry date in Thai | ๑ มกราคม ๒๕๗๓ |
| `religion` | string | Religion | พุทธ |
| `address` | string | Full address in Thai | 123/456 หมู่ 1 ถ.สุขุมวิท เขตคลองเตย กรุงเทพฯ 10110 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@thai_id.jpg" \
  -F "documentType=th_id_card"
```

### JavaScript (Browser)

```javascript
async function processThaiIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'th_id_card');

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
    console.error('Error processing Thai ID card:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('thai-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processThaiIDCard(file, 'YOUR_API_KEY');
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

def extract_thai_id_data(image_path, api_key):
    """Extract data from Thai ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'th_id_card'}

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
result = extract_thai_id_data('thai_id.jpg', 'YOUR_API_KEY')
if result:
    print("ID Number:", result['idNumber'])
    print("Name (English):", result['nameEn'])
    print("Full response:", result)
else:
    print("Failed to extract Thai ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processThaiIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'th_id_card');

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

processThaiIDCard('./thai_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Rate Limits](../../../limits.md) - Usage limits and quotas
- [All Thailand Documents](../../../supported-documents.md#asia) - Other Thai documents
