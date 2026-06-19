---
title: "New Zealand Driver's Licence"
description: "Complete API documentation for New Zealand Driver's Licence OCR with examples and field reference"
category: "reference"
region: "oceania"
country: "new-zealand"
documentType: "nz_drivers_license"
language: "en"
order: 1
showInSidebar: true
---

# New Zealand Driver's Licence

Extract data from New Zealand driver's licences with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Licence image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `nz_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "firstName": "JANE",
  "lastName": "DOE",
  "licenseNumber": "AB123456",
  "versionNumber": "5a",
  "dateOfBirth": "1990-01-15",
  "issueDate": "2020-08-20",
  "expiryDate": "2030-08-19",
  "address": "123 QUEEN STREET\nAUCKLAND 1010",
  "licenseClass": "1, 6",
  "conditions": "CORRECTIVE LENSES"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `firstName` | `string` | The first name of the licence holder. | JANE |
| `lastName` | `string` | The last name of the licence holder. | DOE |
| `licenseNumber` | `string` | The unique number assigned to the driver's licence. | AB123456 |
| `versionNumber` | `string` | The version number of the card. | 5a |
| `dateOfBirth` | `string` | The date of birth of the licence holder in YYYY-MM-DD format. | 1990-01-15 |
| `issueDate` | `string` | The date the licence was issued in YYYY-MM-DD format. | 2020-08-20 |
| `expiryDate` | `string` | The date the licence expires in YYYY-MM-DD format. | 2030-08-19 |
| `address` | `string` | The residential address of the licence holder. | 123 QUEEN STREET\nAUCKLAND 1010 |
| `licenseClass` | `string` | The class or classes of licence. | 1, 6 |
| `conditions` | `string` | Any conditions or endorsements on the licence. | CORRECTIVE LENSES |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@nz_license.jpg" \
  -F "documentType=nz_drivers_license"
```

### Python

```python
import requests
import os

def extract_nz_license_data(image_path, api_key):
    """Extract data from New Zealand Driver's Licence image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'nz_drivers_license'}
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