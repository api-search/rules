---
api_specs:
- filename: unsplash-openapi.yml
  format: yaml
  label: Unsplash API
  slug: unsplash
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unsplash/refs/heads/main/openapi/unsplash-openapi.yml
categories:
- unsplash
description: Spectral linting rules defining API design standards and conventions for Unsplash.
layout: rules
name: Unsplash API Rules
provider_name: Unsplash
provider_slug: unsplash
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: unsplash-title-case-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: unsplash-operation-id
  severity: error
- description: Photo objects must include download_location link for tracking compliance
  given: $.components.schemas.Photo.properties.links.properties
  name: unsplash-download-tracking
  severity: warn
- description: Operations should document Accept-Version header usage
  given: $.paths[*][get]
  name: unsplash-accept-version
  severity: info
- description: List endpoints should include pagination parameters
  given: $.paths[/photos,/collections,/topics,/search/photos,/search/collections,/search/users][get].parameters[*].name
  name: unsplash-pagination-params
  severity: warn
- description: Write operations (PUT, POST, DELETE) must require OAuth authentication
  given: $.paths[*][put,post,delete]
  name: unsplash-write-auth
  severity: error
- description: Resource endpoints should define 404 responses
  given: $.paths[*/{id}*][get]
  name: unsplash-not-found
  severity: warn
- description: Photo-returning endpoints should support content_filter parameter
  given: $.paths[/photos/random,/search/photos,/topics/{id_or_slug}/photos][get]
  name: unsplash-content-filter
  severity: info
rules_file: rules/unsplash-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unsplash/refs/heads/main/rules/unsplash-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: unsplash-rules
source_filename: unsplash-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n\n  # Summaries must be Title Case\n  unsplash-title-case-summary:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations must have operationIds\n  unsplash-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation missing operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Download tracking compliance — download_location must be defined\n  unsplash-download-tracking:\n    description: Photo objects must include download_location link for tracking compliance\n    message: \"Photo links should include download_location for Unsplash API guidelines compliance\"\n    severity: warn\n    given:\
  \ \"$.components.schemas.Photo.properties.links.properties\"\n    then:\n      field: download_location\n      function: truthy\n\n  # Accept-Version header best practice\n  unsplash-accept-version:\n    description: Operations should document Accept-Version header usage\n    message: \"Consider documenting the Accept-Version: v1 header\"\n    severity: info\n    given: \"$.paths[*][get]\"\n    then:\n      field: parameters\n      function: defined\n\n  # Pagination parameters for list endpoints\n  unsplash-pagination-params:\n    description: List endpoints should include pagination parameters\n    message: \"List endpoint should define page and per_page parameters\"\n    severity: warn\n    given: \"$.paths[/photos,/collections,/topics,/search/photos,/search/collections,/search/users][get].parameters[*].name\"\n    then:\n      function: defined\n\n  # OAuth scopes for write operations\n  unsplash-write-auth:\n    description: Write operations (PUT, POST, DELETE) must require OAuth\
  \ authentication\n    message: \"Write operation should require OAuth2 security\"\n    severity: error\n    given: \"$.paths[*][put,post,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # 404 for resource endpoints\n  unsplash-not-found:\n    description: Resource endpoints should define 404 responses\n    message: \"Resource endpoint missing 404 response\"\n    severity: warn\n    given: \"$.paths[*/{id}*][get]\"\n    then:\n      field: \"responses.404\"\n      function: truthy\n\n  # Content filter parameter best practice\n  unsplash-content-filter:\n    description: Photo-returning endpoints should support content_filter parameter\n    message: \"Consider adding content_filter parameter for safe content filtering\"\n    severity: info\n    given: \"$.paths[/photos/random,/search/photos,/topics/{id_or_slug}/photos][get]\"\n    then:\n      field: parameters\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unsplash/refs/heads/main/rules/unsplash-rules.yml
tags:
- Photos
- Images
- Photography
- Stock Photos
- Creative
- Open Source
- Media
- Spectral
- Linting
- API Governance
---
