---
categories:
- spendflo
description: Spectral linting rules defining API design standards and conventions for Spendflo.
layout: rules
name: Spendflo API Rules
provider_name: Spendflo
provider_slug: spendflo
rule_count: 4
rules:
- description: All API operations should have an operationId for Spendflo integration mapping.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: spendflo-operationid-required
  severity: error
- description: All API operations should have a summary describing the procurement action.
  given: $.paths[*][get,post,put,patch,delete]
  name: spendflo-summary-required
  severity: error
- description: Operations should be tagged by procurement domain (Vendors, Contracts, Spend, etc.).
  given: $.paths[*][get,post,put,patch,delete]
  name: spendflo-tags-required
  severity: warn
- description: Operations should document error responses for procurement workflow error handling.
  given: $.paths[*][post,put,patch,delete].responses
  name: spendflo-error-responses-defined
  severity: warn
rules_file: rules/spendflo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spendflo/refs/heads/main/rules/spendflo-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 2
slug: spendflo-rules
source_filename: spendflo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  spendflo-operationid-required:\n    description: All API operations should have an operationId for Spendflo integration mapping.\n    message: \"Operation at {{path}} must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spendflo-summary-required:\n    description: All API operations should have a summary describing the procurement action.\n    message: \"Operation {{path}} is missing a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  spendflo-tags-required:\n    description: Operations should be tagged by procurement domain (Vendors, Contracts, Spend, etc.).\n    message: \"Operation {{path}} should have at least one domain tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n\
  \      field: tags\n      function: truthy\n\n  spendflo-error-responses-defined:\n    description: Operations should document error responses for procurement workflow error handling.\n    message: \"Operation {{path}} should define error response codes (400, 401, 403, 404).\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 2\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spendflo/refs/heads/main/rules/spendflo-rules.yml
tags:
- License Management
- Procurement
- SaaS Management
- Spend Management
- Usage Analytics
- Vendor Management
- Spectral
- Linting
- API Governance
---
