---
api_specs:
- filename: synopsys-polaris-openapi.yml
  format: yaml
  label: Synopsys Polaris API
  slug: polaris
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synopsys/refs/heads/main/openapi/synopsys-polaris-openapi.yml
- filename: synopsys-cloud-openlink-openapi.yml
  format: yaml
  label: Synopsys Cloud OpenLink API
  slug: cloud-openlink
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synopsys/refs/heads/main/openapi/synopsys-cloud-openlink-openapi.yml
categories:
- async
- issue
- operation
- paths
- polaris
- report
- scan
description: Spectral linting rules defining API design standards and conventions for Synopsys.
layout: rules
name: Synopsys API Rules
provider_name: Synopsys
provider_slug: synopsys
rule_count: 12
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All operations must be tagged.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: Scan completion responses should include issue count information.
  given: $.components.schemas.Scan.properties
  name: scan-response-issue-count
  severity: info
- description: Issue schema must include a severity field.
  given: $.components.schemas.Issue.properties
  name: issue-severity-required
  severity: error
- description: Issue schema should include a CWE reference field.
  given: $.components.schemas.Issue.properties
  name: issue-cwe-field
  severity: warn
- description: Polaris API responses may use versioned vendor content types.
  given: $.paths[*][*].responses[*].content
  name: polaris-content-type
  severity: info
- description: Operations that may be asynchronous must include a 202 response.
  given: $.paths[*].post.responses
  name: async-operation-202
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Report request schema must include a format field.
  given: $.components.schemas.ReportRequest.properties
  name: report-format-required
  severity: warn
rules_file: rules/synopsys-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/synopsys/refs/heads/main/rules/synopsys-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 7
slug: synopsys-rules
source_filename: synopsys-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Require operationId\n  operation-operationId:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require summary\n  operation-summary:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Enforce Title Case on summaries\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ()/-]*$\"\n\n  # Require tags\n  operation-tags:\n    description: All operations must be tagged.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n\
  \    then:\n      field: tags\n      function: truthy\n\n  # Require description\n  operation-description:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Security scan responses should include issue counts\n  scan-response-issue-count:\n    description: Scan completion responses should include issue count information.\n    severity: info\n    given: \"$.components.schemas.Scan.properties\"\n    then:\n      field: issueCount\n      function: truthy\n\n  # Issues must have severity field\n  issue-severity-required:\n    description: Issue schema must include a severity field.\n    severity: error\n    given: \"$.components.schemas.Issue.properties\"\n    then:\n      field: severity\n      function: truthy\n\n  # Issues must have CWE field\n  issue-cwe-field:\n    description: Issue schema should include a CWE reference field.\n    severity:\
  \ warn\n    given: \"$.components.schemas.Issue.properties\"\n    then:\n      field: cwe\n      function: truthy\n\n  # Polaris content-type pattern\n  polaris-content-type:\n    description: Polaris API responses may use versioned vendor content types.\n    severity: info\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: truthy\n\n  # Require 202 for async operations\n  async-operation-202:\n    description: Operations that may be asynchronous must include a 202 response.\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: truthy\n\n  # Paths must use kebab-case\n  paths-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  # Report requests must specify format\n  report-format-required:\n    description: Report request schema must include a format field.\n    severity:\
  \ warn\n    given: \"$.components.schemas.ReportRequest.properties\"\n    then:\n      field: format\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/synopsys/refs/heads/main/rules/synopsys-rules.yml
tags:
- Software Security
- Application Security Testing
- Static Analysis
- Software Composition Analysis
- EDA Tools
- Semiconductor Design
- Spectral
- Linting
- API Governance
---
