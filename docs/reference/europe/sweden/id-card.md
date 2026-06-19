---
title: "Sweden National ID Card"
description: "Complete API documentation for Sweden National ID Card OCR with examples and field reference"
category: "reference"
region: "europe"
country: "sweden"
documentType: "se_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Sweden National ID Card

Extract data from Sweden National ID Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `se_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "ANDERSSON",
  "firstName": "ANNA",
  "documentNumber": "123456789",
  "personalIdNumber": "19900101-1234",
  "dateOfBirth": "1990-01-01",
  "expiryDate": "2030-01-01",
  "issueDate": "2020-01-01",
  "height": "170",
  "issuingAuthority": "POLISEN",
  "mrz": "IDSWEANDERSSON<<ANNA<<<<<<<<<<<<<<<<<\n123456789<19001011F3001011SWE<<<<<<<<<<<<<<<4"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `lastName` | `string` | The last name of the card holder. | ANDERSSON |
| `firstName` | `string` | The first name of the card holder. | ANNA |
| `documentNumber` | `string` | The unique document number. | 123456789 |
| `personalIdNumber` | `string` | The Swedish personal identity number (personnummer). | 19900101-1234 |
| `dateOfBirth` | `string` | The date of birth in YYYY-MM-DD format. | 1990-01-01 |
| `expiryDate` | `string` | The date the card expires in YYYY-MM-DD format. | 2030-01-01 |
| `issueDate` | `string` | The date the card was issued in YYYY-MM-DD format. | 2020-01-01 |
| `height` | `string` | The height of the holder in centimeters. | 170 |
| `issuingAuthority` | `string` | The authority that issued the card. | POLISEN |
| `mrz` | `string` | The Machine Readable Zone from the card. Preserve line breaks as `\n` exactly as printed. | IDSWEANDERSSON<<ANNA...`\n`123456789<19001011... |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@se_id.jpg" \
  -F "documentType=se_id_card"
```

### Python

```python
import requests
import os

def extract_se_id_data(image_path, api_key):
    """Extract data from Sweden National ID Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'se_id_card'}
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
- [All Europe Documents](../../../supported-documents.md#europe)
