---
api_specs:
- filename: sap-api-management-portal-openapi.yml
  format: yaml
  label: SAP API Management API Portal API
  slug: sap-api-management-api-portal
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-api-management/refs/heads/main/openapi/sap-api-management-portal-openapi.yml
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP API Management.
layout: rules
name: SAP API Management API Rules
provider_name: SAP API Management
provider_slug: sap-api-management
rule_count: 7
rules:
- description: SAP API Management endpoints require OAuth 2.0 authentication
  given: $.paths[*][*]
  name: sap-apimgmt-oauth2-required
  severity: error
- description: All SAP API Management servers must use HTTPS
  given: $.servers[*]
  name: sap-apimgmt-https-only
  severity: error
- description: All operations must have operationId for automation tooling
  given: $.paths[*][*]
  name: sap-apimgmt-operation-id-required
  severity: error
- description: All operations must have tags for grouping in developer portal
  given: $.paths[*][*]
  name: sap-apimgmt-tags-required
  severity: warn
- description: OData responses should use the d.results envelope format
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: sap-apimgmt-odata-response-format
  severity: info
- description: All operations must have descriptions
  given: $.paths[*][*]
  name: sap-apimgmt-description-required
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: sap-apimgmt-204-on-delete
  severity: warn
rules_file: rules/sap-api-management-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-api-management/refs/heads/main/rules/sap-api-management-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: sap-api-management-rules
source_filename: sap-api-management-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sap-apimgmt-oauth2-required:\n    description: SAP API Management endpoints require OAuth 2.0 authentication\n    message: \"Endpoint {{path}} must use OAuth2 security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n\n  sap-apimgmt-https-only:\n    description: All SAP API Management servers must use HTTPS\n    message: \"Server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  sap-apimgmt-operation-id-required:\n    description: All operations must have operationId for automation tooling\n    message: \"Operation at {{path}} must have an operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function:\
  \ truthy\n\n  sap-apimgmt-tags-required:\n    description: All operations must have tags for grouping in developer portal\n    message: \"Operation {{operationId}} must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  sap-apimgmt-odata-response-format:\n    description: OData responses should use the d.results envelope format\n    message: \"OData response at {{path}} should use d.results envelope\"\n    severity: info\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            d:\n              type: object\n\n  sap-apimgmt-description-required:\n    description: All operations must have descriptions\n    message: \"Operation {{operationId}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n\
  \      function: truthy\n\n  sap-apimgmt-204-on-delete:\n    description: DELETE operations should return 204 No Content\n    message: \"DELETE operation at {{path}} should return 204\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-api-management/refs/heads/main/rules/sap-api-management-rules.yml
tags:
- API Management
- Developer Portal
- Enterprise
- SAP
- Spectral
- Linting
- API Governance
---
