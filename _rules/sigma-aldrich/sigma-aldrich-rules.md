---
api_specs:
- filename: sigma-aldrich-product-openapi.yml
  format: yaml
  label: Sigma-Aldrich Product Search API
  slug: sigma-aldrich-product-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sigma-aldrich/refs/heads/main/openapi/sigma-aldrich-product-openapi.yml
categories:
- sigma
description: Spectral linting rules defining API design standards and conventions for Sigma-Aldrich.
layout: rules
name: Sigma-Aldrich API Rules
provider_name: Sigma-Aldrich
provider_slug: sigma-aldrich
rule_count: 8
rules:
- description: Sigma-Aldrich API must use API key authentication via x-api-key header
  given: $.components.securitySchemes[?(@.type == 'apiKey')]
  name: sigma-aldrich-api-key-auth
  severity: error
- description: Product search endpoints must require a search query parameter
  given: $.paths[?(@property =~ /search/)].get.parameters[?(@.in == 'query')]
  name: sigma-aldrich-search-requires-query
  severity: warn
- description: CAS number path parameters should validate the CAS format pattern
  given: $.components.parameters[?(@.name == 'casNumber')]
  name: sigma-aldrich-cas-number-format
  severity: warn
- description: Structure search request must include structure and searchType fields
  given: $.components.schemas.StructureSearchRequest
  name: sigma-aldrich-structure-search-required-fields
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: sigma-aldrich-operation-summary-required
  severity: error
- description: All operations must define an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: sigma-aldrich-operation-id-required
  severity: error
- description: Stock level field should use enumerated values
  given: $.components.schemas[*].properties.stockLevel
  name: sigma-aldrich-stock-level-enum
  severity: warn
- description: Search result schemas should include total, page, and pageSize
  given: $.components.schemas.ProductSearchResults.properties
  name: sigma-aldrich-search-results-pagination
  severity: warn
rules_file: rules/sigma-aldrich-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sigma-aldrich/refs/heads/main/rules/sigma-aldrich-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: sigma-aldrich-rules
source_filename: sigma-aldrich-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sigma-Aldrich uses API key authentication\n  sigma-aldrich-api-key-auth:\n    description: Sigma-Aldrich API must use API key authentication via x-api-key header\n    message: API security must use apiKey type with x-api-key header\n    severity: error\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - x-api-key\n\n  # Product search must require a query parameter\n  sigma-aldrich-search-requires-query:\n    description: Product search endpoints must require a search query parameter\n    message: Search endpoint should require a 'q' query parameter\n    severity: warn\n    given: \"$.paths[?(@property =~ /search/)].get.parameters[?(@.in == 'query')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^(q|query|keyword|cas|smiles|inchi)$\"\n\n  # CAS number parameters\
  \ should validate format\n  sigma-aldrich-cas-number-format:\n    description: CAS number path parameters should validate the CAS format pattern\n    message: CAS number parameter should use format validation pattern\n    severity: warn\n    given: \"$.components.parameters[?(@.name == 'casNumber')]\"\n    then:\n      field: schema.pattern\n      function: truthy\n\n  # Chemical structure searches should require structure and searchType\n  sigma-aldrich-structure-search-required-fields:\n    description: Structure search request must include structure and searchType fields\n    message: Structure search schema must require 'structure' and 'searchType' fields\n    severity: error\n    given: \"$.components.schemas.StructureSearchRequest\"\n    then:\n      field: required\n      function: truthy\n\n  # All operations must have a summary\n  sigma-aldrich-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity:\
  \ error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Operations must have operationId\n  sigma-aldrich-operation-id-required:\n    description: All operations must define an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Stock level should use enumeration\n  sigma-aldrich-stock-level-enum:\n    description: Stock level field should use enumerated values\n    message: stockLevel should define an enum\n    severity: warn\n    given: \"$.components.schemas[*].properties.stockLevel\"\n    then:\n      field: enum\n      function: truthy\n\n  # Search results should include pagination metadata\n  sigma-aldrich-search-results-pagination:\n    description: Search result schemas should include total, page, and pageSize\n    message: Search results should define total, page, and pageSize properties\n\
  \    severity: warn\n    given: \"$.components.schemas.ProductSearchResults.properties\"\n    then:\n      field: total\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sigma-aldrich/refs/heads/main/rules/sigma-aldrich-rules.yml
tags:
- Life Science
- Chemistry
- Biochemistry
- Laboratory
- Research
- Chemical Catalog
- Spectral
- Linting
- API Governance
---
