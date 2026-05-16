---
api_specs:
- filename: openapi
  format: yaml
  label: Memesio API
  slug: memesio-api
  spec_type: OpenAPI
  url: https://memesio.com/api/openapi
categories:
- memesio
description: Spectral linting rules defining API design standards and conventions for Memesio.
layout: rules
name: Memesio API Rules
provider_name: Memesio
provider_slug: memesio
rule_count: 18
rules:
- description: API info.title must include "Memesio".
  given: $.info.title
  name: memesio-info-title-required
  severity: warn
- description: API info.version must be present and follow semver-like format.
  given: $.info.version
  name: memesio-info-version-required
  severity: error
- description: All paths must be served under /api (Memesio routes prefix all surfaces with /api).
  given: $.paths.*~
  name: memesio-paths-must-start-with-api
  severity: error
- description: Path segments must use kebab-case (lowercase with hyphens), not snake_case or camelCase.
  given: $.paths.*~
  name: memesio-paths-kebab-case
  severity: warn
- description: Long-lived versioned routes use /api/v1/* (e.g. /api/v1/agents, /api/v1/memes, /api/v1/templates).
  given: $.paths[?(@property.match(/\/api\/v\d+\//) && !@property.startsWith('/api/v1/'))]~
  name: memesio-versioned-paths-under-v1
  severity: hint
- description: Operation summaries must be in Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: memesio-operation-summary-title-case
  severity: warn
- description: Every operation must have a non-empty summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: memesio-operation-summary-required
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: memesio-operation-must-have-tags
  severity: error
- description: Tags should come from the Memesio domain vocabulary.
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: memesio-operation-tag-vocabulary
  severity: hint
- description: Operations should declare at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: memesio-response-codes-required
  severity: warn
- description: AI features live under /api/ai/* or are explicitly tagged "ai".
  given: $.paths[?(@property.match(/(caption|generate|face-swap|background-remove|moderate)/) && !@property.match(/\/api\/ai\//) && !@property.match(/\/free\//))]~
  name: memesio-ai-routes-grouped
  severity: hint
- description: Mutating AI endpoints under /api/ai/captions and /api/ai/memes should expose a sibling GET for quota inspection.
  given: $.paths[?(@property.match(/\/api\/ai\/(captions|memes)\/generate$/))]
  name: memesio-ai-quota-get-pairing
  severity: hint
- description: Anonymous routes under /api/free/* must carry the "public-free" tag.
  given: $.paths[?(@property.startsWith('/api/free/'))][get,post].tags
  name: memesio-free-routes-tagged-public-free
  severity: error
- description: Agent identity and key management routes under /api/v1/agents/* must be tagged "agent-infra" or "developer-api".
  given: $.paths[?(@property.startsWith('/api/v1/agents'))][get,post,patch,delete].tags
  name: memesio-agent-routes-tagged
  severity: warn
- description: List endpoints that paginate must expose `page` and `pageSize` query parameters.
  given: $.paths[*].get.parameters
  name: memesio-list-pagination-shape
  severity: hint
- description: pageSize parameters should declare a maximum.
  given: $.paths[*][get].parameters[?(@.name=='pageSize')].schema
  name: memesio-pagesize-bounded
  severity: warn
- description: Component schemas must be PascalCase.
  given: $.components.schemas.*~
  name: memesio-schema-names-pascal-case
  severity: warn
- description: MemeSummary should expose stable identifiers and a hosted URL.
  given: $.components.schemas.MemeSummary.properties
  name: memesio-meme-summary-required-fields
  severity: hint
rules_file: rules/memesio-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/memesio/refs/heads/main/rules/memesio-rules.yml
severity_counts:
  error: 5
  hint: 6
  info: 0
  warn: 7
slug: memesio-rules
source_filename: memesio-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - \"spectral:oas\"\ndocumentationUrl: https://memesio.com/developers/api\ndescription: |\n  Spectral ruleset enforcing the conventions observed in Memesio's OpenAPI\n  contract (https://memesio.com/api/openapi). Covers naming, tagging,\n  authentication, AI quota signaling, public/free routes, agent identity, and\n  caption/template content discipline.\n\nfunctions: []\n\nrules:\n  # === Provider info ============================================================\n  memesio-info-title-required:\n    description: API info.title must include \"Memesio\".\n    message: '{{property}} should mention \"Memesio\" — \"{{value}}\" does not.'\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)Memesio\"\n\n  memesio-info-version-required:\n    description: API info.version must be present and follow semver-like format.\n    severity: error\n    given: $.info.version\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^\\\\d+\\\\.\\\\d+\\\\.\\\\d+(-[A-Za-z0-9.]+)?$\"\n\n  # === Path conventions =========================================================\n  memesio-paths-must-start-with-api:\n    description: All paths must be served under /api (Memesio routes prefix all surfaces with /api).\n    message: '{{path}} should start with /api/'\n    severity: error\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/\"\n\n  memesio-paths-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens), not snake_case or camelCase.\n    message: 'Path segment in {{path}} should be kebab-case.'\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/(api|v1|v\\\\d+)|/[a-z0-9-]+|/\\\\{[a-zA-Z]+\\\\})+$\"\n\n  memesio-versioned-paths-under-v1:\n    description: Long-lived versioned routes use /api/v1/* (e.g. /api/v1/agents, /api/v1/memes,\
  \ /api/v1/templates).\n    message: '{{path}} appears to be a versioned route but does not use /api/v1/.'\n    severity: hint\n    given: $.paths[?(@property.match(/\\/api\\/v\\d+\\//) && !@property.startsWith('/api/v1/'))]~\n    then:\n      function: falsy\n\n  # === Operation conventions ====================================================\n  memesio-operation-summary-title-case:\n    description: Operation summaries must be in Title Case.\n    message: 'Summary \"{{value}}\" should be Title Case.'\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  memesio-operation-summary-required:\n    description: Every operation must have a non-empty summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  memesio-operation-must-have-tags:\n    description: Every operation must declare at least\
  \ one tag.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  memesio-operation-tag-vocabulary:\n    description: Tags should come from the Memesio domain vocabulary.\n    message: 'Tag \"{{value}}\" is outside the known Memesio tag vocabulary.'\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete].tags[*]\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - agent-infra\n          - ai\n          - ai-captions\n          - ai-jobs\n          - ai-providers\n          - analytics\n          - audio\n          - auth\n          - backend\n          - background-remove\n          - billing\n          - channels\n          - collaboration\n          - compliance\n          - data-eng\n          - data-ops\n          - data-science\n          - developer-api\n          - distribution\n          - experimentation\n          - face-swap\n          - finops\n\
  \          - growth\n          - history\n          - lifecycle\n          - marketing-ops\n          - media\n          - memes\n          - moderation\n          - motion\n          - notifications\n          - observability\n          - performance\n          - personalization\n          - platform\n          - product-marketing\n          - public-free\n          - safety\n          - templates\n          - trend-alerts\n          - uploads\n          - video\n\n  memesio-response-codes-required:\n    description: Operations should declare at least one 2xx response.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2\\\\d{2}$\":\n              type: object\n\n  # === AI / quota routes ========================================================\n  memesio-ai-routes-grouped:\n    description: AI features live under\
  \ /api/ai/* or are explicitly tagged \"ai\".\n    message: '{{path}} looks AI-related but lives outside /api/ai/.'\n    severity: hint\n    given: $.paths[?(@property.match(/(caption|generate|face-swap|background-remove|moderate)/) && !@property.match(/\\/api\\/ai\\//) && !@property.match(/\\/free\\//))]~\n    then:\n      function: falsy\n\n  memesio-ai-quota-get-pairing:\n    description: Mutating AI endpoints under /api/ai/captions and /api/ai/memes should expose a sibling GET for quota inspection.\n    severity: hint\n    given: $.paths[?(@property.match(/\\/api\\/ai\\/(captions|memes)\\/generate$/))]\n    then:\n      field: get\n      function: truthy\n\n  # === Public/free routes =======================================================\n  memesio-free-routes-tagged-public-free:\n    description: Anonymous routes under /api/free/* must carry the \"public-free\" tag.\n    severity: error\n    given: $.paths[?(@property.startsWith('/api/free/'))][get,post].tags\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: \"public-free\"\n\n  # === Agent identity routes ====================================================\n  memesio-agent-routes-tagged:\n    description: Agent identity and key management routes under /api/v1/agents/* must be tagged \"agent-infra\" or \"developer-api\".\n    severity: warn\n    given: $.paths[?(@property.startsWith('/api/v1/agents'))][get,post,patch,delete].tags\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            anyOf:\n              - const: \"agent-infra\"\n              - const: \"developer-api\"\n\n  # === Pagination ===============================================================\n  memesio-list-pagination-shape:\n    description: List endpoints that paginate must expose `page` and `pageSize` query parameters.\n    severity: hint\n    given: $.paths[*].get.parameters\n    then:\n\
  \      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  memesio-pagesize-bounded:\n    description: pageSize parameters should declare a maximum.\n    severity: warn\n    given: $.paths[*][get].parameters[?(@.name=='pageSize')].schema\n    then:\n      field: maximum\n      function: truthy\n\n  # === Schemas ==================================================================\n  memesio-schema-names-pascal-case:\n    description: Component schemas must be PascalCase.\n    severity: warn\n    given: $.components.schemas.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]+$\"\n\n  memesio-meme-summary-required-fields:\n    description: MemeSummary should expose stable identifiers and a hosted URL.\n    severity: hint\n    given: $.components.schemas.MemeSummary.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [slug]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/memesio/refs/heads/main/rules/memesio-rules.yml
tags:
- Memes
- Media
- Image Generation
- Content
- Developer Tools
- Spectral
- Linting
- API Governance
---
