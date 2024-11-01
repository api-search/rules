# API Rules
These are machine-readable API rules that define and automate the technical details behind the APIs we govern, providing specific patterns and anti-patterns that can be linted during the design, development, and build of APIs to ensure that common standards are being applied consistently across teams producing APIs.

All of the rules used to automate API governance across APIs.io APIs use a mix of linting engines like Spectral, wrapped in an API Commons schema. Rules currently are available across multiple YAML files in the repository, but these will likely be combined shortly, as things are changing rapidly to support interface work, and different approaches to automation.

## API Commons
API rules are a new [API Commons](https://apicommons.org) schema that provides a wrapper for Spectral, and eventually other linting engines applied at different stages of the API lifecycle. Rules provide more metadata, and allow for the switching of different types of rules as well as different engines processing the rules to help automate API governance.

## Example ([rule-example-1](rule-example-1.yml))

```
name: OpenAPI Info Version
slug: openapi-info-version
description: A rule for governing the info version property of the OpenAPI specification.
engine: Spectral
specification: OpenAPI
specificationUrl: https://spec.openapis.org/oas/latest.html#info-object
guidance: API Evangelist
guidanceUrl: https://guidance.apievangelist.com/guidance/openapi/info-version.html
scope: Error
type: Default

tags:
  - Versioning

rule:

  openapi-info-version-error:
    description: Publishing a version for your OpenAPI technical contract helps you
      communicate change with consumers using Semantic or date-based versioning
      published to the info version property. You can find details about the <a
      href="https://spec.openapis.org/oas/latest.html#info-object">info object
      for OpenAPI</a>, and explore <a
      href="https://guidance.apievangelist.com/guidance/openapi/info-version.html"
      target="_blank">API versioning</a> via API Evangelist guidance.
    message: Info MUST Have Version
    given: $.info
    severity: error
    then:
      field: version
      function: truthy
```

## JSON Schema ([rule-json-schema](rule-json-schema.yml))

```
"$schema": http://json-schema.org/2020-12/schema
type: object
title: Rule
description: This is a rule schema for automating the governance of APIs using multiple types of rules engines.
properties:
  name:
    type: string
    description: The name for the governance rule.
  slug:
    type: string
    description: A slugified version of the rule name.
  description:
    type: string
    description: A more detailed overview of the rule.
  engine:
    type: string
    description: Which linting engine is being applied.
    enum:
      - SPECTRAL
  specification:
    type: string
    description: The specification which the rule is applied.
  specificationUrl:
    type: string
    description: The URL to the specification page that applies.
  guidance:
    type: string
    description: The type of guidance being provided for rule.
  guidanceUrl:
    type: string
    description: The URL to the guidance page being applied.
  scope:
    type: string
    description: The scope of the rule being applied.
    enum:
      - error
      - info
      - warn
      - hint
  type:
    type: string
    description: The type of rule being applied.
    enum:
      - Default
      - Custom
  tags:
    type: array
    description: A key word or phrase applied to rule.
    items:
    - type: string
  rule:
    description: The rest of this is just Spectral JSON Schema.
    "$ref": "#/$defs/Rule"
required:
- name
- slug
- description
- engine
- specification
- specificationUrl
- guidance
- guidanceUrl
- scope
- type
- tags
- rule

"$defs":
  Ruleset:
    type: object
    additionalProperties: false
    properties:
      documentationUrl:
        type: string
        format: url
        errorMessage: must be a valid URL
      description:
        type: string
      rules:
        type: object
        additionalProperties:
          "$ref": "#/$defs/Rule"
      functions:
        "$ref": "#/$defs/Functions"
      functionsDir:
        "$ref": "#/$defs/FunctionsDir"
      formats:
        "$ref": "#/$defs/Formats"
      extends:
        "$ref": "#/$defs/Extends"
      parserOptions:
        type: object
        properties:
          duplicateKeys:
            "$ref": "#/$defs/Severity"
          incompatibleValues:
            "$ref": "#/$defs/Severity"
        additionalProperties: false
      overrides:
        type: array
        minItems: 1
        items:
          if:
            type: object
            properties:
              files:
                type: array
                minItems: 1
                items:
                  type: string
                  minLength: 1
                  pattern: "^[^#]+#"
                errorMessage: must be an non-empty array of glob patterns
            required:
            - files
          then:
            type: object
            properties:
              files: true
              rules:
                type: object
                additionalProperties:
                  "$ref": "#/$defs/Severity"
                errorMessage:
                  enum: must be a valid severity level
            required:
            - rules
            additionalProperties: false
            errorMessage:
              required: must contain rules when JSON Pointers are defined
              additionalProperties: must not override any other property than rules when
                JSON Pointers are defined
          else:
            allOf:
            - type: object
              properties:
                files:
                  type: array
                  minItems: 1
                  items:
                    type: string
                    pattern: "[^#]"
                    minLength: 1
                  errorMessage: must be an non-empty array of glob patterns
              required:
              - files
              errorMessage:
                type: 'must be an override, i.e. { "files": ["v2/**/*.json"], "rules":
                  {} }'
            - type: object
              properties:
                formats:
                  "$ref": "#/$defs/Formats"
                extends:
                  "$ref": "#/properties/extends"
                rules:
                  "$ref": "#/properties/rules"
                parserOptions:
                  "$ref": "#/properties/parserOptions"
                aliases:
                  "$ref": "#/properties/aliases"
              anyOf:
              - required:
                - extends
              - required:
                - rules
        errorMessage:
          minItems: must not be empty
      aliases:
        type: object
        propertyNames:
          pattern: "^[A-Za-z][A-Za-z0-9_-]*$"
          errorMessage:
            pattern: to avoid confusion the name must match /^[A-Za-z][A-Za-z0-9_-]*$/
              regular expression
            minLength: the name of an alias must not be empty
        additionalProperties:
          type: object
          properties:
            description:
              type: string
            targets:
              type: array
              minItems: 1
              items:
                type: object
                properties:
                  formats:
                    "$ref": "#/$defs/Formats"
                  given:
                    "$ref": "#/$defs/Given"
                required:
                - formats
                - given
                errorMessage: a valid target must contain given and non-empty formats
              errorMessage:
                minItems: targets must have at least a single alias definition
          required:
          - targets
          errorMessage:
            required: targets must be present and have at least a single alias definition
    patternProperties:
      "^x-": true
    anyOf:
    - required:
      - extends
    - required:
      - rules
    - required:
      - overrides  

  Then:
    type: object
    allOf:
    - properties:
        field:
          type: string
    - "$ref": "#/$defs/Function"
  Rule:
    type: object
    properties:
      description:
        type: string
      documentationUrl:
        type: string
        format: url
        errorMessage: must be a valid URL
      recommended:
        type: boolean
      given:
        "$ref": "#/$defs/Given"
      resolved:
        type: boolean
      severity:
        "$ref": "#/$defs/Severity"
      message:
        type: string
      tags:
        items:
          type: string
        type: array
      formats:
        "$ref": "#/$defs/Formats"
      then:
        if:
          type: array
        then:
          type: array
          items:
            "$ref": "#/$defs/Then"
        else:
          "$ref": "#/$defs/Then"
      type:
        enum:
        - style
        - validation
        type: string
        errorMessage: allowed types are "style" and "validation"
      extensions:
        type: object
    required:
    - given
    - then
    additionalProperties: false
    patternProperties:
      "^x-": true
    errorMessage:
      required: the rule must have at least "given" and "then" properties
  Formats:
    "$anchor": formats
    type: array
    items:
      "$ref": "#/$defs/Format"
    errorMessage: must be an array of formats
  DiagnosticSeverity:
    enum:
    - -1
    - 0
    - 1
    - 2
    - 3
  HumanReadableSeverity:
    enum:
    - error
    - warn
    - info
    - hint
    - 'off'
  Severity:
    "$anchor": severity
    oneOf:
    - "$ref": "#/$defs/DiagnosticSeverity"
    - "$ref": "#/$defs/HumanReadableSeverity"
    errorMessage: 'the value has to be one of: 0, 1, 2, 3 or "error", "warn", "info",
      "hint", "off"'
  Given:
    "$anchor": given
    if:
      type: array
    then:
      "$anchor": arrayish-given
      type: array
      items:
        "$ref": "#/$defs/PathExpression"
      minItems: 1
      errorMessage:
        minItems: must be a non-empty array of expressions
    else:
      "$ref": "#/$defs/PathExpression"
  PathExpression:
    "$id": path-expression
    if:
      type: string
    then:
      type: string
      if:
        pattern: "^#"
      then:
        x-spectral-runtime: alias
      else:
        pattern: "^\\$"
        errorMessage: must be a valid JSON Path expression or a reference to the existing
          Alias optionally paired with a JSON Path expression subset
    else:
      not: {}
      errorMessage: must be a valid JSON Path expression or a reference to the existing
        Alias optionally paired with a JSON Path expression subset
  Extends:
    "$anchor": extends
    oneOf:
    - type: string
    - type: array
      items:
        oneOf:
        - type: string
        - type: array
          minItems: 2
          additionalItems: false
          items:
          - type: string
          - enum:
            - all
            - recommended
            - 'off'
            errorMessage: allowed types are "off", "recommended" and "all"
  Format:
    "$anchor": format
    type: string
    errorMessage: must be a valid format
  Functions:
    "$anchor": functions
    type: array
    items:
      type: string
  FunctionsDir:
    "$anchor": functionsDir
    type: string
  Function:
    "$anchor": function
    type: object
    properties:
      function:
        type: string
    required:
    - function
```

# API Policies, Rules, Experience, and Guidance
Rule can be applied all by themselves, and are often are as part of enterprise API operations, but as part of a more holistic business and technical approach to API governance, rules can also be linked to policies, guidance, experience, and each stage of the lifecycle, helping bring more alignment between product and engineering.

<img src="https://kinlane-productions2.s3.us-east-1.amazonaws.com/policies-rules-guidance-experience-lifecycle.jpg">

This work acknowledges that services, tooling, and the general approach of API governance is only using rules applied to OpenAPI, which is beginning to expand to AsyncAPI, GraphQL, and Arazzo workflows, but is proposing the first schema for aligning this work with business objectives, when teams are ready for it.

## Support
This work is in early stage of development and rapidly moving as they are being applied in a variety of user interfaces and approaches to the automation and reporting of API governance. If you would like to contribute, have any questions, or would like to inform the work happening, please submit a GitHub issue on the repository or email kin@apievangelist.com.