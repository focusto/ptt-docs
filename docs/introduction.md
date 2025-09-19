---
title: "Introduction"
description: "Extract structured data from ID cards, passports, and documents using AI-powered OCR"
category: "guide"
language: "en"
order: 0
showInSidebar: true
---

# Introduction

Extract structured data from ID cards, passports, driver's licenses, and other identity documents using our AI-powered OCR service.

## What is PicToText?

PicToText provides powerful OCR (Optical Character Recognition) capabilities specifically designed for identity documents. Upload an image, get structured JSON data back.

## Key Features

- **📄 Multi-country Support**: ID cards, passports, driver's licenses from 50+ countries
- **🎯 High Accuracy**: AI-powered text extraction with field recognition
- **⚡ Fast Processing**: Results in 2-5 seconds
- **🔒 Secure**: Images encrypted, processed securely, with automatic deletion
- **🌍 Multi-language**: Support for documents in various languages

## Quick Links

<div class="grid grid-cols-1 md:grid-cols-2 gap-4 my-8">
  <a href="./quickstart" class="block p-6 border rounded-lg hover:bg-gray-50">
    <h3 class="text-lg font-semibold mb-2">🚀 Quickstart Guide</h3>
    <p class="text-gray-600">Get your first API call working in 5 minutes</p>
  </a>

  <a href="./supported-documents" class="block p-6 border rounded-lg hover:bg-gray-50">
    <h3 class="text-lg font-semibold mb-2">📚 API Reference</h3>
    <p class="text-gray-600">Complete endpoint documentation by region</p>
  </a>

  <a href="./errors" class="block p-6 border rounded-lg hover:bg-gray-50">
    <h3 class="text-lg font-semibold mb-2">🔧 Error Reference</h3>
    <p class="text-gray-600">Error codes and troubleshooting guide</p>
  </a>

  <a href="./limits" class="block p-6 border rounded-lg hover:bg-gray-50">
    <h3 class="text-lg font-semibold mb-2">📊 Rate Limits</h3>
    <p class="text-gray-600">Usage limits and quota information</p>
  </a>
</div>

## API Overview

**Base URL:** `https://pictotext.io`

**Authentication:** Bearer token in Authorization header

**Main Endpoint:** `POST /api/v1/ocr`

**Response Format:** Direct JSON with extracted fields

```json
// Example response for Chinese ID card
{
  "name": "张三",
  "gender": "男",
  "ethnicity": "汉",
  "dateOfBirth": "1990-01-01",
  "address": "北京市朝阳区",
  "idNumber": "110101199001011234"
}
```

## Regional API Documentation

Browse API documentation by region:

- **🌏 Asia**: [China](./reference/asia/china/id-card), [India](./reference/asia/india/aadhaar-front)
- **🌎 North America**: [USA](./reference/north-america/usa/drivers-license)

For a complete list, see the [Supported Documents](./supported-documents) page.

## Need Help?

- 📧 **Email:** support@pictotext.io
- 💬 **Discord:** [Join our community](https://discord.gg/pictotext)
- 📖 **FAQ:** [Frequently Asked Questions](/docs/faq)
- 📝 **Blog:** [Latest updates and guides](/blog)