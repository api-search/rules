---
api_specs:
- filename: saml-sso-bindings.yml
  format: yaml
  label: SAML 2.0 SSO HTTP Bindings API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/saml/refs/heads/main/openapi/saml-sso-bindings.yml
categories:
- saml
description: Spectral linting rules defining API design standards and conventions for SAML.
layout: rules
name: SAML API Rules
provider_name: SAML
provider_slug: saml
rule_count: 9
rules:
- description: Operation summaries must use Title Case per SAML spec naming conventions
  given: $.paths[*][*].summary
  name: saml-summary-title-case
  severity: warn
- description: SAML endpoints require digital signature verification; security schemes should be documented
  given: $.paths[*][*]
  name: saml-security-schemes-defined
  severity: info
- description: SAML SSO redirect binding GET endpoints must define a SAMLRequest parameter
  given: $.paths['/saml/sso/redirect'].get.parameters[*]
  name: saml-samlrequest-parameter
  severity: warn
- description: RelayState parameter must enforce 80 byte maximum per SAML spec Section 3.4.3
  given: $.paths[*][*].parameters[?(@.name=='RelayState')].schema
  name: saml-relay-state-max-length
  severity: error
- description: SAML XML responses should specify application/xml or text/xml content type
  given: $.paths[*][*].responses[*].content
  name: saml-response-xml-content-type
  severity: warn
- description: All operations must have an operationId per SAML API standards
  given: $.paths[*][*]
  name: saml-operation-id-required
  severity: error
- description: Operations must use defined tags matching SAML specification domains
  given: $.paths[*][*].tags[*]
  name: saml-tags-defined
  severity: warn
- description: All parameters must have descriptions explaining SAML-specific constraints
  given: $.paths[*][*].parameters[*]
  name: saml-parameter-descriptions
  severity: warn
- description: SAML endpoints should define 400 Bad Request for malformed SAML messages
  given: $.paths[*][*].responses
  name: saml-response-400-defined
  severity: info
rules_file: rules/saml-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/saml/refs/heads/main/rules/saml-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: saml-rules
source_filename: saml-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  # SAML 2.0 SSO HTTP Bindings API Conventions\n\n  saml-summary-title-case:\n    description: Operation summaries must use Title Case per SAML spec naming conventions\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  saml-security-schemes-defined:\n    description: SAML endpoints require digital signature verification; security schemes should be documented\n    message: \"Security requirements should be documented for SAML endpoints\"\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  saml-samlrequest-parameter:\n    description: SAML SSO redirect binding GET endpoints must define a SAMLRequest parameter\n    message: \"SAML redirect binding endpoints should define SAMLRequest parameter\"\n    severity: warn\n    given:\
  \ \"$.paths['/saml/sso/redirect'].get.parameters[*]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - SAMLRequest\n          - RelayState\n          - SigAlg\n          - Signature\n\n  saml-relay-state-max-length:\n    description: RelayState parameter must enforce 80 byte maximum per SAML spec Section 3.4.3\n    message: \"RelayState maxLength must be 80\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name=='RelayState')].schema\"\n    then:\n      field: maxLength\n      function: defined\n\n  saml-response-xml-content-type:\n    description: SAML XML responses should specify application/xml or text/xml content type\n    message: \"SAML response should specify XML content type\"\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: truthy\n\n  saml-operation-id-required:\n    description: All operations must have an operationId per SAML API standards\n    message:\
  \ \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: defined\n\n  saml-tags-defined:\n    description: Operations must use defined tags matching SAML specification domains\n    message: \"Tag must be one of: SSO, SLO, Metadata\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - SSO\n          - SLO\n          - Metadata\n\n  saml-parameter-descriptions:\n    description: All parameters must have descriptions explaining SAML-specific constraints\n    message: \"Parameter '{{value}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: defined\n\n  saml-response-400-defined:\n    description: SAML endpoints should define 400 Bad Request for malformed SAML messages\n    message: \"400 Bad Request response should\
  \ be defined for SAML protocol errors\"\n    severity: info\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"400\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/saml/refs/heads/main/rules/saml-rules.yml
tags:
- Authentication
- Authorization
- Federation
- Identity Management
- Open Standard
- Security
- Single Sign-On
- SSO
- XML
- Spectral
- Linting
- API Governance
---
