---
title: "Netherlands National ID Card"
description: "Complete API documentation for Netherlands National ID Card OCR with examples and field reference"
category: "reference"
region: "europe"
country: "netherlands"
documentType: "nl_id_card"
language: "en"
order: 1
showInSidebar: true
---

# Netherlands National ID Card

Extract data from Netherlands National ID Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | ID card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `nl_id_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "DE JONG",
  "firstName": "JAN",
  "documentNumber": "IDNLD12345",
  "personalNumber": "123456789",
  "dateOfBirth": "1985-05-10",
  "placeOfBirth": "AMSTERDAM",
  "expiryDate": "2031-01-01",
  "issueDate": "2021-01-01",
  "gender": "M",
  "height": "180",
  "nationality": "NEDERLANDSE",
  "issuingAuthority": "BURG. VAN AMSTERDAM",
  "qrCodeData": "...",
  "mrz": "I<NLD123456789<<<<<<<<<<<<<<<\n8505100M3101012NLD<<<<<<<<<<<<<<<4\nDE<JONG<<JAN"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `lastName` | `string` | The last name of the card holder. | DE JONG |
| `firstName` | `string` | The first name of the card holder. | JAN |
| `documentNumber` | `string` | The unique document number. | IDNLD12345 |
| `personalNumber` | `string` | The personal number (BSN). | 123456789 |
| `dateOfBirth` | `string` | The date of birth in YYYY-MM-DD format. | 1985-05-10 |
| `placeOfBirth` | `string` | The place of birth. | AMSTERDAM |
| `expiryDate` | `string` | The date the card expires in YYYY-MM-DD format. | 2031-01-01 |
| `issueDate` | `string` | The date the card was issued in YYYY-MM-DD format. | 2021-01-01 |
| `gender` | `string` | The gender of the holder (M/V). | M |
| `height` | `string` | The height of the holder in centimeters. | 180 |
| `nationality` | `string` | The nationality of the holder. | NEDERLANDSE |
| `issuingAuthority` | `string` | The authority that issued the card. | BURG. VAN AMSTERDAM |
| `qrCodeData` | `string` | Data from the QR code, if present. | ... |
| `mrz` | `string` | The Machine Readable Zone from the card. Preserve line breaks as `\n` exactly as printed. | I<NLD123456789...`\n`8505100M...`\n`DE<JONG<<JAN |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@nl_id.jpg" \
  -F "documentType=nl_id_card"
```

### Python

```python
import requests
import os

def extract_nl_id_data(image_path, api_key):
    """Extract data from Netherlands National ID Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'nl_id_card'}
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
