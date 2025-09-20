---
title: "Quickstart"
description: "Get your first OCR API call working in 5 minutes"
category: "guide"
language: "en"
order: 1
showInSidebar: true
---

# Quickstart

Get your first OCR API call working in under 5 minutes.

## Step 1: Get Your API Key

1. Sign up at [pictotext.io](https://pictotext.io)
2. Go to **Dashboard → API Keys**
3. Click **Generate New Key**
4. Copy your key (starts with `sk-`)

## Step 2: Make Your First Request

### Using cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "image=@document.jpg" \
  -F "documentType=cn_id_card"
```

### Using JavaScript

```javascript
const formData = new FormData();
formData.append('image', fileInput.files[0]);
formData.append('documentType', 'cn_id_card');

const response = await fetch('https://pictotext.io/api/v1/ocr', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY'
  },
  body: formData
});

const data = await response.json();
console.log(data);
```

### Using Python

```python
import requests

url = 'https://pictotext.io/api/v1/ocr'
headers = {'Authorization': 'Bearer YOUR_API_KEY'}

with open('document.jpg', 'rb') as f:
    files = {'image': f}
    data = {'documentType': 'cn_id_card'}

    response = requests.post(url, headers=headers, files=files, data=data)
    result = response.json()
    print(result)
```

## Step 3: Understand the Response

Success response (200):

```json
{
  "name": "张三",
  "gender": "男",
  "ethnicity": "汉",
  "dateOfBirth": "1990-01-01",
  "address": "北京市朝阳区",
  "idNumber": "110101199001011234"
}
```

## That's It!

You've successfully extracted data from an ID card.

## Next Steps

- 📋 [Browse supported documents](./supported-documents.md) - See what else you can extract
- 📖 [Read the API reference](./supported-documents.md) - Complete endpoint documentation

## Common Issues

**401 Unauthorized**: Check your API key format - should be `Bearer YOUR_API_KEY`

**400 Invalid Document Type**: Use a valid type like `cn_id_card`, not `auto`

**Image Upload Failed**: Ensure your image is JPG, PNG, GIF, or WebP format

Need help? Contact support@pictotext.io
