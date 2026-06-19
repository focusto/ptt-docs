---
title: "Hong Kong ID Card"
description: "Complete API documentation for Hong Kong ID Card OCR with examples and field reference"
category: "reference"
region: "asia"
country: "china"
documentType: "hk_id_card"
language: "en"
order: 2
showInSidebar: true
---

# Hong Kong ID Card

Extract data from Hong Kong Smart ID Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `hk_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "englishName": "CHAN, TAI MAN",
  "chineseName": "陳大文",
  "chineseCommercialCode": "7111 1111",
  "idNumber": "W123456(7)",
  "dateOfBirth": "1980-01-01",
  "gender": "M",
  "issueDate": "2020-06-10",
  "firstRegistrationDate": "2003-01-01",
  "symbols": "***AZ"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `englishName` | `string` | The name in English, typically SURNAME, GIVEN NAMES. | CHAN, TAI MAN |
| `chineseName` | `string` | The name in Chinese characters. | 陳大文 |
| `chineseCommercialCode` | `string` | The Chinese Commercial Code for the name. | 7111 1111 |
| `idNumber` | `string` | The Hong Kong Identity Card number. | W123456(7) |
| `dateOfBirth` | `string` | The date of birth in DD-MM-YYYY or YYYY-MM-DD format. | 1980-01-01 |
| `gender` | `string` | The gender of the holder (M/F). | M |
| `issueDate` | `string` | The date the card was issued in DD-MM-YYYY format. | 2020-06-10 |
| `firstRegistrationDate` | `string` | The date of first registration. | 2003-01-01 |
| `symbols` | `string` | Symbols indicating eligibility for right of abode and other statuses. | ***AZ |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@hk_id.jpg" \
  -F "documentType=hk_id_card"
```

### Python

```python
import requests
import os

def extract_hk_id_data(image_path, api_key):
    """Extract data from Hong Kong ID Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'hk_id_card'}
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

