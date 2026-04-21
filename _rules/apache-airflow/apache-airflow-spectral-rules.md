---
categories:
- delete
- get
- info
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tag
description: Spectral linting rules defining API design standards and conventions for Apache Airflow.
layout: rules
name: Apache Airflow API Rules
provider_name: Apache Airflow
provider_slug: apache-airflow
rule_count: 19
rules:
- description: API title must start with "Apache Airflow"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: API info must include a version.
  given: $.info
  name: info-version-required
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Apache Airflow".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-apache-airflow
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId-required
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body.
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Global tags should have descriptions.
  given: $.tags[*]
  name: tag-description-required
  severity: info
rules_file: rules/apache-airflow-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-airflow/refs/heads/main/rules/apache-airflow-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 9
slug: apache-airflow-spectral-rules
tags:
- Apache
- DAG
- Data Pipeline
- ETL
- Open Source
- Orchestration
- Python
- Scheduling
- Workflow
- Spectral
- Linting
- API Governance
---
