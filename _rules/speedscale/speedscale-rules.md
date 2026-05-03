---
categories:
- speedscale
description: Spectral linting rules defining API design standards and conventions for Speedscale.
layout: rules
name: Speedscale API Rules
provider_name: Speedscale
provider_slug: speedscale
rule_count: 4
rules:
- description: All operations should have an operationId for Speedscale CLI mapping.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: speedscale-operationid-required
  severity: error
- description: Operations should define response schemas for accurate mock generation.
  given: $.paths[*][get,post,put,patch,delete].responses[200,201,202]
  name: speedscale-response-schema-required
  severity: warn
- description: APIs with authentication should define security schemes for capture.
  given: $.components
  name: speedscale-security-defined
  severity: info
- description: Server URLs should be defined for correct traffic routing in replay.
  given: $
  name: speedscale-servers-defined
  severity: warn
rules_file: rules/speedscale-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/speedscale/refs/heads/main/rules/speedscale-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 2
slug: speedscale-rules
source_filename: speedscale-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  speedscale-operationid-required:\n    description: All operations should have an operationId for Speedscale CLI mapping.\n    message: \"Operation at {{path}} must have an operationId for traffic replay mapping.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  speedscale-response-schema-required:\n    description: Operations should define response schemas for accurate mock generation.\n    message: \"Operation {{path}} should define a response schema for service virtualization.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201,202]\"\n    then:\n      field: content\n      function: truthy\n\n  speedscale-security-defined:\n    description: APIs with authentication should define security schemes for capture.\n    message: \"API spec should define security schemes to enable authenticated traffic\
  \ capture.\"\n    severity: info\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  speedscale-servers-defined:\n    description: Server URLs should be defined for correct traffic routing in replay.\n    message: \"API spec should define at least one server for replay target configuration.\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/speedscale/refs/heads/main/rules/speedscale-rules.yml
tags:
- API Mocking
- API Testing
- Kubernetes
- Load Testing
- Performance Testing
- Regression Testing
- Service Virtualization
- Traffic Replay
- Spectral
- Linting
- API Governance
---
