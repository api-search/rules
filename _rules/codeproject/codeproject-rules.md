---
categories:
- codeproject
description: Spectral linting rules defining API design standards and conventions for CodeProject.
layout: rules
name: CodeProject API Rules
provider_name: CodeProject
provider_slug: codeproject
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: codeproject-info-contact
  severity: error
- description: Public CodeProject API servers must use HTTPS.
  given: $.servers[?(@.url && @.url.indexOf('codeproject.com') > -1)].url
  name: codeproject-public-server-https
  severity: error
- description: CodeProject.AI Server example server URL should reference localhost.
  given: $.servers[?(@.url && @.url.indexOf('localhost') > -1)].url
  name: codeproject-ai-server-localhost
  severity: info
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: codeproject-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: codeproject-operation-tags
  severity: warn
- description: All paths must be versioned under /v1/.
  given: $.paths
  name: codeproject-version-prefix
  severity: warn
- description: My/* operations must require oauth2 with at least one scope.
  given: $.paths['/v1/My/Profile','/v1/My/Reputation','/v1/My/Articles','/v1/My/Answers','/v1/My/Blog','/v1/My/Bookmarks','/v1/My/Notifications','/v1/My/Tips'][get].security
  name: codeproject-oauth2-on-my
  severity: error
- description: Operations should declare 4xx error responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: codeproject-error-responses
  severity: warn
- description: CodeProject.AI Server upload endpoints should accept multipart/form-data.
  given: $.paths[?(@property && @property.indexOf('/v1/vision/') > -1)].post.requestBody.content
  name: codeproject-ai-multipart
  severity: info
rules_file: rules/codeproject-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/codeproject/refs/heads/main/rules/codeproject-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 3
slug: codeproject-rules
tags:
- AI
- Articles
- Community
- Computer Vision
- Developer Community
- Face Recognition
- Forum
- Knowledge Base
- License Plate Recognition
- Object Detection
- Q&A
- Software Development
- Tutorials
- Spectral
- Linting
- API Governance
---
