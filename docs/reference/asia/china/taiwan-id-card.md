---
title: "Taiwan National ID Card"
description: "Complete API documentation for Taiwan National ID Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "china"
documentType: "tw_id_card"
language: "en"
order: 3
showInSidebar: true
---

# Taiwan National ID Card

Extract data from Taiwan National ID Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `tw_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "name": "陳志明",
  "idNumber": "A123456789",
  "dateOfBirth": "1990-01-01",
  "gender": "男",
  "address": "台北市信義區市府路1號",
  "parentsNames": "陳大文、林美玲",
  "issueDate": "2020-01-01",
  "placeOfIssue": "台北市"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `name` | `string` | The full name in Chinese characters. | 陳志明 |
| `idNumber` | `string` | The unique national ID number. | A123456789 |
| `dateOfBirth` | `string` | The date of birth in YYYY-MM-DD format. | 1990-01-01 |
| `gender` | `string` | The gender of the holder (男/女). | 男 |
| `address` | `string` | The residential address. | 台北市信義區市府路1號 |
| `parentsNames` | `string` | The names of the holder's parents. | 陳大文、林美玲 |
| `issueDate` | `string` | The date the card was issued in YYYY-MM-DD format. | 2020-01-01 |
| `placeOfIssue` | `string` | The place where the card was issued. | 台北市 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@tw_id.jpg" \
  -F "documentType=tw_id_card"
```

### Python

```python
import requests
import os

def extract_tw_id_data(image_path, api_key):
    """Extract data from Taiwan National ID Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'tw_id_card'}
            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()
            return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return None
```

## Related Documentation

- [Authentication Guide](../../../authentication.md)
- [Error Reference](../../../errors.md)
- [All Asia Documents](../../../supported-documents.md#asia)

