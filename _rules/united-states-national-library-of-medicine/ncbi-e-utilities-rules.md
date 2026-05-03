---
api_specs:
- filename: ncbi-e-utilities-openapi.yml
  format: yaml
  label: NCBI E-Utilities API
  slug: ncbi-e-utilities-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-national-library-of-medicine/refs/heads/main/openapi/ncbi-e-utilities-openapi.yml
- filename: openapi3.docs.yaml
  format: yaml
  label: NCBI Datasets REST API
  slug: ncbi-datasets-api
  spec_type: OpenAPI
  url: https://www.ncbi.nlm.nih.gov/datasets/docs/v2/openapi3/openapi3.docs.yaml
- filename: ncbi-blast-openapi.yml
  format: yaml
  label: NCBI BLAST URL API
  slug: ncbi-blast-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-national-library-of-medicine/refs/heads/main/openapi/ncbi-blast-openapi.yml
- filename: nlm-clinicaltrials-openapi.yml
  format: yaml
  label: ClinicalTrials.gov API
  slug: nlm-clinical-trials-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-national-library-of-medicine/refs/heads/main/openapi/nlm-clinicaltrials-openapi.yml
categories:
- ncbi
description: Spectral linting rules defining API design standards and conventions for United States National Library of Medicine.
layout: rules
name: United States National Library of Medicine API Rules
provider_name: United States National Library of Medicine
provider_slug: united-states-national-library-of-medicine
rule_count: 7
rules:
- description: All operations must have operationIds.
  given: $.paths[*][get,post,put,delete,patch]
  name: ncbi-operation-ids-required
  severity: error
- description: E-utilities operations require a db parameter.
  given: $.paths[?(@property =~ /esearch|efetch|esummary|elink/)][get].parameters[?(@.name == 'db')]
  name: ncbi-db-param-for-eutils
  severity: error
- description: All operations should have tags for grouping.
  given: $.paths[*][get,post,put,delete,patch]
  name: ncbi-operations-have-tags
  severity: warn
- description: All parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: ncbi-parameters-have-descriptions
  severity: warn
- description: Operations must document 200 success responses.
  given: $.paths[*][get,post,put].responses
  name: ncbi-success-responses
  severity: error
- description: Schema components should have descriptions.
  given: $.components.schemas[*]
  name: ncbi-schemas-have-descriptions
  severity: warn
- description: API info should include contact information.
  given: $.info
  name: ncbi-info-contact
  severity: warn
rules_file: rules/ncbi-e-utilities-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-national-library-of-medicine/refs/heads/main/rules/ncbi-e-utilities-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: ncbi-e-utilities-rules
source_filename: ncbi-e-utilities-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  ncbi-operation-ids-required:\n    description: All operations must have operationIds.\n    message: Operation must have an operationId.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n    severity: error\n\n  ncbi-db-param-for-eutils:\n    description: E-utilities operations require a db parameter.\n    message: E-utilities operations should include a db query parameter.\n    given: \"$.paths[?(@property =~ /esearch|efetch|esummary|elink/)][get].parameters[?(@.name == 'db')]\"\n    then:\n      field: required\n      function: truthy\n    severity: error\n\n  ncbi-operations-have-tags:\n    description: All operations should have tags for grouping.\n    message: Operation must include at least one tag.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  ncbi-parameters-have-descriptions:\n    description: All parameters\
  \ should have descriptions.\n    message: Parameter must have a description.\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  ncbi-success-responses:\n    description: Operations must document 200 success responses.\n    message: Operation must document a 200 success response.\n    given: \"$.paths[*][get,post,put].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n\n  ncbi-schemas-have-descriptions:\n    description: Schema components should have descriptions.\n    message: Schema component must have a description.\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  ncbi-info-contact:\n    description: API info should include contact information.\n    message: API info block must contain a contact object.\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n    severity:\
  \ warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-national-library-of-medicine/refs/heads/main/rules/ncbi-e-utilities-rules.yml
tags:
- Federal Government
- Biomedical Research
- Healthcare
- Genomics
- Literature
- Spectral
- Linting
- API Governance
---
