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

- [🚀 Quickstart Guide](./quickstart.md)
- [📚 API Reference](./supported-documents.md)
- [🔧 Error Reference](./errors.md)
- [📊 Usage and Limits](./limits.md)

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



## Need Help?

- 📧 **Email:** support@pictotext.io
- 📖 **FAQ:** [Frequently Asked Questions](https://pictotext.io/#faq)
- 📝 **Blog:** [Latest updates and guides](https://pictotext.io/blog)
