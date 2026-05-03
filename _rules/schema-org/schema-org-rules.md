---
categories:
- schema
description: Spectral linting rules defining API design standards and conventions for Schema.org.
layout: rules
name: Schema.org API Rules
provider_name: Schema.org
provider_slug: schema-org
rule_count: 10
rules:
- description: JSON-LD documents must include @context pointing to schema.org
  given: $
  name: schema-org-context-required
  severity: error
- description: JSON-LD documents must include @type declaring the Schema.org type
  given: $
  name: schema-org-type-required
  severity: error
- description: Most Schema.org types should have a name property
  given: $[?(@type)]
  name: schema-org-name-recommended
  severity: warn
- description: URL properties must be valid URIs
  given: $.url
  name: schema-org-url-format
  severity: error
- description: sameAs references should be valid URIs
  given: $.sameAs
  name: schema-org-same-as-format
  severity: warn
- description: AggregateRating must include ratingValue
  given: $[?(@type == 'AggregateRating')]
  name: schema-org-aggregate-rating-values
  severity: warn
- description: Offers must include both price and priceCurrency
  given: $[?(@type == 'Offer')]
  name: schema-org-offer-price-currency
  severity: error
- description: WebAPI types should include documentation URL
  given: $[?(@type == 'WebAPI')]
  name: schema-org-webapi-documentation
  severity: warn
- description: Organization entities should include a URL
  given: $[?(@type == 'Organization')]
  name: schema-org-organization-url
  severity: warn
- description: Person entities must include a name
  given: $[?(@type == 'Person')]
  name: schema-org-person-name
  severity: error
rules_file: rules/schema-org-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/schema-org/refs/heads/main/rules/schema-org-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: schema-org-rules
source_filename: schema-org-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  schema-org-context-required:\n    description: JSON-LD documents must include @context pointing to schema.org\n    message: \"JSON-LD structured data must include @context with schema.org or https://schema.org\"\n    severity: error\n    given: \"$\"\n    then:\n      field: \"@context\"\n      function: truthy\n\n  schema-org-type-required:\n    description: JSON-LD documents must include @type declaring the Schema.org type\n    message: \"JSON-LD structured data must include @type\"\n    severity: error\n    given: \"$\"\n    then:\n      field: \"@type\"\n      function: truthy\n\n  schema-org-name-recommended:\n    description: Most Schema.org types should have a name property\n    message: \"Schema.org entities should have a name property for human-readable identification\"\n    severity: warn\n    given: \"$[?(@type)]\"\n    then:\n      field: name\n      function: truthy\n\n  schema-org-url-format:\n    description: URL properties must be valid URIs\n    message:\
  \ \"Schema.org url properties must be valid URIs\"\n    severity: error\n    given: \"$.url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https?://\"\n\n  schema-org-same-as-format:\n    description: sameAs references should be valid URIs\n    message: \"sameAs links should be valid URIs pointing to authoritative references\"\n    severity: warn\n    given: \"$.sameAs\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https?://\"\n\n  schema-org-aggregate-rating-values:\n    description: AggregateRating must include ratingValue\n    message: \"AggregateRating should include ratingValue, ratingCount, and bestRating\"\n    severity: warn\n    given: \"$[?(@type == 'AggregateRating')]\"\n    then:\n      field: ratingValue\n      function: truthy\n\n  schema-org-offer-price-currency:\n    description: Offers must include both price and priceCurrency\n    message: \"Offer objects must include both price and priceCurrency properties\"\
  \n    severity: error\n    given: \"$[?(@type == 'Offer')]\"\n    then:\n      field: priceCurrency\n      function: truthy\n\n  schema-org-webapi-documentation:\n    description: WebAPI types should include documentation URL\n    message: \"WebAPI structured data should include a documentation URL\"\n    severity: warn\n    given: \"$[?(@type == 'WebAPI')]\"\n    then:\n      field: documentation\n      function: truthy\n\n  schema-org-organization-url:\n    description: Organization entities should include a URL\n    message: \"Organization type should include a url property\"\n    severity: warn\n    given: \"$[?(@type == 'Organization')]\"\n    then:\n      field: url\n      function: truthy\n\n  schema-org-person-name:\n    description: Person entities must include a name\n    message: \"Person type must include a name property\"\n    severity: error\n    given: \"$[?(@type == 'Person')]\"\n    then:\n      field: name\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/schema-org/refs/heads/main/rules/schema-org-rules.yml
tags:
- Schema.org
- Structured Data
- Linked Data
- JSON-LD
- Vocabulary
- SEO
- Web Standards
- RDF
- Ontology
- Spectral
- Linting
- API Governance
---
