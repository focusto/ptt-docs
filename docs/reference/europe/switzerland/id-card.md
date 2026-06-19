---
title: "Switzerland National ID Card"
description: "Complete API documentation for Switzerland National ID Card OCR with examples and field reference"
category: "reference"
region: "europe"
country: "switzerland"
documentType: "ch_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Switzerland National ID Card

Extract data from Switzerland National ID Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `ch_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "MUSTER",
  "firstName": "ERIKA",
  "documentNumber": "C1A2B3D4E",
  "dateOfBirth": "1980-01-01",
  "nationality": "SCHWEIZ/SUISSE/SVIZZERA",
  "expiryDate": "2030-12-31",
  "issueDate": "2020-01-01",
  "gender": "F",
  "height": "165",
  "placeOfBirth": "ZÜRICH",
  "issuingAuthority": "KANTON ZÜRICH",
  "mrz": "IDCHEMUSTER<<ERIKA<<<<<<<<<<<<<<<<<<<<<<\nC1A2B3D4E<8001012F3012315CHE<<<<<<<<<<<<<<<0"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `lastName` | `string` | The last name of the card holder. | MUSTER |
| `firstName` | `string` | The first name of the card holder. | ERIKA |
| `documentNumber` | `string` | The unique document number. | C1A2B3D4E |
| `dateOfBirth` | `string` | The date of birth in YYYY-MM-DD format. | 1980-01-01 |
| `nationality` | `string` | The nationality of the holder. | SCHWEIZ/SUISSE/SVIZZERA |
| `expiryDate` | `string` | The date the card expires in YYYY-MM-DD format. | 2030-12-31 |
| `issueDate` | `string` | The date the card was issued in YYYY-MM-DD format. | 2020-01-01 |
| `gender` | `string` | The gender of the holder (M/F). | F |
| `height` | `string` | The height of the holder in centimeters. | 165 |
| `placeOfBirth` | `string` | The place of birth. | ZÜRICH |
| `issuingAuthority` | `string` | The authority that issued the card. | KANTON ZÜRICH |
| `mrz` | `string` | The Machine Readable Zone from the card. Preserve line breaks as `\n` exactly as printed. | IDCHEMUSTER<<ERIKA...`\n`C1A2B3D4E... |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@ch_id.jpg" \
  -F "documentType=ch_id_card"
```

### Python

```python
import requests
import os

def extract_ch_id_data(image_path, api_key):
    """Extract data from Switzerland National ID Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'ch_id_card'}
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
