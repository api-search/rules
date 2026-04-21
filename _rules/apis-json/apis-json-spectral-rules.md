---
categories:
- api
- common
- documentation
- maintainer
- 'no'
- openapi
- property
- root
- specification
description: Spectral linting rules defining API design standards and conventions for APIs.json.
layout: rules
name: APIs.json API Rules
provider_name: APIs.json
provider_slug: apis-json
rule_count: 34
rules:
- description: APIs.json root must have a name field
  given: $
  name: root-name-required
  severity: error
- description: APIs.json root must have a description field
  given: $
  name: root-description-required
  severity: error
- description: APIs.json root must have a url field pointing to the file location
  given: $
  name: root-url-required
  severity: error
- description: APIs.json root url should use HTTPS
  given: $.url
  name: root-url-https
  severity: warn
- description: APIs.json root must have a created date
  given: $
  name: root-created-required
  severity: error
- description: APIs.json root must have a modified date
  given: $
  name: root-modified-required
  severity: error
- description: APIs.json root must have a specificationVersion field
  given: $
  name: root-specification-version-required
  severity: error
- description: APIs.json root should have an aid (unique identifier) field
  given: $
  name: root-aid-recommended
  severity: warn
- description: APIs.json aid should follow the format domain:string
  given: $.aid
  name: root-aid-format
  severity: warn
- description: APIs.json root should have maintainers defined
  given: $
  name: root-maintainers-recommended
  severity: warn
- description: APIs.json root should have tags for discoverability
  given: $
  name: root-tags-recommended
  severity: info
- description: APIs.json root should have an image URL for visual representation
  given: $
  name: root-image-recommended
  severity: info
- description: Maintainer entries must have an FN (full name) field
  given: $.maintainers[*]
  name: maintainer-fn-required
  severity: error
- description: Maintainer FN must not be empty
  given: $.maintainers[*].FN
  name: maintainer-fn-not-empty
  severity: error
- description: Maintainer email should be a valid email format
  given: $.maintainers[*].email
  name: maintainer-email-format
  severity: warn
- description: Each API entry must have an aid (unique identifier)
  given: $.apis[*]
  name: api-aid-required
  severity: error
- description: API aid should follow the format domain:string
  given: $.apis[*].aid
  name: api-aid-format
  severity: warn
- description: Each API entry must have a name
  given: $.apis[*]
  name: api-name-required
  severity: error
- description: Each API entry must have a description
  given: $.apis[*]
  name: api-description-required
  severity: error
- description: API description should be descriptive (at least 20 characters)
  given: $.apis[*].description
  name: api-description-min-length
  severity: warn
- description: Each API entry should have a humanURL
  given: $.apis[*]
  name: api-human-url-required
  severity: warn
- description: API humanURL should use HTTPS
  given: $.apis[*].humanURL
  name: api-human-url-https
  severity: warn
- description: API baseURL should use HTTPS
  given: $.apis[*].baseURL
  name: api-base-url-https
  severity: warn
- description: Each API entry should have tags for discoverability
  given: $.apis[*]
  name: api-tags-recommended
  severity: info
- description: Each API entry should have at least one property
  given: $.apis[*]
  name: api-properties-recommended
  severity: warn
- description: Common properties should include a Website entry
  given: $.common
  name: common-website-recommended
  severity: info
- description: Each property entry must have a type field
  given: $..properties[*]
  name: property-type-required
  severity: error
- description: Each property entry must have either a url or data field
  given: $..properties[*]
  name: property-url-or-data-required
  severity: error
- description: Property URLs should use HTTPS
  given: $..properties[*].url
  name: property-url-https
  severity: warn
- description: Name fields must not be empty strings
  given: $..name
  name: no-empty-names
  severity: error
- description: Description fields must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: specificationVersion should use the latest stable version (0.19)
  given: $.specificationVersion
  name: specification-version-current
  severity: info
- description: APIs should have a Documentation property for human-readable reference
  given: $.apis[*].properties[*].type
  name: documentation-property-recommended
  severity: info
- description: APIs should have an OpenAPI property for machine-readable interface definition
  given: $.apis[*].properties[*].type
  name: openapi-property-recommended
  severity: info
rules_file: rules/apis-json-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apis-json/refs/heads/main/rules/apis-json-spectral-rules.yml
severity_counts:
  error: 15
  hint: 0
  info: 7
  warn: 12
slug: apis-json-spectral-rules
tags:
- API Aggregation
- API Cataloging
- API Commons
- API Discovery
- API Governance
- API Operations
- Machine Readable
- Specification
- Standard
- Spectral
- Linting
- API Governance
---
