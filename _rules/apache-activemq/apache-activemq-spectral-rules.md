---
categories:
- delete
- get
- info
- operation
- parameter
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache ActiveMQ.
layout: rules
name: Apache ActiveMQ API Rules
provider_name: Apache ActiveMQ
provider_slug: apache-activemq
rule_count: 19
rules:
- description: API title must start with "Apache ActiveMQ"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API must have a description of at least 50 characters.
  given: $.info
  name: info-description-required
  severity: error
- description: API info must include a version.
  given: $.info
  name: info-version-required
  severity: error
- description: API must declare an Apache 2.0 license.
  given: $.info
  name: info-license-required
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Server URLs should use HTTPS in production.
  given: $.servers[*].url
  name: servers-https-only
  severity: info
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Apache ActiveMQ".
  given: $.paths[*][get,post,put,patch,delete,options,head].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-operationId-required
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,patch,delete,options,head].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete,options,head].responses
  name: response-success-required
  severity: error
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head].responses[*]
  name: response-description-required
  severity: error
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
- description: Operations should include x-microcks-operation extension for mock server compatibility.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-microcks-extension
  severity: info
rules_file: rules/apache-activemq-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-activemq/refs/heads/main/rules/apache-activemq-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 9
slug: apache-activemq-spectral-rules
tags:
- AMQP
- Apache
- Java
- JMS
- Message Broker
- Messaging
- MQTT
- Open Source
- STOMP
- Spectral
- Linting
- API Governance
---
