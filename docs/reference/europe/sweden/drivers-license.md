---
title: "Sweden Driver's Licence"
description: "Complete API documentation for Sweden Driver's Licence OCR with examples and field reference"
category: "reference"
region: "europe"
country: "sweden"
documentType: "se_drivers_license"
language: "en"
order: 2
showInSidebar: true
---

# Sweden Driver's Licence

Extract data from Sweden Driver's Licences with our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Licence image file (JPG, PNG, WebP, HEIC and HEIF, max 10MB) |
| `documentType` | String | ✅ | Must be `se_drivers_license` |


## Response Format

### Success Response (200 OK)

```json
{
  "lastName": "ANDERSSON",
  "firstName": "ANNA",
  "licenseNumber": "990101-1234",
  "personalIdNumber": "19900101-1234",
  "dateOfBirth": "1990-01-01",
  "expiryDate": "2030-01-01",
  "issueDate": "2020-01-01",
  "vehicleCategories": "B"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `lastName` | `string` | The last name of the licence holder. | ANDERSSON |
| `firstName` | `string` | The first name of the licence holder. | ANNA |
| `licenseNumber` | `string` | The unique licence number. | 990101-1234 |
| `personalIdNumber` | `string` | The Swedish personal identity number (personnummer). | 19900101-1234 |
| `dateOfBirth` | `string` | The date of birth in YYYY-MM-DD format. | 1990-01-01 |
| `expiryDate` | `string` | The date the licence expires in YYYY-MM-DD format. | 2030-01-01 |
| `issueDate` | `string` | The date the licence was issued in YYYY-MM-DD format. | 2020-01-01 |
| `vehicleCategories` | `string` | The vehicle categories the holder is licensed for. | B |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \
  -H "Authorization: Bearer sk_live_123456789abcdef" \
  -F "image=@se_license.jpg" \
  -F "documentType=se_drivers_license"
```

### Python

```python
import requests
import os

def extract_se_license_data(image_path, api_key):
    """Extract data from Sweden Driver's Licence image"""
    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}
    try:
        with open(image_path, 'rb') as f:
            files = {'image': (os.path.basename(image_path), f, 'image/jpeg')}
            data = {'documentType': 'se_drivers_license'}
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

