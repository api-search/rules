---
api_specs:
- filename: svn-webdav-openapi.yml
  format: yaml
  label: SVN WebDAV HTTP API
  slug: svn-webdav-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/svn/refs/heads/main/openapi/svn-webdav-openapi.yml
categories:
- svn
description: Spectral linting rules defining API design standards and conventions for Subversion.
layout: rules
name: Subversion API Rules
provider_name: Subversion
provider_slug: svn
rule_count: 8
rules:
- description: All SVN WebDAV operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: svn-operations-have-tags
  severity: warn
- description: All SVN WebDAV operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: svn-operations-have-summaries
  severity: error
- description: All SVN WebDAV operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: svn-operations-have-operation-ids
  severity: error
- description: SVN operation summaries must use Title Case
  given: $.paths[*][get,put,post,delete,patch].summary
  name: svn-summaries-title-case
  severity: warn
- description: All SVN WebDAV operations must have a description
  given: $.paths[*][get,put,post,delete,patch]
  name: svn-operations-have-descriptions
  severity: warn
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: svn-responses-have-descriptions
  severity: warn
- description: All path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: svn-path-parameters-required
  severity: error
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: svn-components-schemas-described
  severity: warn
rules_file: rules/svn-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/svn/refs/heads/main/rules/svn-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: svn-rules
source_filename: svn-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  svn-operations-have-tags:\n    description: All SVN WebDAV operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  svn-operations-have-summaries:\n    description: All SVN WebDAV operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  svn-operations-have-operation-ids:\n    description: All SVN WebDAV operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  svn-summaries-title-case:\n    description: SVN operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  svn-operations-have-descriptions:\n    description: All SVN WebDAV operations must have a description\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  svn-responses-have-descriptions:\n    description: All response objects must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  svn-path-parameters-required:\n    description: All path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  svn-components-schemas-described:\n    description: All component schemas must have a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/svn/refs/heads/main/rules/svn-rules.yml
tags:
- Apache
- Open Source
- Repository
- Source Control
- Svn
- Version Control
- Webdav
- Spectral
- Linting
- API Governance
---
