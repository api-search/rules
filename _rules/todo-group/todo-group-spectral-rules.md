---
categories:
- todo
description: Spectral linting rules defining API design standards and conventions for TODO Group.
layout: rules
name: TODO Group API Rules
provider_name: TODO Group
provider_slug: todo-group
rule_count: 29
rules:
- description: API must have a title in the info object.
  given: $.info
  name: todo-group-info-title-present
  severity: error
- description: API title should use Title Case.
  given: $.info.title
  name: todo-group-info-title-title-case
  severity: warn
- description: API must have a description in the info object.
  given: $.info
  name: todo-group-info-description-present
  severity: error
- description: API must declare a version.
  given: $.info
  name: todo-group-info-version-present
  severity: error
- description: API info should include contact information.
  given: $.info
  name: todo-group-info-contact-present
  severity: warn
- description: Open source APIs must declare a license.
  given: $.info
  name: todo-group-info-license-present
  severity: error
- description: API paths must use kebab-case for multi-word path segments.
  given: $.paths[*]~
  name: todo-group-paths-kebab-case
  severity: warn
- description: API paths must not end with a trailing slash.
  given: $.paths[*]~
  name: todo-group-paths-no-trailing-slash
  severity: warn
- description: API versioning should be in the path with a version prefix.
  given: $.paths[*]~
  name: todo-group-paths-no-versioning-in-path
  severity: info
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: todo-group-operation-summary-present
  severity: error
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,post,put,patch,delete,options,head].summary
  name: todo-group-operation-summary-title-case
  severity: warn
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: todo-group-operation-description-present
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: todo-group-operation-id-present
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete,options,head].operationId
  name: todo-group-operation-id-camel-case
  severity: warn
- description: Every operation should have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: todo-group-operation-tags-present
  severity: warn
- description: Every operation must define a success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: todo-group-response-success-present
  severity: error
- description: Operations should define error responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: todo-group-response-error-present
  severity: warn
- description: GET operations must return a 200 success response.
  given: $.paths[*].get.responses
  name: todo-group-get-response-200
  severity: error
- description: POST operations creating resources should return 201.
  given: $.paths[*].post.responses
  name: todo-group-post-response-201
  severity: warn
- description: Schema components should have a title.
  given: $.components.schemas[*]
  name: todo-group-schema-title-present
  severity: warn
- description: Schema components should have a description.
  given: $.components.schemas[*]
  name: todo-group-schema-description-present
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: todo-group-schema-properties-described
  severity: info
- description: Schema components should declare a type.
  given: $.components.schemas[*]
  name: todo-group-schema-type-present
  severity: warn
- description: API should define security schemes.
  given: $.components
  name: todo-group-security-schemes-present
  severity: warn
- description: Operations should define security requirements.
  given: $.paths[*][get,post,put,patch,delete]
  name: todo-group-operation-security-defined
  severity: info
- description: All parameters should have descriptions.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: todo-group-parameter-description-present
  severity: warn
- description: Parameter names should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: todo-group-parameter-name-camel-case
  severity: info
- description: API should link to external documentation.
  given: $
  name: todo-group-external-docs-present
  severity: info
- description: Tags used in operations should be defined at the top level.
  given: $.tags
  name: todo-group-tags-defined
  severity: warn
rules_file: rules/todo-group-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/todo-group/refs/heads/main/rules/todo-group-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 5
  warn: 16
slug: todo-group-spectral-rules
source_filename: todo-group-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # -----------------------------------------------------------------------\n  # 1. Info Object Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-info-title-present:\n    description: API must have a title in the info object.\n    message: \"info.title is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  todo-group-info-title-title-case:\n    description: API title should use Title Case.\n    message: \"info.title should use Title Case (capitalize first letter of each word).\"\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  todo-group-info-description-present:\n    description: API must have a description in the info object.\n    message: \"info.description is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n\
  \      function: truthy\n\n  todo-group-info-version-present:\n    description: API must declare a version.\n    message: \"info.version is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  todo-group-info-contact-present:\n    description: API info should include contact information.\n    message: \"info.contact is recommended for open source tools.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  todo-group-info-license-present:\n    description: Open source APIs must declare a license.\n    message: \"info.license is required for TODO Group open source tools.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  # -----------------------------------------------------------------------\n  # 2. Path Naming Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-paths-kebab-case:\n\
  \    description: API paths must use kebab-case for multi-word path segments.\n    message: \"Path segments should use kebab-case (e.g., /open-source-tools not /openSourceTools).\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  todo-group-paths-no-trailing-slash:\n    description: API paths must not end with a trailing slash.\n    message: \"Path must not end with a trailing slash.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  todo-group-paths-no-versioning-in-path:\n    description: API versioning should be in the path with a version prefix.\n    message: \"Use /v{n}/ versioning prefix (e.g., /v1/repositories).\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  # -----------------------------------------------------------------------\n\
  \  # 3. Operation Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-operation-summary-present:\n    description: Every operation must have a summary.\n    message: \"Operation summary is required.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  todo-group-operation-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Operation summary should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  todo-group-operation-description-present:\n    description: Every operation should have a description.\n    message: \"Operation description is recommended for open source tool APIs.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  todo-group-operation-id-present:\n    description: Every operation must have an operationId.\n    message: \"operationId is required for SDK generation and tooling.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  todo-group-operation-id-camel-case:\n    description: operationId should use camelCase.\n    message: \"operationId should use camelCase (e.g., listRepositories, lintRepository).\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  todo-group-operation-tags-present:\n    description: Every operation should have at least one tag.\n    message: \"Operation should include at least one tag for grouping.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # -----------------------------------------------------------------------\n  # 4. Response Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-response-success-present:\n    description: Every operation must define a success response.\n    message: \"At least one 2xx response is required.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  todo-group-response-error-present:\n    description: Operations should define error responses.\n    message: \"Define at least one error response (4xx or 5xx).\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  todo-group-get-response-200:\n \
  \   description: GET operations must return a 200 success response.\n    message: \"GET operations must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  todo-group-post-response-201:\n    description: POST operations creating resources should return 201.\n    message: \"POST operations should define a 201 Created response.\"\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  # -----------------------------------------------------------------------\n  # 5. Schema Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-schema-title-present:\n    description: Schema components should have a title.\n    message: \"Schema should have a title describing the resource.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\
  \n  todo-group-schema-description-present:\n    description: Schema components should have a description.\n    message: \"Schema should have a description for documentation.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  todo-group-schema-properties-described:\n    description: Schema properties should have descriptions.\n    message: \"Schema property should include a description.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  todo-group-schema-type-present:\n    description: Schema components should declare a type.\n    message: \"Schema should declare a type.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # -----------------------------------------------------------------------\n  # 6. Security Rules\n  # -----------------------------------------------------------------------\n\
  \n  todo-group-security-schemes-present:\n    description: API should define security schemes.\n    message: \"Define security schemes in components.securitySchemes.\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  todo-group-operation-security-defined:\n    description: Operations should define security requirements.\n    message: \"Operations should specify security requirements or explicitly mark as public.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # -----------------------------------------------------------------------\n  # 7. Parameter Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-parameter-description-present:\n    description: All parameters should have descriptions.\n    message: \"Parameter should include a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  todo-group-parameter-name-camel-case:\n    description: Parameter names should use camelCase.\n    message: \"Parameter name should use camelCase.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # -----------------------------------------------------------------------\n  # 8. Open Source Specific Rules\n  # -----------------------------------------------------------------------\n\n  todo-group-external-docs-present:\n    description: API should link to external documentation.\n    message: \"externalDocs is recommended for linking to full documentation.\"\n    severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n\n  todo-group-tags-defined:\n    description: Tags used in operations should be defined at the top level.\n    message:\
  \ \"Define all tags at the top level with descriptions.\"\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/todo-group/refs/heads/main/rules/todo-group-spectral-rules.yml
tags:
- Community
- Linux Foundation
- Open Source
- OSPO
- Spectral
- Linting
- API Governance
---
