---
categories:
- cff
description: Spectral linting rules defining API design standards and conventions for Citation File Format.
layout: rules
name: Citation File Format API Rules
provider_name: Citation File Format
provider_slug: citation-cff
rule_count: 10
rules:
- description: A CITATION.cff file MUST declare a cff-version field.
  given: '#CitationCff'
  name: cff-version-required
  severity: error
- description: cff-version SHOULD be 1.2.0 to use the current schema.
  given: '#CitationCff.cff-version'
  name: cff-version-current
  severity: warn
- description: A CITATION.cff file MUST contain a message field.
  given: '#CitationCff'
  name: cff-message-required
  severity: error
- description: A CITATION.cff file MUST contain a title field.
  given: '#CitationCff'
  name: cff-title-required
  severity: error
- description: A CITATION.cff file MUST contain at least one author.
  given: '#CitationCff'
  name: cff-authors-required
  severity: error
- description: A CITATION.cff file SHOULD declare a DOI for citable releases.
  given: '#CitationCff'
  name: cff-doi-recommended
  severity: warn
- description: A CITATION.cff file SHOULD declare a software version.
  given: '#CitationCff'
  name: cff-version-recommended
  severity: warn
- description: A CITATION.cff file SHOULD declare a date-released.
  given: '#CitationCff'
  name: cff-date-released-recommended
  severity: warn
- description: A CITATION.cff file SHOULD declare an SPDX license identifier.
  given: '#CitationCff'
  name: cff-license-recommended
  severity: warn
- description: A CITATION.cff file SHOULD declare a repository-code URL.
  given: '#CitationCff'
  name: cff-repository-recommended
  severity: warn
rules_file: rules/citation-cff-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/citation-cff/refs/heads/main/rules/citation-cff-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: citation-cff-rules
tags:
- Academic
- Citation
- Metadata
- Open Standard
- Repository
- Research
- Software
- YAML
- Spectral
- Linting
- API Governance
---
