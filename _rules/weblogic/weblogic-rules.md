---
api_specs:
- filename: weblogic-restful-management-services-openapi.yml
  format: yaml
  label: WebLogic RESTful Management Services API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weblogic/refs/heads/main/openapi/weblogic-restful-management-services-openapi.yml
- filename: weblogic-monitoring-diagnostics-openapi.yml
  format: yaml
  label: WebLogic Monitoring and Diagnostics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weblogic/refs/heads/main/openapi/weblogic-monitoring-diagnostics-openapi.yml
- filename: weblogic-deployment-openapi.yml
  format: yaml
  label: WebLogic Deployment API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weblogic/refs/heads/main/openapi/weblogic-deployment-openapi.yml
categories:
- weblogic
description: Spectral linting rules defining API design standards and conventions for Oracle WebLogic Server APIs.
layout: rules
name: Oracle WebLogic Server APIs API Rules
provider_name: Oracle WebLogic Server APIs
provider_slug: weblogic
rule_count: 13
rules:
- description: Operation summaries must start with "Oracle WebLogic Server APIs"
  given: $.paths[*][*].summary
  name: weblogic-summary-prefix
  severity: warn
- description: Operation summary after the prefix must use Title Case
  given: $.paths[*][*].summary
  name: weblogic-summary-title-case
  severity: warn
- description: operationId must use camelCase naming
  given: $.paths[*][*].operationId
  name: weblogic-operation-id-camel-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: weblogic-operation-id-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: weblogic-operation-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: weblogic-operation-tags-required
  severity: warn
- description: Operations must define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: weblogic-response-401-required
  severity: warn
- description: Path parameters must have a description
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: weblogic-path-parameter-description
  severity: warn
- description: Named schemas in components must have a description
  given: $.components.schemas[*]
  name: weblogic-schema-description
  severity: warn
- description: API must define at least one security scheme
  given: $
  name: weblogic-security-defined
  severity: error
- description: Path segments must use kebab-case (lowercase, hyphens)
  given: $.paths[*]~
  name: weblogic-path-kebab-case
  severity: warn
- description: API info must include contact information
  given: $.info
  name: weblogic-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: weblogic-info-license
  severity: warn
rules_file: rules/weblogic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/weblogic/refs/heads/main/rules/weblogic-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 11
slug: weblogic-rules
source_filename: weblogic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # WebLogic summaries must follow: \"Oracle WebLogic Server APIs {Title Case Summary}\"\n  weblogic-summary-prefix:\n    description: Operation summaries must start with \"Oracle WebLogic Server APIs\"\n    message: Summary \"{{value}}\" must begin with \"Oracle WebLogic Server APIs \"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Oracle WebLogic Server APIs \"\n\n  # All operation summaries must use Title Case after the prefix\n  weblogic-summary-title-case:\n    description: Operation summary after the prefix must use Title Case\n    message: Summary \"{{value}}\" must use Title Case for each significant word\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Oracle WebLogic Server APIs [A-Z]\"\n\n  # All operationIds must be camelCase\n  weblogic-operation-id-camel-case:\n\
  \    description: operationId must use camelCase naming\n    message: operationId \"{{value}}\" must use camelCase (e.g., getServer, createCluster)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Operations must have an operationId\n  weblogic-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Operations must have a description\n  weblogic-operation-description-required:\n    description: All operations must have a description\n    message: Operation is missing a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: description\n      function: truthy\n\n  # Operations\
  \ must have at least one tag\n  weblogic-operation-tags-required:\n    description: All operations must have at least one tag\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Responses must define 200/201 success and 401 unauthorized\n  weblogic-response-401-required:\n    description: Operations must define a 401 Unauthorized response\n    message: Operation is missing a 401 Unauthorized response definition\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Path parameters must have descriptions\n  weblogic-path-parameter-description:\n    description: Path parameters must have a description\n    message: Path parameter \"{{value}}\" is missing a description\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n   \
  \   field: description\n      function: truthy\n\n  # Schema components must have descriptions\n  weblogic-schema-description:\n    description: Named schemas in components must have a description\n    message: Schema \"{{path}}\" is missing a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # API must define a security scheme\n  weblogic-security-defined:\n    description: API must define at least one security scheme\n    message: No security schemes defined in components\n    severity: error\n    given: \"$\"\n    then:\n      field: \"components.securitySchemes\"\n      function: truthy\n\n  # Paths must use kebab-case\n  weblogic-path-kebab-case:\n    description: Path segments must use kebab-case (lowercase, hyphens)\n    message: Path \"{{value}}\" contains uppercase letters or non-hyphen separators\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^(/[a-z0-9{}-]+)*$\"\n\n  # Info must have contact\n  weblogic-info-contact:\n    description: API info must include contact information\n    message: API is missing contact information in info section\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # Info must have license\n  weblogic-info-license:\n    description: API info must include license information\n    message: API is missing license information in info section\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/weblogic/refs/heads/main/rules/weblogic-rules.yml
tags:
- Application Server
- Enterprise
- Java EE
- Middleware
- Oracle
- WebLogic
- Spectral
- Linting
- API Governance
---
