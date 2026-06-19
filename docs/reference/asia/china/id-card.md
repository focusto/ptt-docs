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
codeExamples:
  - title: 'Send a request'
    language: curl
    code: |
      curl -X POST "https://pictotext.io/api/v1/ocr" \
        -H "Authorization: Bearer sk_live_123456789abcdef" \
        -F "image=@cn_id_card.jpg" \
        -F "documentType=cn_id_card"
  - title: 'Send a request (Node.js server)'
    language: javascript
    code: |
      async function processChineseIDCard(imageFile, apiKey) {
        const formData = new FormData()
        formData.append('image', imageFile)
        formData.append('documentType', 'cn_id_card')

        try {
          const response = await fetch('https://pictotext.io/api/v1/ocr', {
            method: 'POST',
            headers: {
              Authorization: `Bearer ${apiKey}`,
            },
            body: formData,
          })

          if (!response.ok) {
            const error = await response.json()
            throw new Error(error.error.message)
          }

          return await response.json()
        } catch (error) {
          console.error('Error processing ID card:', error)
          throw error
        }
      }

      const fileInput = document.getElementById('id-card-file')
      fileInput.addEventListener('change', async (event) => {
        const file = event.target.files[0]
        if (!file) return

        try {
          const result = await processChineseIDCard(file, 'YOUR_API_KEY')
          console.log('Extracted data:', result)
        } catch (error) {
          alert('Processing failed: ' + error.message)
        }
      })
  - title: 'Send a request'
    language: python
    code: |
      import os
      import requests


      def extract_chinese_id_data(image_path: str, api_key: str):
        """Extract data from a Chinese ID card image"""

        url = 'https://pictotext.io/api/v1/ocr'
        headers = {'Authorization': f'Bearer {api_key}'}

        try:
          with open(image_path, 'rb') as fh:
            files = {
              'image': (os.path.basename(image_path), fh, 'image/jpeg'),
            }
            data = {'documentType': 'cn_id_card'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as err:
          print(f'Request failed: {err}')
          if getattr(err, 'response', None) is not None:
            print(f'Status code: {err.response.status_code}')
            print(f'Error response: {err.response.text}')
          return None


      result = extract_chinese_id_data('chinese_id.jpg', 'YOUR_API_KEY')
      if result:
        print('Name:', result['name'])
        print('ID Number:', result['idNumber'])
        print('Full response:', result)
      else:
        print('Failed to extract ID card data')
  - title: 'Send a request'
    language: javascript
    code: |
      import FormData from 'form-data'
      import fs from 'fs'
      import axios from 'axios'


      async function processIDCard(imagePath, apiKey) {
        const formData = new FormData()
        formData.append('image', fs.createReadStream(imagePath))
        formData.append('documentType', 'cn_id_card')

        try {
          const response = await axios.post('https://pictotext.io/api/v1/ocr', formData, {
            headers: {
              ...formData.getHeaders(),
              Authorization: `Bearer ${apiKey}`,
            },
          })

          return response.data
        } catch (error) {
          if (error.response) {
            console.error('API Error:', error.response.data)
          }
          throw error
        }
      }


      processIDCard('./chinese_id.jpg', 'YOUR_API_KEY')
        .then((result) => console.log(result))
        .catch((error) => console.error('Error:', error.message))
---

# Chinese ID Card

Extract data from Chinese resident identity cards with 99%+ accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
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
  "idNumber": "110101199001011234",
  "issuingAuthority": "北京市公安局朝阳分局",
  "validityPeriod": "2010.01.01-2030.01.01"
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
| `issuingAuthority` | string | Issuing authority | 北京市公安局朝阳分局 |
| `validityPeriod` | string | Validity period (YYYY.MM.DD-YYYY.MM.DD) | 2010.01.01-2030.01.01 |

Use the language-specific code samples below to send your first OCR request quickly.

## Related Documentation

- [Authentication Guide](../../../authentication.md) - API key management
- [Error Reference](../../../errors.md) - Complete error codes
- [Usage and Limits](../../../limits.md) - Usage limits and quotas
- [All China Documents](../../../supported-documents.md#asia) - Other Chinese documents
