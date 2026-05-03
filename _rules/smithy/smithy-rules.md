---
categories:
- smithy
description: Spectral linting rules defining API design standards and conventions for Smithy.
layout: rules
name: Smithy API Rules
provider_name: Smithy
provider_slug: smithy
rule_count: 5
rules:
- description: All operations must have an operationId when represented as OpenAPI
  given: $.paths[*][*]
  name: smithy-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: smithy-operation-tags
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smithy-summary-title-case
  severity: warn
- description: API paths must not have trailing slashes
  given: $.paths
  name: smithy-no-trailing-slashes
  severity: warn
- description: Smithy API paths should include version prefix for HTTP bindings
  given: $.paths
  name: smithy-versioned-paths
  severity: info
rules_file: rules/smithy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smithy/refs/heads/main/rules/smithy-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 3
slug: smithy-rules
source_filename: smithy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# Smithy IDL Spectral-Style Ruleset\n# Note: Smithy uses its own validation model (validators and linters) built into the Smithy CLI.\n# These rules document Smithy's own quality conventions for API models.\nextends: spectral:oas\nrules:\n  smithy-operation-ids:\n    description: All operations must have an operationId when represented as OpenAPI\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  smithy-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smithy-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  smithy-no-trailing-slashes:\n    description: API paths must not have trailing slashes\n\
  \    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  smithy-versioned-paths:\n    description: Smithy API paths should include version prefix for HTTP bindings\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smithy/refs/heads/main/rules/smithy-rules.yml
tags:
- Code Generation
- IDL
- SDKs
- API Design
- Interface Definition Language
- Toolchain
- Spectral
- Linting
- API Governance
---
