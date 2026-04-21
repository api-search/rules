---
categories:
- avro
description: Spectral linting rules defining API design standards and conventions for Apache Avro.
layout: rules
name: Apache Avro API Rules
provider_name: Apache Avro
provider_slug: avro
rule_count: 15
rules:
- description: Avro schemas must specify a type.
  given: $
  name: avro-schema-type-required
  severity: error
- description: Avro record types must have a name.
  given: $..[?(@.type == 'record')]
  name: avro-record-name-required
  severity: error
- description: Avro record types must have a fields array.
  given: $..[?(@.type == 'record')]
  name: avro-record-fields-required
  severity: error
- description: Each Avro record field must have a name.
  given: $..fields[*]
  name: avro-field-name-required
  severity: error
- description: Each Avro record field must have a type.
  given: $..fields[*]
  name: avro-field-type-required
  severity: error
- description: Avro enum types must have a name.
  given: $..[?(@.type == 'enum')]
  name: avro-enum-name-required
  severity: error
- description: Avro enum types must define symbols.
  given: $..[?(@.type == 'enum')]
  name: avro-enum-symbols-required
  severity: error
- description: Avro fixed types must have a name.
  given: $..[?(@.type == 'fixed')]
  name: avro-fixed-name-required
  severity: error
- description: Avro fixed types must specify a size.
  given: $..[?(@.type == 'fixed')]
  name: avro-fixed-size-required
  severity: error
- description: Avro named types should include a namespace.
  given: $..[?(@.type == 'record' || @.type == 'enum' || @.type == 'fixed')]
  name: avro-namespace-recommended
  severity: warn
- description: Avro schemas should include documentation.
  given: $
  name: avro-doc-recommended
  severity: warn
- description: Avro record fields should include documentation.
  given: $..fields[*]
  name: avro-field-doc-recommended
  severity: info
- description: Nullable Avro fields should specify a default value.
  given: $..fields[?(@.type[0] == 'null')]
  name: avro-field-default-for-nullable
  severity: warn
- description: Avro schema names should use camelCase or PascalCase.
  given: $..name
  name: avro-name-camel-case
  severity: info
- description: Avro namespaces should use dot-separated package notation.
  given: $..namespace
  name: avro-namespace-dot-separated
  severity: warn
rules_file: rules/avro-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/avro/refs/heads/main/rules/avro-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 2
  warn: 4
slug: avro-spectral-rules
tags:
- Apache
- Big Data
- Binary Format
- Data Serialization
- Schema Evolution
- Spectral
- Linting
- API Governance
---
