---
title: "Philippines Voter's ID"
description: "Complete API documentation for Philippines Voter's ID OCR with examples and field reference"
category: "reference"
region: "asia"
country: "philippines"
documentType: "ph_voters_id"
language: "en"
order: 1
showInSidebar: true
---

# Philippines Voter's ID

Extract data from Philippines Voter's Identification Card with high accuracy using our advanced OCR technology.

## Request Parameters

### Required Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Voter's ID image file (JPG, PNG, WebP, max 10MB) |
| `documentType` | String | ✅ | Must be `ph_voters_id` |


## Response Format

### Success Response (200 OK)

```json
{
  "vin": "V1234567890",
  "firstName": "JUAN",
  "lastName": "DELA CRUZ",
  "birthday": "1990-01-01",
  "civilStatus": "Single",
  "citizenship": "Filipino",
  "address": "123 MAIN STREET, QUEZON CITY",
  "precinctNo": "1234A"
}
```

### Response Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `vin` | string | Voter's Identification Number | V1234567890 |
| `firstName` | string | First name | JUAN |
| `lastName` | string | Last name | DELA CRUZ |
| `birthday` | string | Date of birth (YYYY-MM-DD) | 1990-01-01 |
| `civilStatus` | string | Civil status | Single |
| `citizenship` | string | Citizenship | Filipino |
| `address` | string | Registered address | 123 MAIN STREET, QUEZON CITY |
| `precinctNo` | string | Precinct number | 1234A |

## Code Examples

### cURL

```bash
curl -X POST "https://pictotext.io/api/v1/ocr" \\
  -H "Authorization: Bearer sk_live_123456789abcdef" \\
  -F "image=@voters_id.jpg" \\
  -F "documentType=ph_voters_id"
```

### JavaScript (Browser)

```javascript
async function processVotersID(imageFile, apiKey) {
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('documentType', 'ph_voters_id');

  try {
    const response = await fetch('https://pictotext.io/api/v1/ocr', {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${apiKey}`
      },
      body: formData
    });

    if (!response.ok) {
      const error = await response.json();
      throw new Error(error.error.message);
    }

    return await response.json();
  } catch (error) {
    console.error('Error processing voter\'s ID:', error);
    throw error;
  }
}

// Usage example
const fileInput = document.getElementById('voters-id-file');
fileInput.addEventListener('change', async (event) => {
  const file = event.target.files[0];
  if (file) {
    try {
      const result = await processVotersID(file, 'YOUR_API_KEY');
      console.log('Extracted data:', result);
    } catch (error) {
      alert('Processing failed: ' + error.message);
    }
  }
});
```

### Python

```python
import requests
import os

def extract_voters_id_data(image_path, api_key):
    """Extract data from voter's ID image"""

    url = 'https://pictotext.io/api/v1/ocr'
    headers = {'Authorization': f'Bearer {api_key}'}

    try:
        with open(image_path, 'rb') as f:
            files = {
                'image': (os.path.basename(image_path), f, 'image/jpeg')
            }
            data = {'documentType': 'ph_voters_id'}

            response = requests.post(url, headers=headers, files=files, data=data, timeout=30)
            response.raise_for_status()

            return response.json()

    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        if hasattr(e, 'response') and e.response is not None:
            print(f"Status code: {e.response.status_code}")
            print(f"Error response: {e.response.text}")
        return None

# Usage
result = extract_voters_id_data('voters_id.jpg', 'YOUR_API_KEY')
if result:
    print("VIN:", result['vin'])
    print("Name:", result['firstName'], result['lastName'])
    print("Full response:", result)
else:
    print("Failed to extract voter's ID data")
```

### Node.js

```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function processVotersID(imagePath, apiKey) {
  const formData = new FormData();
  formData.append('image', fs.createReadStream(imagePath));
  formData.append('documentType', 'ph_voters_id');

  try {
    const response = await axios.post('https://pictotext.io/api/v1/ocr', formData, {
      headers: {
        ...formData.getHeaders(),
        'Authorization': `Bearer ${apiKey}`
      }
    });

    return response.data;
  } catch (error) {
    if (error.response) {
      console.error('API Error:', error.response.data);
    }
    throw error;
  }
}

// Usage
processVotersID('./voters_id.jpg', 'YOUR_API_KEY')
  .then(result => console.log(result))
  .catch(error => console.error('Error:', error.message));
```

## Related Documentation

- [Authentication Guide](../../../authentication) - API key management
- [Error Reference](../../../errors) - Complete error codes
- [Rate Limits](../../../limits) - Usage limits and quotas
- [All Philippines Documents](../../../supported-documents#asia) - Other Philippine documents