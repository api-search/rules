---
api_specs:
- filename: tomcat-manager-openapi.yml
  format: yaml
  label: Apache Tomcat Manager API
  slug: tomcat-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tomcat/refs/heads/main/openapi/tomcat-manager-openapi.yml
categories:
- tomcat
description: Spectral linting rules defining API design standards and conventions for Apache Tomcat.
layout: rules
name: Apache Tomcat API Rules
provider_name: Apache Tomcat
provider_slug: tomcat
rule_count: 7
rules:
- description: Tomcat Manager text API returns text/plain responses
  given: $.paths[/text/*][get,put,post,delete].responses.200.content
  name: tomcat-text-plain-responses
  severity: warn
- description: Tomcat Manager requires HTTP Basic authentication
  given: $.components.securitySchemes
  name: tomcat-basic-auth
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: tomcat-operation-id-required
  severity: error
- description: Manager text interface paths should use /text/ prefix
  given: $.paths[*]~
  name: tomcat-text-path-prefix
  severity: info
- description: Destructive operations must have clear descriptions
  given: $.paths[*][get,put,post,delete]
  name: tomcat-destructive-operations
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tomcat-summary-title-case
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: tomcat-tags-required
  severity: warn
rules_file: rules/tomcat-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tomcat/refs/heads/main/rules/tomcat-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: tomcat-rules
source_filename: tomcat-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Tomcat Manager uses text/plain responses\n  tomcat-text-plain-responses:\n    description: Tomcat Manager text API returns text/plain responses\n    message: Text interface operations should return text/plain content type\n    severity: warn\n    given: \"$.paths[/text/*][get,put,post,delete].responses.200.content\"\n    then:\n      function: defined\n\n  # Tomcat uses Basic auth\n  tomcat-basic-auth:\n    description: Tomcat Manager requires HTTP Basic authentication\n    message: Security scheme should be HTTP Basic auth\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  # All operations must have operationId\n  tomcat-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\
  \n  # Manager text paths should start with /text/\n  tomcat-text-path-prefix:\n    description: Manager text interface paths should use /text/ prefix\n    message: Text interface paths should start with /text/\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/text/|/status|/jmxproxy).*$\"\n\n  # Destructive operations should be documented\n  tomcat-destructive-operations:\n    description: Destructive operations must have clear descriptions\n    message: Operations that modify server state must include descriptions\n    severity: error\n    given: \"$.paths[*][get,put,post,delete]\"\n    then:\n      field: description\n      function: defined\n\n  # Summaries must use Title Case\n  tomcat-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"{{value}} summary should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n  \
  \  then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ()-]*$\"\n\n  # Operations must have tags\n  tomcat-tags-required:\n    description: All operations must be tagged\n    message: Operation is missing tags for grouping\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tomcat/refs/heads/main/rules/tomcat-rules.yml
tags:
- Application Server
- Java
- Servlet Container
- Web Server
- Open Source
- Apache
- Spectral
- Linting
- API Governance
---
