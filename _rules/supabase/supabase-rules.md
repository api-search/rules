---
api_specs:
- filename: supabase-management-api-openapi.yml
  format: yaml
  label: Supabase Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-management-api-openapi.yml
- filename: supabase-auth-api-openapi.yml
  format: yaml
  label: Supabase Auth API
  slug: auth-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-auth-api-openapi.yml
- filename: supabase-storage-api-openapi.yml
  format: yaml
  label: Supabase Storage API
  slug: storage-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-storage-api-openapi.yml
- filename: supabase-database-rest-api-openapi.yml
  format: yaml
  label: Supabase Database REST API
  slug: database-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-database-rest-api-openapi.yml
- filename: supabase-edge-functions-api-openapi.yml
  format: yaml
  label: Supabase Edge Functions API
  slug: edge-functions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-edge-functions-api-openapi.yml
- filename: supabase-realtime-api-asyncapi.yml
  format: yaml
  label: Supabase Realtime API
  slug: realtime-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/asyncapi/supabase-realtime-api-asyncapi.yml
categories:
- supabase
description: Spectral linting rules defining API design standards and conventions for Supabase.
layout: rules
name: Supabase API Rules
provider_name: Supabase
provider_slug: supabase
rule_count: 11
rules:
- description: Supabase operation IDs must use camelCase (e.g. listProjects, createProject)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: supabase-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: supabase-tags-title-case
  severity: warn
- description: All operation tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: supabase-operation-tags-title-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: supabase-summaries-title-case
  severity: warn
- description: Server URLs with per-project base URLs must use {project_ref} variable naming convention
  given: $.servers[*].variables
  name: supabase-project-ref-variable
  severity: warn
- description: Supabase APIs use either apikey header authentication, Bearer JWT authentication, or both. Every operation should specify security.
  given: $.paths[*][get,post,put,patch,delete]
  name: supabase-security-apikey-or-bearer
  severity: warn
- description: Operations should document 401 Unauthorized responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: supabase-error-responses
  severity: info
- description: POST operations creating resources should have a request body
  given: $.paths[*].post
  name: supabase-request-body-post
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: supabase-operation-description
  severity: info
- description: APIs must include contact information
  given: $.info
  name: supabase-info-contact
  severity: warn
- description: APIs must define at least one server
  given: $
  name: supabase-servers-defined
  severity: error
rules_file: rules/supabase-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/rules/supabase-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 8
slug: supabase-rules
source_filename: supabase-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  supabase-operation-ids-camel-case:\n    description: Supabase operation IDs must use camelCase (e.g. listProjects, createProject)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  supabase-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  supabase-operation-tags-title-case:\n    description: All operation tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  supabase-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"\
  $.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  supabase-project-ref-variable:\n    description: >-\n      Server URLs with per-project base URLs must use {project_ref} variable\n      naming convention\n    severity: warn\n    given: \"$.servers[*].variables\"\n    then:\n      function: truthy\n\n  supabase-security-apikey-or-bearer:\n    description: >-\n      Supabase APIs use either apikey header authentication, Bearer JWT\n      authentication, or both. Every operation should specify security.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  supabase-error-responses:\n    description: Operations should document 401 Unauthorized responses\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  supabase-request-body-post:\n\
  \    description: POST operations creating resources should have a request body\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  supabase-operation-description:\n    description: All operations should have a description\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: defined\n\n  supabase-info-contact:\n    description: APIs must include contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  supabase-servers-defined:\n    description: APIs must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/rules/supabase-rules.yml
tags:
- Backend As A Service
- PostgreSQL
- Open Source
- Authentication
- Real Time
- Storage
- Edge Functions
- Database
- Spectral
- Linting
- API Governance
---
