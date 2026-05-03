---
api_specs:
- filename: vagrant-cloud-api-openapi.yml
  format: yaml
  label: Vagrant Cloud API
  slug: vagrant-cloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vagrant/refs/heads/main/openapi/vagrant-cloud-api-openapi.yml
- filename: vagrant-hcp-vagrant-box-registry-openapi.yml
  format: yaml
  label: HCP Vagrant Box Registry API
  slug: vagrant-hcp-box-registry
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vagrant/refs/heads/main/openapi/vagrant-hcp-vagrant-box-registry-openapi.yml
categories:
- vagrant
description: Spectral linting rules defining API design standards and conventions for Vagrant.
layout: rules
name: Vagrant API Rules
provider_name: Vagrant
provider_slug: vagrant
rule_count: 7
rules:
- description: Vagrant Cloud API operations should use bearerAuth security
  given: $.paths[*][*]
  name: vagrant-bearer-auth
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: vagrant-operations-have-summaries
  severity: error
- description: All operations should have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: vagrant-operations-have-tags
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: vagrant-operation-ids-camel-case
  severity: warn
- description: Box paths should use :username/:name format
  given: $.paths
  name: vagrant-username-name-paths
  severity: hint
- description: Operations should document error responses
  given: $.paths[*][get,post,put,delete].responses
  name: vagrant-error-responses
  severity: warn
- description: API responses should use application/json content type
  given: $.paths[*][*].responses[*].content
  name: vagrant-json-content-type
  severity: warn
rules_file: rules/vagrant-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vagrant/refs/heads/main/rules/vagrant-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 5
slug: vagrant-rules
source_filename: vagrant-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  vagrant-bearer-auth:\n    description: Vagrant Cloud API operations should use bearerAuth security\n    message: Operations should use bearerAuth security scheme\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: truthy\n      field: security\n\n  vagrant-operations-have-summaries:\n    description: All operations must have a summary\n    message: Operations must have a summary field\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: truthy\n      field: summary\n\n  vagrant-operations-have-tags:\n    description: All operations should have at least one tag\n    message: Operations should be tagged\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: truthy\n      field: tags\n\n  vagrant-operation-ids-camel-case:\n    description: Operation IDs should use camelCase\n    message: OperationId should use camelCase\n\
  \    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  vagrant-username-name-paths:\n    description: Box paths should use :username/:name format\n    message: Box resource paths should include username and name parameters\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: truthy\n\n  vagrant-error-responses:\n    description: Operations should document error responses\n    message: Operations should have 401 or 404 error responses defined\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].responses\"\n    then:\n      function: truthy\n\n  vagrant-json-content-type:\n    description: API responses should use application/json content type\n    message: Responses should use application/json content type\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vagrant/refs/heads/main/rules/vagrant-rules.yml
tags:
- DevOps
- Virtualization
- Development Environments
- Boxes
- Cloud
- HashiCorp
- Infrastructure
- Spectral
- Linting
- API Governance
---
