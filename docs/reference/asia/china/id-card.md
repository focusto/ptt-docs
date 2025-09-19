---
title: "Chinese ID Card"
description: "Complete API documentation for Chinese ID Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "china"
documentType: "cn_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Chinese ID Card

Extract data from Chinese resident identity cards with 99%+ accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `cn_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "name": "张三",
  "gender": "男",
  "ethnicity": "汉",
  "dateOfBirth": "1990-01-01",
  "address": "北京市朝阳区xxx街道xxx号",
  "idNumber": "110101199001011234"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `name` | string | Full name in Chinese characters | 张三 |
| `gender` | string | Gender (男/女) | 男 |
| `ethnicity` | string | Ethnic group | 汉 |
| `dateOfBirth` | string | Birth date (YYYY-MM-DD) | 1990-01-01 |
| `address` | string | Full residential address | 北京市朝阳区xxx街道xxx号 |
| `idNumber` | string | 18-digit ID number | 110101199001011234 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@cn_id_card.jpg" \
  -F "documentType=cn_id_card"
```

### JavaScript (Browser)

```javascript
async function processChineseIDCard(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'cn_id_card');

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

// Usage example
const fileInput = document.getElementById('id-card-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processChineseIDCard(file, 'YOUR_API_KEY');
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

def extract_chinese_id_data(image_path, api_key):
    """Extract data from Chinese ID card image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'cn_id_card'}

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
result = extract_chinese_id_data('chinese_id.jpg', 'YOUR_API_KEY')
if result:
    print("Name:", result['name'])
    print("ID Number:", result['idNumber'])
    print("Full response:", result)
else:
    print("Failed to extract ID card data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processIDCard(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'cn_id_card');

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
processIDCard('./chinese_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All China Documents](../../../supported-documents#asia) - Other Chinese documents