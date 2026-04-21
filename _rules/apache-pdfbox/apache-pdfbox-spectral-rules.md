---
categories:
- info
- operation
- paths
- response
description: Spectral linting rules defining API design standards and conventions for Apache PDFBox.
layout: rules
name: Apache PDFBox API Rules
provider_name: Apache PDFBox
provider_slug: apache-pdfbox
rule_count: 6
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: Summaries should start with Apache PDFBox
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: Document paths should follow /documents pattern
  given: $.paths[*]~
  name: paths-document-resource
  severity: info
- description: ''
  given: $.paths[*][get,post,put].responses
  name: response-success-required
  severity: error
rules_file: rules/apache-pdfbox-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-pdfbox/refs/heads/main/rules/apache-pdfbox-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 0
slug: apache-pdfbox-spectral-rules
tags:
- Document Processing
- Java
- PDF
- Text Extraction
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
