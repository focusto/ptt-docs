---
title: "New Zealand Kiwi Access Card"
description: "Complete API documentation for New Zealand Kiwi Access Card OCR with examples and field reference"
category: "reference"
region: "oceania"
country: "new-zealand"
documentType: "nz_kiwi_access_card"
language: "en"
order: 2
showInSidebar: true
---

# New Zealand Kiwi Access Card

Extract data from New Zealand Kiwi Access Cards with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Card image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `nz_kiwi_access_card` |


## Response Format

### Success Response (200 OK)

```json
{
  "firstName": "JANE",
  "lastName": "DOE",
  "dateOfBirth": "2005-03-20",
  "cardNumber": "12345678"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `firstName` | `string` | The first name of the card holder. | JANE |
| `lastName` | `string` | The last name of the card holder. | DOE |
| `dateOfBirth` | `string` | The date of birth of the card holder in YYYY-MM-DD format. | 2005-03-20 |
| `cardNumber` | `string` | The unique number assigned to the card. | 12345678 |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@kiwi_card.jpg" \
  -F "documentType=nz_kiwi_access_card"
```

### Python

```python
import requests
import os

def extract_kiwi_card_data(image_path, api_key):
    """Extract data from New Zealand Kiwi Access Card image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'nz_kiwi_access_card'}
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
- [All Oceania Documents](../../../supported-documents.md#oceania)

