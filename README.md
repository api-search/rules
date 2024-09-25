# APIs.io Governance Rules
These are all of the Spectral rules used to govern the APIs published to support the APIs.io platform, providing machine-readable rules for both the [APIs.json](https://apisjson.org/) and [OpenAPI](https://www.openapis.org/) specifications.

## Operational Rules
This are the Spectral rules governing the operations surrounding the APIs.io API search API, linting for all the things that support both producer and consumers of the API.

## APIs MUST have a aid property. (apis-json-apis-aid-error)
This property ensures that a collection of APIs defined using a APIs.json can have a unique identifier expressed as an `aid`. API identifiers (AID) are a standardized format for allowing API producers to establish a unique identifier for API resources and capabilities they publish using APIs.json, which will have the aid for the APIs.json prepended to each APIs aid. You can find details about the <a href="https://apisjson.org/schema/aid/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/identifiers/api-identifier.html" target="_blank">API Unique Identifiers</a> more via API Evangelist.

```
description: >-
  This property ensures that a collection of APIs defined using a APIs.json can
  have a unique identifier expressed as an `aid`. API identifiers (AID) are a
  standardized format for allowing API producers to establish a unique
  identifier for API resources and capabilities they publish using APIs.json,
  which will have the aid for the APIs.json prepended to each APIs aid. You can
  find details about the <a href="https://apisjson.org/schema/aid/">aid property
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/identifiers/api-identifier.html"
  target="_blank">API Unique Identifiers</a> more via API Evangelist.
message: APIs MUST have a aid property.
given: $.apis.*
severity: error
then:
  field: aid
  function: truthy
```
## API has an aid property. (apis-json-apis-aid-info)
This property ensures that each APIs indexed within an APIs.json can have a unique identifier expressed as an `aid`. API identifiers (AID) are a standardized format for allowing API producers to establish a unique identifier for each API they publish using APIs.json, which will have the aid for the APIs.json prepended to each APIs aid. You can find details about the <a href="https://apisjson.org/schema/aid/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/unique-identifiers.html" target="_blank">API Unique Identifiers</a> more via API Evangelist.

```
description: >-
  This property ensures that each APIs indexed within an APIs.json can have a
  unique identifier expressed as an `aid`. API identifiers (AID) are a
  standardized format for allowing API producers to establish a unique
  identifier for each API they publish using APIs.json, which will have the aid
  for the APIs.json prepended to each APIs aid. You can find details about the
  <a href="https://apisjson.org/schema/aid/">aid property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/apis/unique-identifiers.html"
  target="_blank">API Unique Identifiers</a> more via API Evangelist.
message: API has an aid property.
given: $.apis.*
severity: info
then:
  field: aid
  function: falsy
```
## APIs MUST Have a Base URL (apis-json-apis-baseURL-error)
This is the base URL used for an API defined using APIs.json, providing a reference for developers to use when onboarding and making calls to an API, but it is also used as a way of referencing an API, and validating what domain it is part of. You can find details about the <a href="https://apisjson.org/schema/base-url/">baseUrl property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/base-url.html" target="_blank">Base URLs</a> more via API Evangelist.

```
description: >-
  This is the base URL used for an API defined using APIs.json, providing a
  reference for developers to use when onboarding and making calls to an API,
  but it is also used as a way of referencing an API, and validating what domain
  it is part of. You can find details about the <a
  href="https://apisjson.org/schema/base-url/">baseUrl property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/apis/base-url.html"
  target="_blank">Base URLs</a> more via API Evangelist.
message: APIs MUST Have a Base URL
given: $.apis.*
severity: error
then:
  field: baseURL
  function: truthy
```
## APIs Has a Base URL (apis-json-apis-baseURL-info)
This is the base URL used for an API defined using APIs.json, providing a reference for developers to use when onboarding and making calls to an API, but it is also used as a way of referencing an API, and validating what domain it is part of. You can find details about the <a href="https://apisjson.org/schema/base-url/">baseUrl property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/base-url.html" target="_blank">Base URLs</a> more via API Evangelist.

```
description: >-
  This is the base URL used for an API defined using APIs.json, providing a
  reference for developers to use when onboarding and making calls to an API,
  but it is also used as a way of referencing an API, and validating what domain
  it is part of. You can find details about the <a
  href="https://apisjson.org/schema/base-url/">baseUrl property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/apis/base-url.html"
  target="_blank">Base URLs</a> more via API Evangelist.
message: APIs Has a Base URL
given: $.apis.*
severity: info
then:
  field: baseURL
  function: falsy
```
## API contact COULD have email. (apis-json-apis-contact-email-error)
Providing an email address is a quick way to provide support for each API being indexed. Depending on whether it is public or private, the email may be an individual or wider, and associated with a team. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/email.html" target="_blank">support emails</a> more via API Evangelist.

```
description: >-
  Providing an email address is a quick way to provide support for each API
  being indexed. Depending on whether it is public or private, the email may be
  an individual or wider, and associated with a team. You can find details about
  the <a href="https://apisjson.org/schema/apis-contact/">API contact property
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/email.html"
  target="_blank">support emails</a> more via API Evangelist.
message: API contact COULD have email.
given: $.apis.*.contact.*
severity: error
then:
  field: email
  function: truthy
```
## API contact has email. (apis-json-apis-contact-email-info)
Providing an email address is a quick way to provide support for each API being indexed. Depending on whether it is public or private, the email may be an individual or wider, and associated with a team. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/email.html" target="_blank">support emails</a> more via API Evangelist.

```
description: >-
  Providing an email address is a quick way to provide support for each API
  being indexed. Depending on whether it is public or private, the email may be
  an individual or wider, and associated with a team. You can find details about
  the <a href="https://apisjson.org/schema/apis-contact/">API contact property
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/email.html"
  target="_blank">support emails</a> more via API Evangelist.
message: API contact has email.
given: $.apis.*.contact.*
severity: info
then:
  field: email
  function: falsy
```
## API COULD have a contact. (apis-json-apis-contact-error)
The contact object provides the ability to associate a vCard that represents an individual or any organization entity with common contact information like a name, email, or other reference, providing a standardized way of supporting an API. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/contact.html" target="_blank">support contact</a> more via API Evangelist.

```
description: >-
  The contact object provides the ability to associate a vCard that represents
  an individual or any organization entity with common contact information like
  a name, email, or other reference, providing a standardized way of supporting
  an API. You can find details about the <a
  href="https://apisjson.org/schema/apis-contact/">API contact property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/contact.html"
  target="_blank">support contact</a> more via API Evangelist.
message: API COULD have a contact.
severity: warn
given:
  - $.apis.*
then:
  field: contact
  function: truthy
```
## Contact Could Have FN (apis-json-apis-contact-fn-error)
The purpose of the FN is to specify the formatted text corresponding to the contact name in the vCard for an API. It could be a persons name or wider for a domain, team, or other bounded context, providing the reference needed for support or feedback. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/name.html" target="_blank">support name</a> more via API Evangelist.

```
description: >-
  The purpose of the FN is to specify the formatted text corresponding to the
  contact name in the vCard for an API. It could be a persons name or wider for
  a domain, team, or other bounded context, providing the reference needed for
  support or feedback. You can find details about the <a
  href="https://apisjson.org/schema/apis-contact/">API contact property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/name.html"
  target="_blank">support name</a> more via API Evangelist.
message: Contact Could Have FN
given: $.apis.*.contact.*
severity: error
then:
  field: FN
  function: truthy
```
## Contact Has FN (apis-json-apis-contact-fn-info)
The purpose of the FN is to specify the formatted text corresponding to the contact name in the vCard for an API. It could be a persons name or wider for a domain, team, or other bounded context, providing the reference needed for support or feedback. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/name.html" target="_blank">support name</a> more via API Evangelist.

```
description: >-
  The purpose of the FN is to specify the formatted text corresponding to the
  contact name in the vCard for an API. It could be a persons name or wider for
  a domain, team, or other bounded context, providing the reference needed for
  support or feedback. You can find details about the <a
  href="https://apisjson.org/schema/apis-contact/">API contact property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/name.html"
  target="_blank">support name</a> more via API Evangelist.
message: Contact Has FN
given: $.apis.*.contact.*
severity: info
then:
  field: FN
  function: falsy
```
## Has a Contract (apis-json-apis-contact-info)
The contact object provides the ability to associate a vCard that represents an individual or any organization entity with common contact information like a name, email, or other reference, providing a standardized way of supporting an API. You can find details about the <a href="https://apisjson.org/schema/apis-contact/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/contact.html" target="_blank">support contact</a> more via API Evangelist.

```
description: >-
  The contact object provides the ability to associate a vCard that represents
  an individual or any organization entity with common contact information like
  a name, email, or other reference, providing a standardized way of supporting
  an API. You can find details about the <a
  href="https://apisjson.org/schema/apis-contact/">API contact property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/contact.html"
  target="_blank">support contact</a> more via API Evangelist.
message: Has a Contract
severity: info
given:
  - $.apis.*
then:
  field: contact
  function: falsy
```
## Has a Description (apis-json-apis-description-info)
The description of each API is how you make your first impression on consumers, and is what will likely show in portals, networks, search, and other ways that API consumers discover APIs and onboard with them. Make the description of an API talk about what it does, and the value it brings to consumers, not about the structure and standards used--those can be expressed in other ways. You can find details about the <a href="https://apisjson.org/schema/description/">description property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/descriptions.html" target="_blank">API descriptons</a> more via API Evangelist.

```
description: >-
  The description of each API is how you make your first impression on
  consumers, and is what will likely show in portals, networks, search, and
  other ways that API consumers discover APIs and onboard with them. Make the
  description of an API talk about what it does, and the value it brings to
  consumers, not about the structure and standards used--those can be expressed
  in other ways. You can find details about the <a
  href="https://apisjson.org/schema/description/">description property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/apis/descriptions.html"
  target="_blank">API descriptons</a> more via API Evangelist.
message: Has a Description
given: $.apis.*
severity: info
then:
  field: description
  function: falsy
```
## Has a Human URL (apis-json-apis-humanURL-info)
The human URL for an API provides a link for any business or technical consumer to use when learning more about an API and onboarding with it. In some cases it can be directly to documentation, but ideally each API has its own landing page with a simple and intuitive URL, and has links to all of the properties API consumers will need for an API. You can find details about the <a href="https://apisjson.org/schema/human-url/">humanUrl property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/human-url.html" target="_blank">Human URLs</a> more via API Evangelist.

```
description: >-
  The human URL for an API provides a link for any business or technical
  consumer to use when learning more about an API and onboarding with it. In
  some cases it can be directly to documentation, but ideally each API has its
  own landing page with a simple and intuitive URL, and has links to all of the
  properties API consumers will need for an API. You can find details about the
  <a href="https://apisjson.org/schema/human-url/">humanUrl property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/apis/human-url.html"
  target="_blank">Human URLs</a> more via API Evangelist.
message: Has a Human URL
given: $.apis.*
severity: info
then:
  field: humanURL
  function: falsy
```
## Has an Image (apis-json-apis-image-info)
A dedicated image for each API, providing a visual representation of the resource or capability being made available via an API helps make it more approachable and visually appealing in portals, documentation, and via other content format. Images should be simple, consistent, and should avoid just being company logos and other less precise visual representations. You can find details about the <a href="https://apisjson.org/schema/images/">images property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/images.html" target="_blank">API images</a> more via API Evangelist.

```
description: >-
  A dedicated image for each API, providing a visual representation of the
  resource or capability being made available via an API helps make it more
  approachable and visually appealing in portals, documentation, and via other
  content format. Images should be simple, consistent, and should avoid just
  being company logos and other less precise visual representations. You can
  find details about the <a href="https://apisjson.org/schema/images/">images
  property for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/apis/images.html"
  target="_blank">API images</a> more via API Evangelist.
message: Has an Image
given: $.apis.*
severity: info
then:
  field: image
  function: falsy
```
## Has APIs (apis-json-apis-info)
The APIs property provides the ability to define one or many APIs, as part of a larger collection or contract. What constitutes an API s up to the maintainer of the collection, and will vary depending on what the APIs.json contract is defining between producer and consumer. Depending on the scope of an API the sweet spot for the number of APIs is about 250, but could go up to 300 or 400 when necessary, keeping API definitions serving the purpose of the APIs.json artifact. You can find details about the <a href="https://apisjson.org/schema/apis/">baseUrl property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/apis.html" target="_blank">APIs</a> more via API Evangelist guidance.

```
description: >-
  The APIs property provides the ability to define one or many APIs, as part of
  a larger collection or contract. What constitutes an API s up to the
  maintainer of the collection, and will vary depending on what the APIs.json
  contract is defining between producer and consumer. Depending on the scope of
  an API the sweet spot for the number of APIs is about 250, but could go up to
  300 or 400 when necessary, keeping API definitions serving the purpose of the
  APIs.json artifact. You can find details about the <a
  href="https://apisjson.org/schema/apis/">baseUrl property for APIs.json</a>,
  and explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/apis.html"
  target="_blank">APIs</a> more via API Evangelist guidance.
message: Has APIs
given: $
severity: info
then:
  field: apis
  function: falsy
```
## Has a Name (apis-json-apis-name-info)
The name of your API is one of the most important design decision you can make, and will be one you will have to live with throughout the life of your API. Take the time to make sure the API accurately describes the API, and avoid using common words about the patterns and infrastructure used--keep the name of the API simple, easy to read, and meaningful to the consumer of the API. You can find details about the <a href="https://apisjson.org/schema/name/">name property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/apis/names.html" target="_blank">API names</a> more via API Evangelist guidance.

```
description: >-
  The name of your API is one of the most important design decision you can
  make, and will be one you will have to live with throughout the life of your
  API. Take the time to make sure the API accurately describes the API, and
  avoid using common words about the patterns and infrastructure used--keep the
  name of the API simple, easy to read, and meaningful to the consumer of the
  API. You can find details about the <a
  href="https://apisjson.org/schema/name/">name property for APIs.json</a>, and
  explore <a href="https://guidance.apievangelist.com/guidance/apis/names.html"
  target="_blank">API names</a> more via API Evangelist guidance.
message: Has a Name
given: $.apis.*
severity: info
then:
  field: name
  function: falsy
```
## Has About (apis-json-apis-properties-about-info)
This property ensures provides a reference to an about page, either for the company, organization, or government agency behind an API, or specifically about the domain, team, and the APIs they produce. The goal is to provide more background on who is behind an API for consumers, but also any other stakeholder who may want to know more.  You can find details about the <a href="https://apisjson.org/common/about/">about property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/about.html" target="_blank">about pages</a> more via API Evangelist guidance.

```
description: >-
  This property ensures provides a reference to an about page, either for the
  company, organization, or government agency behind an API, or specifically
  about the domain, team, and the APIs they produce. The goal is to provide more
  background on who is behind an API for consumers, but also any other
  stakeholder who may want to know more.  You can find details about the <a
  href="https://apisjson.org/common/about/">about property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/about.html"
  target="_blank">about pages</a> more via API Evangelist guidance.
message: Has About
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(about|About)\b
```
## Has Authentication (apis-json-apis-properties-authentication-info)
This property ensures that there is a human readable authentication page available that will provide what type of authentication is used and how it can be applied, as well as any services or tooling that API consumers can use to troubleshoot authentication with APIs. You can find details about the <a href="https://apisjson.org/common/authentication/">authentication property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/authentication/overview.html" target="_blank">authentication</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that there is a human readable authentication page
  available that will provide what type of authentication is used and how it can
  be applied, as well as any services or tooling that API consumers can use to
  troubleshoot authentication with APIs. You can find details about the <a
  href="https://apisjson.org/common/authentication/">authentication property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/authentication/overview.html"
  target="_blank">authentication</a> more via API Evangelist guidance.
message: Has Authentication
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(Authentication)\b
```
## Has a Blog (apis-json-apis-properties-blog-info)
This property ensures that an API has a reference to a blog where anyone can find updates and other stories that will help keep API consumers and other stakeholders up to speed on what is happening with an API, and the larger operations. You can find details about the <a href="https://apisjson.org/common/blogs/">blog property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/communications/blogs.html" target="_blank">blogs</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that an API has a reference to a blog where anyone can
  find updates and other stories that will help keep API consumers and other
  stakeholders up to speed on what is happening with an API, and the larger
  operations. You can find details about the <a
  href="https://apisjson.org/common/blogs/">blog property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/communications/blogs.html"
  target="_blank">blogs</a> more via API Evangelist guidance.
message: Has a Blog
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(blog|Blogs)\b
```
## Has a Blog Feed (apis-json-apis-properties-blog-feed-info)
This property ensures that blogs in support of APIs have an Atom or RSS feed of posts, allowing for the syndication of updates and information around individual APIs and the operations around them. Feeds are a great way to augment APIs which are very distributed in nature, with information feeds that keep API consumers up to date. You can find details about the <a href="https://apisjson.org/common/blog-feeds/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/communication/blog-feeds.html" target="_blank">API Unique Identifiers</a> more via API Evangelist.

```
description: >-
  This property ensures that blogs in support of APIs have an Atom or RSS feed
  of posts, allowing for the syndication of updates and information around
  individual APIs and the operations around them. Feeds are a great way to
  augment APIs which are very distributed in nature, with information feeds that
  keep API consumers up to date. You can find details about the <a
  href="https://apisjson.org/common/blog-feeds/">aid property for APIs.json</a>,
  and explore <a
  href="https://guidance.apievangelist.com/guidance/communication/blog-feeds.html"
  target="_blank">API Unique Identifiers</a> more via API Evangelist.
message: Has a Blog Feed
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(blog-feed|BlogFeeds)\b
```
## Has Change Log (apis-json-apis-properties-change-log-info)
This property ensures that than an individual API or API operations possesses a change log that catalogs all the changes that have occurred in a recent time frame, with historical and version information available if possible. Change log helps inform API consumers, but also keep API producers grounded in the recent past. You can find details about the <a href="https://apisjson.org/common/change-log/">change log property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/change-log.html" target="_blank">change logs</a> more via API Evangelist.

```
description: >-
  This property ensures that than an individual API or API operations possesses
  a change log that catalogs all the changes that have occurred in a recent time
  frame, with historical and version information available if possible. Change
  log helps inform API consumers, but also keep API producers grounded in the
  recent past. You can find details about the <a
  href="https://apisjson.org/common/change-log/">change log property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/change-log.html"
  target="_blank">change logs</a> more via API Evangelist.
message: Has Change Log
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-change-log|change-log|Change Log|Changelog|ChangeLog)\b
```
## Has an API Comparison (apis-json-apis-properties-compare-info)
This property ensures that an API has the ability to compare two different versions of an API and see what the difference are between them. The ability to compare iterations of an API help develop more awareness amongst both the producers and consumers of an API. You can find details about the <a href="https://apisjson.org/common/compare/">compare property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/compare.html" target="_blank">compare approaches</a> more via API Evangelist.

```
description: >-
  This property ensures that an API has the ability to compare two different
  versions of an API and see what the difference are between them. The ability
  to compare iterations of an API help develop more awareness amongst both the
  producers and consumers of an API. You can find details about the <a
  href="https://apisjson.org/common/compare/">compare property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/compare.html"
  target="_blank">compare approaches</a> more via API Evangelist.
message: Has an API Comparison
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(compare|Compare)\b
```
## Has Deprecation Policy (apis-json-apis-properties-deprecation-policy-info)
This property ensures that an API has a deprecation policy shared as part of the contract, communicating what the lifespan of APIs are, each individual version, as well as communication around the deprecation of APIs. A deprecation policy adds another building block into the change management toolbox, helping better set expectations with everyone involved with APIs. You can find details about the <a href="https://apisjson.org/common/deprecation/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/deprecation-policies.html" target="_blank">API Unique Identifiers</a> more via API Evangelist.

```
description: >-
  This property ensures that an API has a deprecation policy shared as part of
  the contract, communicating what the lifespan of APIs are, each individual
  version, as well as communication around the deprecation of APIs. A
  deprecation policy adds another building block into the change management
  toolbox, helping better set expectations with everyone involved with APIs. You
  can find details about the <a
  href="https://apisjson.org/common/deprecation/">aid property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/deprecation-policies.html"
  target="_blank">API Unique Identifiers</a> more via API Evangelist.
message: Has Deprecation Policy
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: >-
        \b(api-deprecation-policy|deprecation-policy|Deprecation|Deprecation
        Policy|DeprecationPolicy)\b
```
## Has Documentation (apis-json-apis-properties-documentation-info)
This property ensures that there is documentation published for an API, and API consumers will have a set of human-readable instructions for onboarding and integrating with HTTP APIs in their applications. Ideally the documentation is published using an OpenAPI definition, helping automate the delivering of documentation as part of the regular build process. You can find details about the <a href="https://apisjson.org/common/documentation/">documentation property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/documentation/overview.html" target="_blank">API documentation</a> more via API Evangelist.

```
description: >-
  This property ensures that there is documentation published for an API, and
  API consumers will have a set of human-readable instructions for onboarding
  and integrating with HTTP APIs in their applications. Ideally the
  documentation is published using an OpenAPI definition, helping automate the
  delivering of documentation as part of the regular build process. You can find
  details about the <a
  href="https://apisjson.org/common/documentation/">documentation property types
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/documentation/overview.html"
  target="_blank">API documentation</a> more via API Evangelist.
message: Has Documentation
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(documentation|Documentation)\b
```
## Has a Production Environment (apis-json-apis-properties-environments-production-info)
This property ensures that there is a production environment available for an API, providing base URL, tokens, keys, and other key / value pairs that are needed to integrate with an API. Make sure attention is paid towards security and using a secure vault and service to keep all secrets secured. You can find details about the <a href="https://apisjson.org/common/environments/">environments for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/environments/productions.html" target="_blank">production environments</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that there is a production environment available for an
  API, providing base URL, tokens, keys, and other key / value pairs that are
  needed to integrate with an API. Make sure attention is paid towards security
  and using a secure vault and service to keep all secrets secured. You can find
  details about the <a
  href="https://apisjson.org/common/environments/">environments for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/environments/productions.html"
  target="_blank">production environments</a> more via API Evangelist guidance.
message: Has a Production Environment
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(ProductionEnvironment)\b
```
## Has a Stage Environment (apis-json-apis-properties-environments-staging-info)
This property ensures that there is a staging environment available for an API, providing base URL, tokens, keys, and other key / value pairs that are needed to integrate with an API. Make sure attention is paid towards security and using a secure vault and service to keep all secrets secured. You can find details about the <a href="https://apisjson.org/common/environments/">environments for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/environments/sandbox.html" target="_blank">sandbox environments</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that there is a staging environment available for an
  API, providing base URL, tokens, keys, and other key / value pairs that are
  needed to integrate with an API. Make sure attention is paid towards security
  and using a secure vault and service to keep all secrets secured. You can find
  details about the <a
  href="https://apisjson.org/common/environments/">environments for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/environments/sandbox.html"
  target="_blank">sandbox environments</a> more via API Evangelist guidance.
message: Has a Stage Environment
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(StagingEnvironment)\b
```
## Has Discussion Forum (apis-json-apis-properties-forum-info)
This property ensures that there is a link to a discussion forum, providing a way for consumers and producers to engage and support either other throughout the lifecycle. This is a great way for making support self-service and community-driven, while ensuring everyone is taken care of. You can find details about the <a href="https://apisjson.org/common/forum/">forum property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/forums.html" target="_blank">discussion forums</a> more via API Evangelist.

```
description: >-
  This property ensures that there is a link to a discussion forum, providing a
  way for consumers and producers to engage and support either other throughout
  the lifecycle. This is a great way for making support self-service and
  community-driven, while ensuring everyone is taken care of. You can find
  details about the <a href="https://apisjson.org/common/forum/">forum property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/forums.html"
  target="_blank">discussion forums</a> more via API Evangelist.
message: Has Discussion Forum
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(Forums|Forums|Discussions)\b
```
## Has Getting Started (apis-json-apis-properties-getting-started-info)
This property ensures that there is a getting started link available, providing a reference for API consumers to get started with an API is as few steps as possible. Getting started often refer to documentation, authentication, SDKs, and other resources developers commonly need when onboarding. You can find details about the <a href="https://apisjson.org/common/getting-started/">getting started property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/onboarding/getting-started.html" target="_blank">getting started resources</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a getting started link available,
  providing a reference for API consumers to get started with an API is as few
  steps as possible. Getting started often refer to documentation,
  authentication, SDKs, and other resources developers commonly need when
  onboarding. You can find details about the <a
  href="https://apisjson.org/common/getting-started/">getting started property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/onboarding/getting-started.html"
  target="_blank">getting started resources</a> via API Evangelist guidance.
message: Has Getting Started
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(GettingStarted)\b
```
## Has a GitHub Organization (apis-json-apis-properties-github-organization-info)
This property ensures that an API is associated with GitHub organization, providing the URL to where you can engage with the operations surrounding an API. Having a dedicated GitHub Organization for teams producing APIs helps establish a common and well-known place where teams can find out what is happening with an API. You can find details about the <a href="https://apisjson.org/common/github-organizations/">GitHub Organization property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/workspaces/github-organizations.html" target="_blank">GitHub Organization</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that an API is associated with GitHub organization,
  providing the URL to where you can engage with the operations surrounding an
  API. Having a dedicated GitHub Organization for teams producing APIs helps
  establish a common and well-known place where teams can find out what is
  happening with an API. You can find details about the <a
  href="https://apisjson.org/common/github-organizations/">GitHub Organization
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/workspaces/github-organizations.html"
  target="_blank">GitHub Organization</a> more via API Evangelist guidance.
message: Has a GitHub Organization
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(github-organization|GitHubOrganization)\b
```
## Has a GitHub Repository (apis-json-apis-properties-github-repository-info)
This property ensures that an API possess a reference to a dedicated GitHub repository that is used to manage the Open, but also possible server and client code. A GitHub repository provides a single source of truth for the API contract and code, but also the conversation that occurs across the API lifecycle. You can find details about the <a href="https://apisjson.org/common/github-repositories/">GitHub repositories property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/source-control/github.html" target="_blank">GitHub repositories</a> more via API Evangelist.

```
description: >-
  This property ensures that an API possess a reference to a dedicated GitHub
  repository that is used to manage the Open, but also possible server and
  client code. A GitHub repository provides a single source of truth for the API
  contract and code, but also the conversation that occurs across the API
  lifecycle. You can find details about the <a
  href="https://apisjson.org/common/github-repositories/">GitHub repositories
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/source-control/github.html"
  target="_blank">GitHub repositories</a> more via API Evangelist.
message: Has a GitHub Repository
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(github-repository|GitHubRepository)\b
```
## Has a GitHub Action (apis-json-apis-properties-github-action-info)
This property ensures that a GitHub Actions CI/CD pipeline is available for an API, providing a link to the pipeline YAML artifact, which can be used to automate and govern the API as part of the build process. GitHub Actions provide a proven way to automate each stage of the API lifecycle, weaving API governance into each stage of the lifecycle using policies and rules. You can find details about the <a href="https://apisjson.org/schema/aid/">GitHub Actions property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/pipelines/github-actions.html" target="_blank">GitHub Actions</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that a GitHub Actions CI/CD pipeline is available for an
  API, providing a link to the pipeline YAML artifact, which can be used to
  automate and govern the API as part of the build process. GitHub Actions
  provide a proven way to automate each stage of the API lifecycle, weaving API
  governance into each stage of the lifecycle using policies and rules. You can
  find details about the <a href="https://apisjson.org/schema/aid/">GitHub
  Actions property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/pipelines/github-actions.html"
  target="_blank">GitHub Actions</a> more via API Evangelist guidance.
message: Has a GitHub Action
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(github-actions|GitHubActions)\b
```
## Has Insomnia Collection (apis-json-apis-properties-insomnia-collection-info)
This property defines an Insomnia collection available for each API, providing executable artifacts that can be used in the Insomnia client for making calls, and executing automation workflows. Insomnia Collections provide a great way to produce derivatives of an API that can be used to automate using an API, as well as the operations around it. You can find details about the <a href="https://apisjson.org/community/insomnia-collections/">Insomnnia Collection property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/contracts/insomnia-collections.html" target="_blank">Insomnia Collections</a> more via API Evangelist guidance.

```
description: >-
  This property defines an Insomnia collection available for each API, providing
  executable artifacts that can be used in the Insomnia client for making calls,
  and executing automation workflows. Insomnia Collections provide a great way
  to produce derivatives of an API that can be used to automate using an API, as
  well as the operations around it. You can find details about the <a
  href="https://apisjson.org/community/insomnia-collections/">Insomnnia
  Collection property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/contracts/insomnia-collections.html"
  target="_blank">Insomnia Collections</a> more via API Evangelist guidance.
message: Has Insomnia Collection
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(RunInInsomnia)\b
```
## Has Interface License (apis-json-apis-properties-license-info)
This property ensures that an API Commons interface license exists for an API, providing a machine-readable reference for an API, as well as data, backend, and front-end code. An interface license applies copyright to the API, code licensing to backend and frontend of an API, and data licenses for the data being made available. You can find details about the <a href="https://apisjson.org/common/interface-license/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/legal/interface-license.html" target="_blank">API Unique Identifiers</a> more via API Evangelist.

```
description: >-
  This property ensures that an API Commons interface license exists for an API,
  providing a machine-readable reference for an API, as well as data, backend,
  and front-end code. An interface license applies copyright to the API, code
  licensing to backend and frontend of an API, and data licenses for the data
  being made available. You can find details about the <a
  href="https://apisjson.org/common/interface-license/">aid property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/legal/interface-license.html"
  target="_blank">API Unique Identifiers</a> more via API Evangelist.
message: Has Interface License
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-license|License|license|InterfaceLicense)\b
```
## Has An OpenAPI (apis-json-apis-properties-openapi-info)
This property ensures that there is an OpenAPI present for an API, providing the technical contract that describes the surface area of an API. While the OpenAPI will be used for documentation, code generation, and other areas, this makes sure there is a direct link to the OpenAPI for wider use. You can find details about the <a href="https://apisjson.org/community/openapi/">OpenAPI property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/contracts/openapi.html" target="_blank">OpenAPI</a> more via API Evangelist guidance.

```
description: >-
  This property ensures that there is an OpenAPI present for an API, providing
  the technical contract that describes the surface area of an API. While the
  OpenAPI will be used for documentation, code generation, and other areas, this
  makes sure there is a direct link to the OpenAPI for wider use. You can find
  details about the <a href="https://apisjson.org/community/openapi/">OpenAPI
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/contracts/openapi.html"
  target="_blank">OpenAPI</a> more via API Evangelist guidance.
message: Has An OpenAPI
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(openapi|OpenAPI)\b
```
## Has API Performance (apis-json-apis-properties-performance-info)
This property ensures that an API has performance testing in place, providing a URL to the performance testing, dashboard, or other resource. Linking to performance testing is the first step towards actually publishing the results of performance tests as part of the contract. You can find details about the <a href="https://apisjson.org/common/performance/">performance property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/testing/performance.html" target="_blank">performance testing</a>  via API Evangelist guidance.

```
description: >-
  This property ensures that an API has performance testing in place, providing
  a URL to the performance testing, dashboard, or other resource. Linking to
  performance testing is the first step towards actually publishing the results
  of performance tests as part of the contract. You can find details about the
  <a href="https://apisjson.org/common/performance/">performance property type
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/testing/performance.html"
  target="_blank">performance testing</a>  via API Evangelist guidance.
message: Has API Performance
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(Performance|PerformanceTesting)\b
```
## Has API Plans (apis-json-apis-properties-plans-info)
This property provides a link to the dedicated plans page that applies to an API, providing information about access tiers, rate limits, and features available for an API as part of a wider API business plan. You can find details about the <a href="https://apisjson.org/common/plans/">plans property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/plans/overview.html" target="_blank">plans</a> via API Evangelist guidance.

```
description: >-
  This property provides a link to the dedicated plans page that applies to an
  API, providing information about access tiers, rate limits, and features
  available for an API as part of a wider API business plan. You can find
  details about the <a href="https://apisjson.org/common/plans/">plans property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/plans/overview.html"
  target="_blank">plans</a> via API Evangelist guidance.
message: Has API Plans
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-plans|Plans)\b
```
## Has API Governance Policies (apis-json-apis-properties-policies-info)
This property ensures there is a governance policies reference as part of an API contract, usually a common property pointing to a centralized set of policies that get applied. Policies are used to group governance rules and associate them with the business reasoning behind why rules should be applied. You can find details about the <a href="https://apisjson.org/common/policies/">policies property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/policies.html" target="_blank">governance policies</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a governance policies reference as part of an
  API contract, usually a common property pointing to a centralized set of
  policies that get applied. Policies are used to group governance rules and
  associate them with the business reasoning behind why rules should be applied.
  You can find details about the <a
  href="https://apisjson.org/common/policies/">policies property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/policies.html"
  target="_blank">governance policies</a> via API Evangelist guidance.
message: Has API Governance Policies
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-policies|Policies)\b
```
## Has Developer Portal (apis-json-apis-properties-portal-info)
This property ensures there a developer portal associated with an API and that you can find a landing page for the API, documentation, SDKs, and other resources. The API portal should be the front door for the API, providing a single place consumers can find whatever they need. You can find details about the <a href="https://apisjson.org/common/portas/">portals property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/discovery/portals.html" target="_blank">API portals</a> via API Evangelist guidance.

```
description: >-
  This property ensures there a developer portal associated with an API and that
  you can find a landing page for the API, documentation, SDKs, and other
  resources. The API portal should be the front door for the API, providing a
  single place consumers can find whatever they need. You can find details about
  the <a href="https://apisjson.org/common/portas/">portals property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/discovery/portals.html"
  target="_blank">API portals</a> via API Evangelist guidance.
message: Has Developer Portal
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: >-
        \b(api-developer-portal|developer-portal|portal|Portal|Portals|DeveloperPortal)\b
```
## Has a Postman Collection (apis-json-apis-properties-postman-collection-info)
This property ensures that an API has at least one Postman Collection associated with it, providing automation, tests, and other executable derivatives of an APIs OpenAPI. Collections are a great way to define, organize, and execute specific API capabilities and automate API operations. You can find details about the <a href="https://apisjson.org/community/postman-collections/">Postman Collections property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/contracts/postman-collections.html" target="_blank">Postman Collections</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has at least one Postman Collection
  associated with it, providing automation, tests, and other executable
  derivatives of an APIs OpenAPI. Collections are a great way to define,
  organize, and execute specific API capabilities and automate API operations.
  You can find details about the <a
  href="https://apisjson.org/community/postman-collections/">Postman Collections
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/contracts/postman-collections.html"
  target="_blank">Postman Collections</a> via API Evangelist guidance.
message: Has a Postman Collection
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(PostmanCollection)\b
```
## Has Public Postman Workspace (apis-json-apis-properties-postman-public-workspace-info)
This property ensures that an API is associated with a Postman Workspace, providing a single location that API producers and/or API consumers can engage around an API. Postman Workspaces provide a collaborative way to manage an API, meeting developers where they already work as part of their API work. You can find details about the <a href="https://apisjson.org/community/postman-workspaces/">Postman Workspaces property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/workspaces/postman-workspaces.html" target="_blank">Postman Workspaces</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API is associated with a Postman Workspace,
  providing a single location that API producers and/or API consumers can engage
  around an API. Postman Workspaces provide a collaborative way to manage an
  API, meeting developers where they already work as part of their API work. You
  can find details about the <a
  href="https://apisjson.org/community/postman-workspaces/">Postman Workspaces
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/workspaces/postman-workspaces.html"
  target="_blank">Postman Workspaces</a> via API Evangelist guidance.
message: Has Public Postman Workspace
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(postman-public-workspace|PostmanPublicWorkspace|PostmanWorkspace)\b
```
## Has Pricing (apis-json-apis-properties-pricing-info)
This property provides a link to a pricing page that applies to an API, providing a breakdown of the costs associated with using an API. Even if an API is free it should have a pricing page that provides an overview of what is available for free from an API. You can find details about the <a href="https://apisjson.org/common/pricing/">pricing property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/plans/pricing.html" target="_blank">API pricing</a> via API Evangelist guidance.

```
description: >-
  This property provides a link to a pricing page that applies to an API,
  providing a breakdown of the costs associated with using an API. Even if an
  API is free it should have a pricing page that provides an overview of what is
  available for free from an API. You can find details about the <a
  href="https://apisjson.org/common/pricing/">pricing property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/plans/pricing.html"
  target="_blank">API pricing</a> via API Evangelist guidance.
message: Has Pricing
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(Pricing)\b
```
## Has an API Privacy Policy (apis-json-apis-properties-privacy-policy-info)
This property provides a link to the privacy policy for an API, providing the legal details of how privacy is approached for each API. The privacy policy page may be a general company or platform privacy policy, but can also be a specific one for APIs. You can find details about the <a href="https://apisjson.org/common/privacy-policy/">privacy policy property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/legal/privacy-policy.html" target="_blank">privacy policies</a> via API Evangelist guidance.

```
description: >-
  This property provides a link to the privacy policy for an API, providing the
  legal details of how privacy is approached for each API. The privacy policy
  page may be a general company or platform privacy policy, but can also be a
  specific one for APIs. You can find details about the <a
  href="https://apisjson.org/common/privacy-policy/">privacy policy property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/legal/privacy-policy.html"
  target="_blank">privacy policies</a> via API Evangelist guidance.
message: Has an API Privacy Policy
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: >-
        \b(api-privacy-policy|privacy-policy|Privacy|Privacy
        Policy|PrivacyPolicy)\b
```
## Has an API Terms of Services (apis-json-apis-properties-rate-limits-info)
This property ensures there is an API rate limits reference associated with API, ensuring the rate limits applied to an API are clearly communicated. Rate limits may overlap with plans and pricing pages, but depending on the API, there may be dedicated rate limits referenced. You can find details about the <a href="https://apisjson.org/common/rate-limits/">rate limits property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/plans/rate-limits.html" target="_blank">rate limits</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is an API rate limits reference associated with
  API, ensuring the rate limits applied to an API are clearly communicated. Rate
  limits may overlap with plans and pricing pages, but depending on the API,
  there may be dedicated rate limits referenced. You can find details about the
  <a href="https://apisjson.org/common/rate-limits/">rate limits property type
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/plans/rate-limits.html"
  target="_blank">rate limits</a> via API Evangelist guidance.
message: Has an API Terms of Services
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(rate-limits|RateLimits|Rate Limits)\b
```
## Has a Road Map (apis-json-apis-properties-road-map-info)
This property ensures there is a reference to the road map for an API or for the entire API operations within domain, line of business, or teams. The road map provides information about what is being planning for the short-term or long-term future of an API. You can find details about the <a href="https://apisjson.org/common/road-map/">road map property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/road-map.html" target="_blank">road map</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a reference to the road map for an API or for
  the entire API operations within domain, line of business, or teams. The road
  map provides information about what is being planning for the short-term or
  long-term future of an API. You can find details about the <a
  href="https://apisjson.org/common/road-map/">road map property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/road-map.html"
  target="_blank">road map</a> via API Evangelist guidance.
message: Has a Road Map
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-road-map|road-map|Roadmap|Road Map|RoadMap)\b
```
## Has Linting Rules (apis-json-apis-properties-rules-info)
This property ensures that an API has governance rules applied, usually as part of a central set of governance rules, defined by policy, or stages of the API lifecycle. Rules are usually centralized, but you can also augment with rules designed specifically for an API. You can find details about the <a href="https://apisjson.org/community/spectral/">Spectral rules property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/api-rules.html" target="_blank">api governance rules</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has governance rules applied, usually as
  part of a central set of governance rules, defined by policy, or stages of the
  API lifecycle. Rules are usually centralized, but you can also augment with
  rules designed specifically for an API. You can find details about the <a
  href="https://apisjson.org/community/spectral/">Spectral rules property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/api-rules.html"
  target="_blank">api governance rules</a> via API Evangelist guidance.
message: Has Linting Rules
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-rules|OpenApiRules)\b
```
## Has Operational Rules (apis-json-apis-properties-apis-json-rules-info)
This property ensures that an API has operational level rules for APIs.json defined, applying governance to everything surrounding an API. APIs.json operation rules are usually centralized as part of a public, or internal domain, team, or other bounded context. You can find details about the <a href="https://apisjson.org/common/rules/">operational rules property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/operational-rules.html" target="_blank">operational governance rules</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has operational level rules for APIs.json
  defined, applying governance to everything surrounding an API. APIs.json
  operation rules are usually centralized as part of a public, or internal
  domain, team, or other bounded context. You can find details about the <a
  href="https://apisjson.org/common/rules/">operational rules property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/operational-rules.html"
  target="_blank">operational governance rules</a> via API Evangelist guidance.
message: Has Operational Rules
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(operational-rules|OperationalRules)\b
```
## Has API Rules (apis-json-apis-properties-openapi-rules-info)
This property ensures that an OpenAPI has support governance rules, that can be applied during design time via editors, development time via IDE, and run-time via CI/CD pipelines. OpenAPI rules are usually centrally defined, but can also be defined specifically for an API. You can find details about the <a href="https://apisjson.org/common/openapi-rules/">OpenAPI rules property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/openapi-rules.html" target="_blank">OpenAPI rules</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an OpenAPI has support governance rules, that can
  be applied during design time via editors, development time via IDE, and
  run-time via CI/CD pipelines. OpenAPI rules are usually centrally defined, but
  can also be defined specifically for an API. You can find details about the <a
  href="https://apisjson.org/common/openapi-rules/">OpenAPI rules property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/openapi-rules.html"
  target="_blank">OpenAPI rules</a> via API Evangelist guidance.
message: Has API Rules
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-rules|ApiRules)\b
```
## Has an API Lifecycle (apis-json-apis-properties-lifecycle-info)
This property makes sure there is an API lifecycle schema defining all of the stages of a lifecycle and which policies get applied at each stage of the API lifecycle. A lifecycle schema is usually centrally defined, but then applied to each individual API to track the evolution of each version. You can find details about the <a href="https://apisjson.org/common/lifecycle/">lifecycle property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/lifecycle.html" target="_blank">API lifecycle</a> via API Evangelist guidance.

```
description: >-
  This property makes sure there is an API lifecycle schema defining all of the
  stages of a lifecycle and which policies get applied at each stage of the API
  lifecycle. A lifecycle schema is usually centrally defined, but then applied
  to each individual API to track the evolution of each version. You can find
  details about the <a href="https://apisjson.org/common/lifecycle/">lifecycle
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/lifecycle.html"
  target="_blank">API lifecycle</a> via API Evangelist guidance.
message: Has an API Lifecycle
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(lifecycle|Lifecycle)\b
```
## Has Vocabulary (apis-json-apis-properties-vocabulary-info)
This property ensures that there is a centralized vocabulary in use for guiding the creation and usage of tags, path segments, and other metadata associated with an APIs.json, OpenAPI, and other artifacts. A vocabulary provides a common set of key words and phrases that can be applied by teams, helping improve organization and discovery of APIs. You can find details about the <a href="https://apisjson.org/common/vocabulary/">vocabulary property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/governance/vocabulary.html" target="_blank">vocabulary</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a centralized vocabulary in use for
  guiding the creation and usage of tags, path segments, and other metadata
  associated with an APIs.json, OpenAPI, and other artifacts. A vocabulary
  provides a common set of key words and phrases that can be applied by teams,
  helping improve organization and discovery of APIs. You can find details about
  the <a href="https://apisjson.org/common/vocabulary/">vocabulary property type
  for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/governance/vocabulary.html"
  target="_blank">vocabulary</a> via API Evangelist guidance.
message: Has Vocabulary
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(vocabulary|vocabularies|Vocabulary|Vocabularies)\b
```
## Has Go SDK (apis-json-apis-properties-sdk-go-info)
This property ensures that there is a Go SDK available for an API, making it easier for Go developers to integrate an API into their applications. You can find details about the <a href="https://apisjson.org/common/sdk/">sdk property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/sdks/go.html" target="_blank">Go SDKs</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a Go SDK available for an API, making it
  easier for Go developers to integrate an API into their applications. You can
  find details about the <a href="https://apisjson.org/common/sdk/">sdk property
  types for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/sdks/go.html"
  target="_blank">Go SDKs</a> via API Evangelist guidance.
message: Has Go SDK
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-sdk-go)\b
```
## Has SDK (apis-json-apis-properties-sdk-info)
This property ensures that there is an SDK available for an API, making it easier for developers to integrate an API into their applications. You can find details about the <a href="https://apisjson.org/common/sdk/">SDK property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/sdks/overview.html" target="_blank">SDKs</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is an SDK available for an API, making it
  easier for developers to integrate an API into their applications. You can
  find details about the <a href="https://apisjson.org/common/sdk/">SDK property
  types for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/sdks/overview.html"
  target="_blank">SDKs</a> via API Evangelist guidance.
message: Has SDK
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(sdk|sdks|SDKs)\b
```
## Has Java SDK (apis-json-apis-properties-sdk-java-info)
This property ensures that there is a Java SDK available for an API, making it easier for Java developers to integrate an API into their applications. You can find details about the <a href="https://apisjson.org/common/sdk/">sdk property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/sdks/java.html" target="_blank">Java SDKs</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a Java SDK available for an API, making it
  easier for Java developers to integrate an API into their applications. You
  can find details about the <a href="https://apisjson.org/common/sdk/">sdk
  property types for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/sdks/java.html"
  target="_blank">Java SDKs</a> via API Evangelist guidance.
message: Has Java SDK
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-sdk-java)\b
```
## Has Node SDK (apis-json-apis-properties-sdk-node-info)
This property ensures that there is a Node SDK available for an API, making it easier for Node developers to integrate an API into their applications. You can find details about the <a href="https://apisjson.org/common/sdk/">sdk property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/sdks/node.html" target="_blank">Node SDKs</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a Node SDK available for an API, making it
  easier for Node developers to integrate an API into their applications. You
  can find details about the <a href="https://apisjson.org/common/sdk/">sdk
  property types for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/sdks/node.html"
  target="_blank">Node SDKs</a> via API Evangelist guidance.
message: Has Node SDK
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-sdk-node)\b
```
## Has Python SDK (apis-json-apis-properties-sdk-python-info)
This property ensures that there is a Python SDK available for an API, making it easier for Python developers to integrate an API into their applications. You can find details about the <a href="https://apisjson.org/common/sdk/">sdk property types for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/sdks/python.html" target="_blank">Python SDKs</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a Python SDK available for an API, making
  it easier for Python developers to integrate an API into their applications.
  You can find details about the <a href="https://apisjson.org/common/sdk/">sdk
  property types for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/sdks/python.html"
  target="_blank">Python SDKs</a> via API Evangelist guidance.
message: Has Python SDK
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(api-sdk-python)\b
```
## Has Security Path (apis-json-apis-properties-security-info)
This property ensures there is a URL to the security page, providing details about how security is handled for an API. Security pages can start by echoing authentication and authorization technology, but should go further and include OWASP, and other common approaches to security HTTP APIs. You can find details about the <a href="https://apisjson.org/common/security/">security property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/security/overview.html" target="_blank">API security</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a URL to the security page, providing details
  about how security is handled for an API. Security pages can start by echoing
  authentication and authorization technology, but should go further and include
  OWASP, and other common approaches to security HTTP APIs. You can find details
  about the <a href="https://apisjson.org/common/security/">security property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/security/overview.html"
  target="_blank">API security</a> via API Evangelist guidance.
message: Has Security Path
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(Security|SecurityTesting)\b
```
## Has a Sign Up (apis-json-apis-properties-signup-info)
This property ensures there is a link to where you sign up for an API, making sure API consumers can access in a single click. Sign-up is usually to a registration page for humans to sign-in, but there are also more automated ways of making this happen. You can find details about the <a href="https://apisjson.org/common/signup/">sign up property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/onboarding/signup.html" target="_blank">API sign up</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a link to where you sign up for an API, making
  sure API consumers can access in a single click. Sign-up is usually to a
  registration page for humans to sign-in, but there are also more automated
  ways of making this happen. You can find details about the <a
  href="https://apisjson.org/common/signup/">sign up property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/onboarding/signup.html"
  target="_blank">API sign up</a> via API Evangelist guidance.
message: Has a Sign Up
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(X-signup|signup|Sign Up|SignUp)\b
```
## Has a Status Page (apis-json-apis-properties-status-info)
This property ensures that there is a status page available for each API, providing the uptime status for any given moment, as well as historical data. The status page URL is the starting point for communicating status, with eventually publishing uptime data as part of API contract. You can find details about the <a href="https://apisjson.org/community/status/">status property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/monitoring/status.html" target="_blank">API status monitoring</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a status page available for each API,
  providing the uptime status for any given moment, as well as historical data.
  The status page URL is the starting point for communicating status, with
  eventually publishing uptime data as part of API contract. You can find
  details about the <a href="https://apisjson.org/community/status/">status
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/monitoring/status.html"
  target="_blank">API status monitoring</a> via API Evangelist guidance.
message: Has a Status Page
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(x-status|status|Status|StatusPage)\b
```
## Has Support Page (apis-json-apis-properties-support-support-info)
This property ensures that there is a support page available for an API, providing direct and in-direct support opportunities for each API or for entire API platform. Support can be a mix of email, issues, ticketing, forums, and other types, with a single page to help consumers find what they are looking for. You can find details about the <a href="https://apisjson.org/common/support/">support property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/overview.html" target="_blank">API support</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a support page available for an API,
  providing direct and in-direct support opportunities for each API or for
  entire API platform. Support can be a mix of email, issues, ticketing, forums,
  and other types, with a single page to help consumers find what they are
  looking for. You can find details about the <a
  href="https://apisjson.org/common/support/">support property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/overview.html"
  target="_blank">API support</a> via API Evangelist guidance.
message: Has Support Page
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(support|Support)\b
```
## Has Support Email (apis-json-apis-properties-support-email-info)
This property ensures that an API has email support, providing a valid email address that can be used to get API support. Ideally this is a general email rather than a single person, but in some cases an individual email is required. You can find details about the <a href="https://apisjson.org/community/email/">email property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/email.html" target="_blank">email support</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has email support, providing a valid email
  address that can be used to get API support. Ideally this is a general email
  rather than a single person, but in some cases an individual email is
  required. You can find details about the <a
  href="https://apisjson.org/community/email/">email property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/email.html"
  target="_blank">email support</a> via API Evangelist guidance.
message: Has Support Email
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(support-email|SupportEmail)\b
```
## Has Support Issues URL (apis-json-apis-properties-support-issues-info)
This property ensures that there are Git issues available to support an API, using the issues capability of GitHub, GitLab, or Bitbucket to support API consumers. It is common to set up labels and templates to support different tracks of support available for consumers. You can find details about the <a href="https://apisjson.org/common/issues/">issues property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/issues.html" target="_blank">issues</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there are Git issues available to support an API,
  using the issues capability of GitHub, GitLab, or Bitbucket to support API
  consumers. It is common to set up labels and templates to support different
  tracks of support available for consumers. You can find details about the <a
  href="https://apisjson.org/common/issues/">issues property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/issues.html"
  target="_blank">issues</a> via API Evangelist guidance.
message: Has Support Issues URL
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(SupportIssues|SupportGitHubIssues)\b
```
## Has Feedback Email (apis-json-apis-properties-feedback-email-info)
This property ensures that there is an email available for API consumers to provide feedback. Having a dedicated email channel for feedback helps encourage feedback on APIs outside of problems and support issues. You can find details about the <a href="https://apisjson.org/common/feedback-email/">email feedback property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/feedback/email.html" target="_blank">feedback email</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is an email available for API consumers to
  provide feedback. Having a dedicated email channel for feedback helps
  encourage feedback on APIs outside of problems and support issues. You can
  find details about the <a
  href="https://apisjson.org/common/feedback-email/">email feedback property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/feedback/email.html"
  target="_blank">feedback email</a> via API Evangelist guidance.
message: Has Feedback Email
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(feedback-email|FeedbackEmail)\b
```
## Has Feedback Issues URL (apis-json-apis-properties-feedback-issues-info)
This property ensures there is a URL to Git issues specifically for providing feedback. Having a dedicated channel via issues helps encourage consumers to leave feedback, widening how Git issues are used as a feedback loop. You can find details about the <a href="https://apisjson.org/common/feedback-issues/">feedback issues property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/feedback/issues.html" target="_blank">feedback issues</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a URL to Git issues specifically for providing
  feedback. Having a dedicated channel via issues helps encourage consumers to
  leave feedback, widening how Git issues are used as a feedback loop. You can
  find details about the <a
  href="https://apisjson.org/common/feedback-issues/">feedback issues property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/feedback/issues.html"
  target="_blank">feedback issues</a> via API Evangelist guidance.
message: Has Feedback Issues URL
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(FeedbackIssues|FeedbackGitHubIssues)\b
```
## Has Questions Issues URL (apis-json-apis-properties-questions-issues-info)
This property ensures that an API has a dedicated link to Git issues for asking questions. Having this property separates out common questions from problems and other feedback, making it well known to consumers they are welcome to just ask questions. You can find details about the <a href="https://apisjson.org/common/feedack-issues/">feedback issues property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/feedback/issues.html" target="_blank">feedback issues</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has a dedicated link to Git issues for
  asking questions. Having this property separates out common questions from
  problems and other feedback, making it well known to consumers they are
  welcome to just ask questions. You can find details about the <a
  href="https://apisjson.org/common/feedack-issues/">feedback issues property
  type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/feedback/issues.html"
  target="_blank">feedback issues</a> via API Evangelist guidance.
message: Has Questions Issues URL
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(QuestionsIssues|QuestionsGitHubIssues)\b
```
## Has an API Terms of Service (apis-json-apis-properties-terms-of-service-info)
This property ensures that an API has a reference to a terms of service, covering the legal side of using an API. The terms of service could apply to all of operations, or be specific to an individual API. You can find details about the <a href="https://apisjson.org/common/terms-of-service/">terms of service property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/legal/terms-of-service.html" target="_blank">terms of service</a> via API Evangelist guidance.

```
description: >-
  This property ensures that an API has a reference to a terms of service,
  covering the legal side of using an API. The terms of service could apply to
  all of operations, or be specific to an individual API. You can find details
  about the <a href="https://apisjson.org/common/terms-of-service/">terms of
  service property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/legal/terms-of-service.html"
  target="_blank">terms of service</a> via API Evangelist guidance.
message: Has an API Terms of Service
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: >-
        \b(api-terms-of-service|terms-of-service|Terms of
        Service|TOS|TermsOfService)\b
```
## Property URLs Are Valid (apis-json-apis-properties-url-info)
This property ensures that properties of an API or API contract all have valid URLs, checking if any of the URLs are not properly formed, or could be other formats. This should be evolved based upon other types used like email, ftp, or other. You can find details about the <a href="https://apisjson.org/schema/property-url/">url property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/web/urls.html" target="_blank">urls</a> via API Evangelist guidance.

```
description: >-
  This property ensures that properties of an API or API contract all have valid
  URLs, checking if any of the URLs are not properly formed, or could be other
  formats. This should be evolved based upon other types used like email, ftp,
  or other. You can find details about the <a
  href="https://apisjson.org/schema/property-url/">url property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/web/urls.html"
  target="_blank">urls</a> via API Evangelist guidance.
message: Property URLs Are Valid
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: url
    function: pattern
    functionOptions:
      notMatch: >-
        ^((http|https)://)[-a-zA-Z0-9@:%._\+~#?&//=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%._\+~#?&//=]*)$
```
## Has Use Cases (apis-json-apis-properties-use-cases-info)
This property ensures there is a reference to the use cases for an API, helping align an API with the who, what, how, and why of putting an API to work. Use cases should be provided before an API is designed, but can also be added to over time, helping guid API delivery. You can find details about the <a href="https://apisjson.org/common/use-cases/">use cases property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/use-cases/overview.html" target="_blank">use cases</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a reference to the use cases for an API,
  helping align an API with the who, what, how, and why of putting an API to
  work. Use cases should be provided before an API is designed, but can also be
  added to over time, helping guid API delivery. You can find details about the
  <a href="https://apisjson.org/common/use-cases/">use cases property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/use-cases/overview.html"
  target="_blank">use cases</a> via API Evangelist guidance.
message: Has Use Cases
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(UseCases)\b
```
## Has a Team Defined (apis-json-apis-properties-teams-info)
This property ensures that there is a reference to the team behind an API, providing a reference to business and engineering stakeholders. Teams can be an HTML page, or depend on another system like GitHub to communicate what teams are producing an API. You can find details about the <a href="https://apisjson.org/common/teams/">aid property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/owners/teams.html" target="_blank">teams</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a reference to the team behind an API,
  providing a reference to business and engineering stakeholders. Teams can be
  an HTML page, or depend on another system like GitHub to communicate what
  teams are producing an API. You can find details about the <a
  href="https://apisjson.org/common/teams/">aid property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/owners/teams.html"
  target="_blank">teams</a> via API Evangelist guidance.
message: Has a Team Defined
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(team|teams|Team|Teams)\b
```
## Has Videos for API (apis-json-apis-properties-video-info)
This property ensures there is a reference to a video page or channel for an API. The video reference might be for a single API, or the entire API operation, providing videos for both producers or consumers. You can find details about the <a href="https://apisjson.org/common/videos/">videos property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/communication/videos.html" target="_blank">videos</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a reference to a video page or channel for an
  API. The video reference might be for a single API, or the entire API
  operation, providing videos for both producers or consumers. You can find
  details about the <a href="https://apisjson.org/common/videos/">videos
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/communication/videos.html"
  target="_blank">videos</a> via API Evangelist guidance.
message: Has Videos for API
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(videos|Videos)\b
```
## API MUST Have a Tags Object (apis-json-apis-tags-error)
This property ensures that there are tags associated with an API defined as part of a contract providing metadata and a bounded context for each of the APIs defined by a contract. Ideally tags are derived from a central vocabulary that can be used to define and govern the words and phrases being used as tags. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html" target="_blank">APIs.json tags</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there are tags associated with an API defined as
  part of a contract providing metadata and a bounded context for each of the
  APIs defined by a contract. Ideally tags are derived from a central vocabulary
  that can be used to define and govern the words and phrases being used as
  tags. You can find details about the <a
  href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html"
  target="_blank">APIs.json tags</a> via API Evangelist guidance.
message: API MUST Have a Tags Object
given: $.apis.*
severity: info
then:
  field: tags
  function: truthy
```
## API Have a Tags Object (apis-json-apis-tags-info)
This property ensures that there are tags associated with an API defined as part of a contract providing metadata and a bounded context for each of the APIs defined by a contract. Ideally tags are derived from a central vocabulary that can be used to define and govern the words and phrases being used as tags. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html" target="_blank">APIs.json tags</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there are tags associated with an API defined as
  part of a contract providing metadata and a bounded context for each of the
  APIs defined by a contract. Ideally tags are derived from a central vocabulary
  that can be used to define and govern the words and phrases being used as
  tags. You can find details about the <a
  href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html"
  target="_blank">APIs.json tags</a> via API Evangelist guidance.
message: API Have a Tags Object
given: $.apis.*
severity: info
then:
  field: tags
  function: falsy
```
## API Tags MUST Be Upper Case (apis-json-apis-tags-upper-case-error)
This ensures that the tags applied to APIs in the APIs.json contract are upper case, keeping a consistent look and feel across all tags applied. The casing should reflect whatever is applied in a central vocabulary, and be consistent across all tags applied to API operations. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html"  target="_blank">tag casing</a> via API Evangelist guidance.

```
description: >-
  This ensures that the tags applied to APIs in the APIs.json contract are upper
  case, keeping a consistent look and feel across all tags applied. The casing
  should reflect whatever is applied in a central vocabulary, and be consistent
  across all tags applied to API operations. You can find details about the <a
  href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html" 
  target="_blank">tag casing</a> via API Evangelist guidance.
message: API Tags MUST Be Upper Case
severity: error
given: $.apis.*.tags.*
then:
  function: pattern
  functionOptions:
    match: '[A-Z]\w*'
```
## API Tags are Upper Case (apis-json-apis-tags-upper-case-info)
This ensures that the tags applied to APIs in the APIs.json contract are upper case, keeping a consistent look and feel across all tags applied. The casing should reflect whatever is applied in a central vocabulary, and be consistent across all tags applied to API operations. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html"  target="_blank">tag casing</a> via API Evangelist guidance.

```
description: >-
  This ensures that the tags applied to APIs in the APIs.json contract are upper
  case, keeping a consistent look and feel across all tags applied. The casing
  should reflect whatever is applied in a central vocabulary, and be consistent
  across all tags applied to API operations. You can find details about the <a
  href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/api-tags.html" 
  target="_blank">tag casing</a> via API Evangelist guidance.
message: API Tags are Upper Case
severity: info
given: $.apis.*.tags.*
then:
  function: pattern
  functionOptions:
    notMatch: '[A-Z]\w*'
```
## There is an common property. (apis-json-common-info)
The common property is where all of the properties that apply across multiple APIs are stored. If the APIs.json is maintained by the API producer they are usually the common services supported via the developer portal, but if not, they could be external services offered by community, platform, or other entities. You can find details about the <a href="https://apisjson.org/schema/common/">baseUrl property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/discovery/common.html" target="_blank">common discovery properties</a> more via API Evangelist.

```
description: >-
  The common property is where all of the properties that apply across multiple
  APIs are stored. If the APIs.json is maintained by the API producer they are
  usually the common services supported via the developer portal, but if not,
  they could be external services offered by community, platform, or other
  entities. You can find details about the <a
  href="https://apisjson.org/schema/common/">baseUrl property for APIs.json</a>,
  and explore <a
  href="https://guidance.apievangelist.com/guidance/discovery/common.html"
  target="_blank">common discovery properties</a> more via API Evangelist.
message: There is an common property.
given: $
severity: info
then:
  field: common
  function: falsy
```
## There is a created date. (apis-json-created-info)
The created property is all about setting the timestamp for when an APIs.json index, contract, or other type is established--drawing a line in the sand for when everything started. The created property works in concert with the modified property and other change manage properties to understand and get a handle on the inevitable change that occurs across any API platform. You can find details about the <a href="https://apisjson.org/schema/created/">created property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/created.html" target="_blank">how created property is used to manage change</a> more via API Evangelist.

```
description: >-
  The created property is all about setting the timestamp for when an APIs.json
  index, contract, or other type is established--drawing a line in the sand for
  when everything started. The created property works in concert with the
  modified property and other change manage properties to understand and get a
  handle on the inevitable change that occurs across any API platform. You can
  find details about the <a href="https://apisjson.org/schema/created/">created
  property for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/created.html"
  target="_blank">how created property is used to manage change</a> more via API
  Evangelist.
message: There is a created date.
given: $
severity: info
then:
  field: created
  function: falsy
```
## There is a description. (apis-json-description-info)
The description property is where you provide full details the purpose an APIs.json serves. This description is likely more higher level than any of the descriptions for any single API, and be more about the contract, index, blueprint, or the other reasons why the APIs.json is of value. Don't make the description too long, but also don't make it too short--it is likely the first impression you will make via portals, repos, and other ways an APIs.json will be discovered. You can find details about the <a href="https://apisjson.org/schema/description/">description property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/descriptions/apis-json-descriptions.html" target="_blank">APIs.json</a> more via API Evangelist.

```
description: >-
  The description property is where you provide full details the purpose an
  APIs.json serves. This description is likely more higher level than any of the
  descriptions for any single API, and be more about the contract, index,
  blueprint, or the other reasons why the APIs.json is of value. Don't make the
  description too long, but also don't make it too short--it is likely the first
  impression you will make via portals, repos, and other ways an APIs.json will
  be discovered. You can find details about the <a
  href="https://apisjson.org/schema/description/">description property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/descriptions/apis-json-descriptions.html"
  target="_blank">APIs.json</a> more via API Evangelist.
message: There is a description.
given: $
severity: info
then:
  field: description
  function: falsy
```
## There is an image. (apis-json-image-info)
Images for APIs.json help make them more visible when rendered as a search or individual node, used as part of an API portal, or other ways. The image should represent the entity logo, line of business, or other meaningful visual representation of the bounded context represented within the APis.json. You can find details about the <a href="https://apisjson.org/schema/images/">images property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/images/apis-json-images.html" target="_blank">using images</a> more via API Evangelist.

```
description: >-
  Images for APIs.json help make them more visible when rendered as a search or
  individual node, used as part of an API portal, or other ways. The image
  should represent the entity logo, line of business, or other meaningful visual
  representation of the bounded context represented within the APis.json. You
  can find details about the <a
  href="https://apisjson.org/schema/images/">images property for APIs.json</a>,
  and explore <a
  href="https://guidance.apievangelist.com/guidance/images/apis-json-images.html"
  target="_blank">using images</a> more via API Evangelist.
message: There is an image.
given: $
severity: info
then:
  field: image
  function: falsy
```
## There is a email property for maintainers. (apis-json-maintainers-email-info)
The maintainers email is to provide a quick way to contact the maintainer of an APIs.json contract. The email is just one of multiple vCard properties that can exist, but provides the simplest way to engage with stakeholders involved in maintaining an APIs.json artifact. You can find details about the <a href="https://apisjson.org/schema/maintainers-email/">maintainers email property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/email.html" target="_blank">email support</a> more via API Evangelist.

```
description: >-
  The maintainers email is to provide a quick way to contact the maintainer of
  an APIs.json contract. The email is just one of multiple vCard properties that
  can exist, but provides the simplest way to engage with stakeholders involved
  in maintaining an APIs.json artifact. You can find details about the <a
  href="https://apisjson.org/schema/maintainers-email/">maintainers email
  property for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/email.html"
  target="_blank">email support</a> more via API Evangelist.
message: There is a email property for maintainers.
given: $.maintainers.*
severity: info
then:
  field: email
  function: falsy
```
## There is a FN property for maintainers. (apis-json-maintainers-fn-info)
The purpose of the FN is to specify the formatted text corresponding to the contact name in the vCard for an APIs.json contract or index. It could be a persons name or wider for a domain, team, or other bounded context, providing the reference needed for support or feedback. You can find details about the <a href="https://apisjson.org/schema/maintainers-fn/">API contact property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/name.html" target="_blank">support name</a> more via API Evangelist.

```
description: >-
  The purpose of the FN is to specify the formatted text corresponding to the
  contact name in the vCard for an APIs.json contract or index. It could be a
  persons name or wider for a domain, team, or other bounded context, providing
  the reference needed for support or feedback. You can find details about the
  <a href="https://apisjson.org/schema/maintainers-fn/">API contact property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/name.html"
  target="_blank">support name</a> more via API Evangelist.
message: There is a FN property for maintainers.
given: $.maintainers.*
severity: info
then:
  field: FN
  function: falsy
```
## There is a maintainer object. (apis-json-maintainers-info)
The maintainers property is for identifying the entity who is maintaining an APIs.json contract, index, or other type. The maintainer may or may not be an API producer, and the maintainer property is used to provide access to the contact information for the maintainer, but is also used to validate the authoritative nature of the contract itself. You can find details about the <a href="https://apisjson.org/schema/maintianers/">maintainers property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/support/names.html" target="_blank">support</a> more via API Evangelist.

```
description: >-
  The maintainers property is for identifying the entity who is maintaining an
  APIs.json contract, index, or other type. The maintainer may or may not be an
  API producer, and the maintainer property is used to provide access to the
  contact information for the maintainer, but is also used to validate the
  authoritative nature of the contract itself. You can find details about the <a
  href="https://apisjson.org/schema/maintianers/">maintainers property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/support/names.html"
  target="_blank">support</a> more via API Evangelist.
message: There is a maintainer object.
given: $
severity: info
then:
  field: maintainers
  function: falsy
```
## There is a modified date. (apis-json-modified-info)
The modified property of an APIs.json is meant to be updated with the date of when any changes were made to the contract or index. The modified properties works in concert with the created property, as well as other change management properties employed to help get a handle on the changes that are inevitable across API operations. You can find details about the <a href="https://apisjson.org/schema/modified/">modified property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/modified.html" target="_blank">modified property and change management</a> more via API Evangelist.

```
description: >-
  The modified property of an APIs.json is meant to be updated with the date of
  when any changes were made to the contract or index. The modified properties
  works in concert with the created property, as well as other change management
  properties employed to help get a handle on the changes that are inevitable
  across API operations. You can find details about the <a
  href="https://apisjson.org/schema/modified/">modified property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/modified.html"
  target="_blank">modified property and change management</a> more via API
  Evangelist.
message: There is a modified date.
given: $
severity: info
then:
  field: modified
  function: falsy
```
## There is a name. (apis-json-name-info)
The name of an APIs.json file is different than the name of your API, and is intended to describe the purpose of the APIs.json artifact, and what it provides for API producers, consumers, and other stakeholders. The name should be short and concise, describing the intent in bringing the the collection together, leaving the names of APIs to describe what each API does. You can find details about the <a href="https://apisjson.org/schema/names/">names property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/naming/apis-json-names.html" target="_blank">APIs.json names</a> more via API Evangelist.

```
description: >-
  The name of an APIs.json file is different than the name of your API, and is
  intended to describe the purpose of the APIs.json artifact, and what it
  provides for API producers, consumers, and other stakeholders. The name should
  be short and concise, describing the intent in bringing the the collection
  together, leaving the names of APIs to describe what each API does. You can
  find details about the <a href="https://apisjson.org/schema/names/">names
  property for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/naming/apis-json-names.html"
  target="_blank">APIs.json names</a> more via API Evangelist.
message: There is a name.
severity: info
given: $
then:
  field: name
  function: falsy
```
## There is an aid. (apis-json-specification-aid-info)
Ensures that each APIs.json has a unique identifier expressed as an `aid`. APIs.json identifiers are a standardized format for allowing API producers to establish a unique identifier for each API contract they provide using APIs.json, which will then be prepended to each APIs defined. You can find details about the standard for <a href="https://apisjson.org/schema/aid/">APIs.json unique identifier on API Commons</a>, and explore <a href="https://guidance.apievangelist.com/guidance/identifiers/apis-json-identifier.html" target="_blank">APIs.json Unique Identifiers</a> via API Evangelist.

```
description: >-
  Ensures that each APIs.json has a unique identifier expressed as an `aid`.
  APIs.json identifiers are a standardized format for allowing API producers to
  establish a unique identifier for each API contract they provide using
  APIs.json, which will then be prepended to each APIs defined. You can find
  details about the standard for <a
  href="https://apisjson.org/schema/aid/">APIs.json unique identifier on API
  Commons</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/identifiers/apis-json-identifier.html"
  target="_blank">APIs.json Unique Identifiers</a> via API Evangelist.
message: There is an aid.
severity: info
given: $
then:
  field: aid
  function: falsy
```
## There is a specification type. (apis-json-specification-type-info)
The specification type for an APIs.json sets the tone for how the APIs.json will be processed, providing a way to namespace different ways of leveraging the machine-readable contents of the APIs/json. The most common is a simple index of one or many APIs, but originally templates and examples were also allowed. Contracts, blueprints, and a handful of other types have recently been added, expanding the ways in which the APIs.json specification can be used beyond just API discovery. You can find details about the <a href="https://apisjson.org/schema/type/">type property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/contracts/type.html" target="_blank">APIs.json Unique Identifiers</a> via API Evangelist..

```
description: >-
  The specification type for an APIs.json sets the tone for how the APIs.json
  will be processed, providing a way to namespace different ways of leveraging
  the machine-readable contents of the APIs/json. The most common is a simple
  index of one or many APIs, but originally templates and examples were also
  allowed. Contracts, blueprints, and a handful of other types have recently
  been added, expanding the ways in which the APIs.json specification can be
  used beyond just API discovery. You can find details about the <a
  href="https://apisjson.org/schema/type/">type property for APIs.json</a>, and
  explore <a
  href="https://guidance.apievangelist.com/guidance/contracts/type.html"
  target="_blank">APIs.json Unique Identifiers</a> via API Evangelist..
message: There is a specification type.
severity: info
given: $
then:
  field: type
  function: falsy
```
## There is a specification version. (apis-json-specification-version-info)
The specification version of an APIs.json defines what properties are supported by the APIs.json artifact. New core properties, as well as property types are being added with each version to support a variety of solutions, and expand how APIs.json is used across API operations. You can find details about the <a href="https://apisjson.org/schema/specification-version/">specification version property for APIs.json</a>.

```
description: >-
  The specification version of an APIs.json defines what properties are
  supported by the APIs.json artifact. New core properties, as well as property
  types are being added with each version to support a variety of solutions, and
  expand how APIs.json is used across API operations. You can find details about
  the <a href="https://apisjson.org/schema/specification-version/">specification
  version property for APIs.json</a>.
message: There is a specification version.
severity: info
given: $
then:
  field: specificationVersion
  function: falsy
```
## There is a Tags Object (apis-json-tags-info)
Tags applied to an APIs.json should provide a handful of high-level tags that describe the purpose and intent of an APIs.json. These could be tags that describe the search node, or tags specifically for the individual APIs that are of concern for a specific API contract between producer and consumer. Tags provide the bounded context needed to help make APIs more tangible and meaningful for both API producers and consumers. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html" target="_blank">tagging</a> more via API Evangelist.

```
description: >-
  Tags applied to an APIs.json should provide a handful of high-level tags that
  describe the purpose and intent of an APIs.json. These could be tags that
  describe the search node, or tags specifically for the individual APIs that
  are of concern for a specific API contract between producer and consumer. Tags
  provide the bounded context needed to help make APIs more tangible and
  meaningful for both API producers and consumers. You can find details about
  the <a href="https://apisjson.org/schema/tags/">tags property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html"
  target="_blank">tagging</a> more via API Evangelist.
message: There is a Tags Object
given: $
severity: info
then:
  field: tags
  function: falsy
```
## Tags Upper Case (apis-json-tags-upper-case-error)
Tags are useful for defining the bounded context of API operations, and it helps to ensure they are consistently capitalized for better display within documentation and other resources. Emsuring that the first letter is upper cased, acronyms properly cased, and other terms, helps make sure things are readable, and act as a vocabulary for API operations. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html" target="_blank">tagging</a> more via API Evangelist.

```
description: >-
  Tags are useful for defining the bounded context of API operations, and it
  helps to ensure they are consistently capitalized for better display within
  documentation and other resources. Emsuring that the first letter is upper
  cased, acronyms properly cased, and other terms, helps make sure things are
  readable, and act as a vocabulary for API operations. You can find details
  about the <a href="https://apisjson.org/schema/tags/">tags property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html"
  target="_blank">tagging</a> more via API Evangelist.
message: Tags Upper Case
severity: error
given: $.tags.*
then:
  function: pattern
  functionOptions:
    match: '[A-Z]\w*'
```
## Tags Upper Case (apis-json-tags-upper-case-info)
Tags are useful for defining the bounded context of API operations, and it helps to ensure they are consistently capitalized for better display within documentation and other resources. Emsuring that the first letter is upper cased, acronyms properly cased, and other terms, helps make sure things are readable, and act as a vocabulary for API operations. You can find details about the <a href="https://apisjson.org/schema/tags/">tags property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html" target="_blank">tagging</a> more via API Evangelist.

```
description: >-
  Tags are useful for defining the bounded context of API operations, and it
  helps to ensure they are consistently capitalized for better display within
  documentation and other resources. Emsuring that the first letter is upper
  cased, acronyms properly cased, and other terms, helps make sure things are
  readable, and act as a vocabulary for API operations. You can find details
  about the <a href="https://apisjson.org/schema/tags/">tags property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/bounded-context/apis-json-tags.html"
  target="_blank">tagging</a> more via API Evangelist.
message: Tags Upper Case
severity: info
given: $.tags.*
then:
  function: pattern
  functionOptions:
    notMatch: '[A-Z]\w*'
```
## There is a URL. (apis-json-url-info)
The URL for an APIs.json provides a link to the source of an APIs.json, but also determines whether or not an APIs.json is authoritative or not. The URL is a locator, but can also be used as an identifier that can be used to ensure the authenticity and origin of APIs.json. The URL is regularly validated as part of API operations and the solutions using the APIs.json. You can find details about the <a href="https://apisjson.org/schema/url/">url property for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/contracts/apis-json-url.html" target="_blank">APIs.json URLs</a> more via API Evangelist.

```
description: >-
  The URL for an APIs.json provides a link to the source of an APIs.json, but
  also determines whether or not an APIs.json is authoritative or not. The URL
  is a locator, but can also be used as an identifier that can be used to ensure
  the authenticity and origin of APIs.json. The URL is regularly validated as
  part of API operations and the solutions using the APIs.json. You can find
  details about the <a href="https://apisjson.org/schema/url/">url property for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/contracts/apis-json-url.html"
  target="_blank">APIs.json URLs</a> more via API Evangelist.
message: There is a URL.
given: $
severity: info
then:
  field: url
  function: falsy
```
## Has Versioning for API (apis-json-apis-properties-versioning-info)
This property ensures there is a reference to how APIs are versioned, providing a single place where teams can learn about how change is communicated. The versioning page will usually talk about whether it is Semantic or date-based versioning, as well as referencing the change log, road map, and other elements You can find details about the <a href="https://apisjson.org/common/versioning/">versioning property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/change/versioning.html" target="_blank">versioning</a> via API Evangelist guidance.

```
description: >-
  This property ensures there is a reference to how APIs are versioned,
  providing a single place where teams can learn about how change is
  communicated. The versioning page will usually talk about whether it is
  Semantic or date-based versioning, as well as referencing the change log, road
  map, and other elements You can find details about the <a
  href="https://apisjson.org/common/versioning/">versioning property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/change/versioning.html"
  target="_blank">versioning</a> via API Evangelist guidance.
message: Has Versioning for API
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(versions|Versions|Versioning|versioning)\b
```
## Has Staging Gateway for API (apis-json-apis-properties-gateway-info)
This property ensures that there is a reference to the gateway for an API, referencing where you can manage the configuration for each API. Each gateway stage for an API ideally has a dedicated URL which contains the unique identifier for the API which can be access via the gateway API. You can find details about the <a href="https://apisjson.org/common/gateways/">gateway property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/gateways/overview.html" target="_blank">gateways</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a reference to the gateway for an API,
  referencing where you can manage the configuration for each API. Each gateway
  stage for an API ideally has a dedicated URL which contains the unique
  identifier for the API which can be access via the gateway API. You can find
  details about the <a href="https://apisjson.org/common/gateways/">gateway
  property type for APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/gateways/overview.html"
  target="_blank">gateways</a> via API Evangelist guidance.
message: Has Staging Gateway for API
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(gateway|Gateway)\b
```
## Has APIs.json (Business) Validator (apis-json-apis-properties-apis-json-validator-info)
This property ensures that there is a link to the validator for the APIs.json business contract, allowing anyone to see the details of governance being applied. The validator is custom to each API and the business contract, providing all the details of rules that are governing the APIs.json for an API. You can find details about the <a href="https://apisjson.org/common/validator/">validator property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/validator/overview.html" target="_blank">validator</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a link to the validator for the APIs.json
  business contract, allowing anyone to see the details of governance being
  applied. The validator is custom to each API and the business contract,
  providing all the details of rules that are governing the APIs.json for an
  API. You can find details about the <a
  href="https://apisjson.org/common/validator/">validator property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/validator/overview.html"
  target="_blank">validator</a> via API Evangelist guidance.
message: Has APIs.json (Business) Validator
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(OperationalValidation)\b
```
## Has OpenAPI (Technical) Validator (apis-json-apis-properties-openapi-validator-info)
This property ensures that there is a link to the validator for the OpenAPI technical contract, allowing anyone to see the details of governance being applied. The validator is custom to each API and the technical contract, providing all the details of rules that are governing the OpenAPI for an API. You can find details about the <a href="https://apisjson.org/common/validator/">validator property type for APIs.json</a>, and explore <a href="https://guidance.apievangelist.com/guidance/validator/overview.html" target="_blank">validator</a> via API Evangelist guidance.

```
description: >-
  This property ensures that there is a link to the validator for the OpenAPI
  technical contract, allowing anyone to see the details of governance being
  applied. The validator is custom to each API and the technical contract,
  providing all the details of rules that are governing the OpenAPI for an API.
  You can find details about the <a
  href="https://apisjson.org/common/validator/">validator property type for
  APIs.json</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/validator/overview.html"
  target="_blank">validator</a> via API Evangelist guidance.
message: Has OpenAPI (Technical) Validator
severity: info
given:
  - $.apis.*.properties.*
  - $.common.*
then:
  - field: type
    function: pattern
    functionOptions:
      notMatch: \b(APIValidation)\b
```
## APIs Rules
This are the Spectral rules governing the surface areas of APIs as defined by OpenAPI, linting for all the common technical details of producing HTTP APIs.

## Components MUST Have a Security Schemes (openapi-security-schemes-error)
Having components security schemes ensures that the security definition for an API have been standardized and are able to be applied across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security schemes object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/security.html" target="_blank">OpenAPI security</a> via API Evangelist guidance.

```
description: >-
  Having components security schemes ensures that the security definition for an
  API have been standardized and are able to be applied across APIs. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security
  schemes object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/security.html"
  target="_blank">OpenAPI security</a> via API Evangelist guidance.
message: Components MUST Have a Security Schemes
severity: error
given: $.components
then:
  field: securitySchemes
  function: truthy
```
## Components Have a Security Schemes (openapi-security-schemes-info)
Having components security schemes ensures that the security definition for an API have been standardized and are able to be applied across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security schemes object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/security.html" target="_blank">OpenAPI security</a> via API Evangelist guidance.

```
description: >-
  Having components security schemes ensures that the security definition for an
  API have been standardized and are able to be applied across APIs. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security
  schemes object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/security.html"
  target="_blank">OpenAPI security</a> via API Evangelist guidance.
message: Components Have a Security Schemes
severity: info
given: $.components
then:
  field: securitySchemes
  function: falsy
```
## Components MUST Have a Parameters Property (openapi-components-parameters-error)
Having a components parameters object allows all parameters used across an API to be centralized, allowing for reuse and easier governance of the parameters used to configure API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/parameters.html" target="_blank">OpenAPI parameters</a> via API Evangelist guidance.

```
description: >-
  Having a components parameters object allows all parameters used across an API
  to be centralized, allowing for reuse and easier governance of the parameters
  used to configure API requests. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/parameters.html"
  target="_blank">OpenAPI parameters</a> via API Evangelist guidance.
message: Components MUST Have a Parameters Property
severity: error
given: $.components
then:
  field: parameters
  function: truthy
```
## Components Have a Parameters Property (openapi-components-parameters-info)
Having a components parameters object allows all parameters used across an API to be centralized, allowing for reuse and easier governance of the parameters used to configure API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/parameters.html" target="_blank">OpenAPI parameters</a> via API Evangelist guidance.

```
description: >-
  Having a components parameters object allows all parameters used across an API
  to be centralized, allowing for reuse and easier governance of the parameters
  used to configure API requests. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/parameters.html"
  target="_blank">OpenAPI parameters</a> via API Evangelist guidance.
message: Components Have a Parameters Property
severity: info
given: $.components
then:
  field: parameters
  function: falsy
```
## Parameters MUST Have a Description (openapi-components-parameters-description-error)
Having a parameters description provides more depth to what a parameter does and will be displayed via documentation, and other tooling used across the API lifecycle. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/parameters.html" target="_blank">OpenAPI parameters</a> via API Evangelist guidance.

```
description: >-
  Having a parameters description provides more depth to what a parameter does
  and will be displayed via documentation, and other tooling used across the API
  lifecycle. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/parameters.html"
  target="_blank">OpenAPI parameters</a> via API Evangelist guidance.
message: Parameters MUST Have a Description
given: $.paths.*.*.parameters.*
then:
  field: description
  function: truthy
```
## Parameters Have a Description (openapi-components-parameters-description-info)
Having a parameters description provides more depth to what a parameter does and will be displayed via documentation, and other tooling used across the API lifecycle. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/parameters.html" target="_blank">OpenAPI parameters</a> via API Evangelist guidance.

```
description: >-
  Having a parameters description provides more depth to what a parameter does
  and will be displayed via documentation, and other tooling used across the API
  lifecycle. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/parameters.html"
  target="_blank">OpenAPI parameters</a> via API Evangelist guidance.
message: Parameters Have a Description
severity: info
given: $.components.parameters.*
then:
  field: description
  function: falsy
```
## Parameters Description MUST Be Less Than 500 Characters (openapi-components-parameters-description-length-error)
Limiting the length of parameters description forces us to be more concise in how we describe each parameter, while keeping our documentation and other ways descriptions show up in discovery and portals more consistent. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/parameters.html" target="_blank">OpenAPI parameters</a> via API Evangelist guidance.

```
description: >-
  Limiting the length of parameters description forces us to be more concise in
  how we describe each parameter, while keeping our documentation and other ways
  descriptions show up in discovery and portals more consistent. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/parameters.html"
  target="_blank">OpenAPI parameters</a> via API Evangelist guidance.
message: Parameters Description MUST Be Less Than 500 Characters
given: $.components.parameters.*
then:
  field: summary
  function: length
  functionOptions:
    max: 500
```
## Parameters Enums MUST Must Be Upper Snake Case (openapi-components-parameters-enum-casing-error)
Keeping parameters enumerator casing consistent across APIs helps reduce confusion by consumers, and can keep aligned with services and applications putting an API to work. You can find details about the <a href="https://spec.openapis.org/oas/latest.html##parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html" target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.

```
description: >-
  Keeping parameters enumerator casing consistent across APIs helps reduce
  confusion by consumers, and can keep aligned with services and applications
  putting an API to work. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html##parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html"
  target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.
message: Parameters Enums MUST Must Be Upper Snake Case
severity: error
given: $.components.parameters.*.enum.*
then:
  function: pattern
  functionOptions:
    notMatch: ^[A-Z]+(?:_[A-Z]+)*$
```
## Parameters Enums Are Upper Snake Case (openapi-components-parameters-enum-casing-info)
Keeping parameters enumerator casing consistent across APIs helps reduce confusion by consumers, and can keep aligned with services and applications putting an API to work. You can find details about the <a href="https://spec.openapis.org/oas/latest.html##parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html" target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.

```
description: >-
  Keeping parameters enumerator casing consistent across APIs helps reduce
  confusion by consumers, and can keep aligned with services and applications
  putting an API to work. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html##parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html"
  target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.
message: Parameters Enums Are Upper Snake Case
severity: info
given: $.components.parameters.*.enum.*
then:
  function: pattern
  functionOptions:
    match: ^[A-Z]+(?:_[A-Z]+)*$
```
## Parameters Have Enum (openapi-components-parameters-enum-info)
Providing enums for your parameters helps reduce errors and keeps the inputs for your API requests more consistent for consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html" target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.

```
description: >-
  Providing enums for your parameters helps reduce errors and keeps the inputs
  for your API requests more consistent for consumers. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-enum.html"
  target="_blank">OpenAPI parameter enums</a> via API Evangelist guidance.
message: Parameters Have Enum
severity: info
given: $.components.parameters.*
then:
  field: enum
  function: falsy
```
## Parameters In Property MUST Be Set (openapi-components-parameters-in-error)
Providing an in property for parameters gets explicit about whether a parameter is in the path, query, or a header, making it clear to consumers where they can configure their request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-in.html" target="_blank">OpenAPI parameter in</a> via API Evangelist guidance.

```
description: >-
  Providing an in property for parameters gets explicit about whether a
  parameter is in the path, query, or a header, making it clear to consumers
  where they can configure their request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-in.html"
  target="_blank">OpenAPI parameter in</a> via API Evangelist guidance.
message: Parameters In Property MUST Be Set
given: $.components.parameters.*
then:
  field: in
  function: truthy
```
## Parameters In Property Is Set (openapi-components-parameters-in-info)
Providing an in property for parameters gets explicit about whether a parameter is in the path, query, or a header, making it clear to consumers where they can configure their request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-in.html" target="_blank">OpenAPI parameter in</a> via API Evangelist guidance.

```
description: >-
  Providing an in property for parameters gets explicit about whether a
  parameter is in the path, query, or a header, making it clear to consumers
  where they can configure their request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-in.html"
  target="_blank">OpenAPI parameter in</a> via API Evangelist guidance.
message: Parameters In Property Is Set
severity: info
given: $.components.parameters.*
then:
  field: in
  function: falsy
```
## Parameters MUST Have a Name (openapi-components-parameters-name-error)
Providing a simple, intuitive, and consistent names for your parameters helps make it easier for API consumers to understand how they are able to configure their API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html" target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.

```
description: >-
  Providing a simple, intuitive, and consistent names for your parameters helps
  make it easier for API consumers to understand how they are able to configure
  their API requests. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html"
  target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.
message: Parameters MUST Have a Name
severity: error
given: $.components.parameters.*
then:
  field: name
  function: truthy
```
## Parameters Have a Name (openapi-components-parameters-name-info)
Providing a simple, intuitive, and consistent names for your parameters helps make it easier for API consumers to understand how they are able to configure their API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html" target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.

```
description: >-
  Providing a simple, intuitive, and consistent names for your parameters helps
  make it easier for API consumers to understand how they are able to configure
  their API requests. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html"
  target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.
message: Parameters Have a Name
severity: info
given: $.components.parameters.*
then:
  field: name
  function: falsy
```
## Parameters Name Length MUST Be Less Than 25 Characters (openapi-components-parameters-name-length-error)
Providing short and concise names for your parameters helps make it easier for API consumers to understand how they are able to configure their API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html" target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.

```
description: >-
  Providing short and concise names for your parameters helps make it easier for
  API consumers to understand how they are able to configure their API requests.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html"
  target="_blank">OpenAPI parameter names</a> via API Evangelist guidance.
message: Parameters Name Length MUST Be Less Than 25 Characters
given: $.components.parameters[?(@.in=='path')].name
then:
  field: summary
  function: length
  functionOptions:
    max: 25
```
## Parameters Names MUST Be Camel Case (openapi-components-parameters-casing-camel-error)
Providing parameters with consistent naming helps make it easier for API consumers to understand how they are able to configure their API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html" target="_blank">OpenAPI parameter casing</a> via API Evangelist guidance.

```
description: >-
  Providing parameters with consistent naming helps make it easier for API
  consumers to understand how they are able to configure their API requests. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html"
  target="_blank">OpenAPI parameter casing</a> via API Evangelist guidance.
message: Parameters Names MUST Be Camel Case
severity: error
given: $.components.parameters.*
then:
  - field: name
    function: pattern
    functionOptions:
      notMatch: ^[a-z]+(?:[A-Z][a-z]+)*$
  - field: name
    function: pattern
    functionOptions:
      match: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Parameters Names Are Camel Case (openapi-components-parameters-casing-camel-info)
Providing parameters with consistent naming helps make it easier for API consumers to understand how they are able to configure their API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html" target="_blank">OpenAPI parameter casing</a> via API Evangelist guidance.

```
description: >-
  Providing parameters with consistent naming helps make it easier for API
  consumers to understand how they are able to configure their API requests. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-names.html"
  target="_blank">OpenAPI parameter casing</a> via API Evangelist guidance.
message: Parameters Names Are Camel Case
severity: info
given: $.components.parameters.*
then:
  - field: name
    function: pattern
    functionOptions:
      notMatch: ^[a-z]+(?:[A-Z][a-z]+)*$
  - field: name
    function: pattern
    functionOptions:
      match: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Parameters MUST Have Schema (openapi-components-parameters-schema-error)
Parameters must always possess a schema to help define the format and shape of the parameter, setting expections with consumers about what should be passed in. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always possess a schema to help define the format and shape of
  the parameter, setting expections with consumers about what should be passed
  in. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameters MUST Have Schema
given: $.components.parameters.*
then:
  field: schema
  function: truthy
```
## Parameters Have Schema (openapi-components-parameters-schema-info)
Parameters must always possess a schema to help define the format and shape of the parameter, setting expections with consumers about what should be passed in. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always possess a schema to help define the format and shape of
  the parameter, setting expections with consumers about what should be passed
  in. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameters Have Schema
severity: info
given: $.components.parameters.*
then:
  field: schema
  function: falsy
```
## Parameters MUST Use Schema Reference (openapi-components-parameters-schema-ref-error)
Parameters must always use a schema reference that utilizes reusable schema that are defined as part of a centralized schema components library. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always use a schema reference that utilizes reusable schema
  that are defined as part of a centralized schema components library. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameters MUST Use Schema Reference
severity: error
given: $.components.parameters.*.schema
then:
  field: $ref
  function: falsy
```
## Parameters Use Schema Reference (openapi-components-parameters-schema-ref-info)
Parameters must always use a schema reference that utilizes reusable schema that are defined as part of a centralized schema components library. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always use a schema reference that utilizes reusable schema
  that are defined as part of a centralized schema components library. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameters Use Schema Reference
severity: info
given: $.components.parameters.*.schema
then:
  field: $ref
  function: truthy
```
## Parameter Schema Array MUST Have Items (openapi-components-parameters-schema-items-array-error)
Parameters that are of an array type should always have the items defined, being explicit about what is continued as part of the array. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of an array type should always have the items defined,
  being explicit about what is continued as part of the array. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameter Schema Array MUST Have Items
given: $.components.parameters.schema[?(@.type=='array')]
then:
  field: items
  function: truthy
```
## Parameter Schema Array MUST Has Items (openapi-components-parameters-schema-items-array-info)
Parameters that are of an array type should always have the items defined, being explicit about what is continued as part of the array. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of an array type should always have the items defined,
  being explicit about what is continued as part of the array. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameter Schema Array MUST Has Items
severity: info
given: $.components.parameters.schema[?(@.type=='array')]
then:
  field: items
  function: falsy
```
## Parameter Schema Type (openapi-components-parameters-schema-type-error)
Parameters must always have their schema type defined, being precise about what type of data can be inputted and used to configure an API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always have their schema type defined, being precise about
  what type of data can be inputted and used to configure an API request. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameter Schema Type
given: $.components.parameters.*.schema
then:
  field: type
  function: truthy
```
## Parameter Schema Type (openapi-components-parameters-schema-type-info)
Parameters must always have their schema type defined, being precise about what type of data can be inputted and used to configure an API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html" target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.

```
description: >-
  Parameters must always have their schema type defined, being precise about
  what type of data can be inputted and used to configure an API request. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-schema.html"
  target="_blank">OpenAPI parameter schema</a> via API Evangelist guidance.
message: Parameter Schema Type
severity: info
given: $.components.parameters.*.schema
then:
  field: type
  function: falsy
```
## Parameter Schema Type Integer Maximum (openapi-components-parameters-schema-type-integer-maximum-info)
Parameters that are of the integer schema type must have their maximum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the integer schema type must have their maximum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type Integer Maximum
given:
  - $.components.parameters.[?(@.type=='integer')]
severity: info
then:
  field: maximum
  function: falsy
```
## Parameter Schema Type Integer Maximum (openapi-components-parameters-schema-type-integer-maximum-warn)
Parameters that are of the integer schema type must have their maximum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the integer schema type must have their maximum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type Integer Maximum
given:
  - $.components.parameters.[?(@.type=='integer')]
severity: warn
then:
  field: maximum
  function: truthy
```
## Parameter Schema Type Integer Minimum (openapi-components-parameters-schema-type-integer-minimum-info)
Parameters that are of the integer schema type must have their minimum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the integer schema type must have their minimum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type Integer Minimum
given:
  - $.components.parameters.[?(@.type=='integer')]
severity: info
then:
  field: minimum
  function: falsy
```
## Parameter Schema Type Integer Minimum (openapi-components-parameters-schema-type-integer-minimum-warn)
Parameters that are of the integer schema type must have their minimum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the integer schema type must have their minimum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type Integer Minimum
given:
  - $.components.parameters.[?(@.type=='integer')]
severity: warn
then:
  field: minimum
  function: truthy
```
## Parameter Schema Type String MaxLength (openapi-components-parameters-schema-type-string-maxlength-info)
Parameters that are of the type string schema type must have their maximum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the type string schema type must have their maximum
  value set, defining the shape of parameter data passed in with a request. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String MaxLength
given:
  - $.components.parameters.[?(@.type=='string')]
severity: info
then:
  field: maxLength
  function: falsy
```
## Parameter Schema Type String MaxLength (openapi-components-parameters-schema-type-string-maxlength-warn)
Parameters that are of the string schema type must have their maximum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the string schema type must have their maximum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String MaxLength
given:
  - $.components.parameters.[?(@.type=='string')]
severity: warn
then:
  field: maxLength
  function: truthy
```
## Parameter Schema Type String MinLength (openapi-components-parameters-schema-type-string-minlength-info)
Parameters that are of the string schema type must have their minimum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the string schema type must have their minimum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String MinLength
given:
  - $.components.parameters.[?(@.type=='string')]
severity: info
then:
  field: minLength
  function: falsy
```
## Parameter Schema Type String MinLength (openapi-components-parameters-schema-type-string-minlength-warn)
Parameters that are of the string schema type must have their minimum value set, defining the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the string schema type must have their minimum value
  set, defining the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String MinLength
given:
  - $.components.parameters.[?(@.type=='string')]
severity: warn
then:
  field: minLength
  function: truthy
```
## Parameter Schema Type String Pattern (openapi-components-parameters-schema-type-string-pattern-info)
Parameters that are of the string schema type must have a pattern set, using a regex to define the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the string schema type must have a pattern set, using a
  regex to define the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String Pattern
given:
  - $.components.parameters.[?(@.type=='string')]
severity: info
then:
  field: pattern
  function: falsy
```
## Parameter Schema Type String Pattern (openapi-components-parameters-schema-type-string-pattern-warn)
Parameters that are of the string schema type must have a pattern set, using a regex to define the shape of parameter data passed in with a request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html" target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.

```
description: >-
  Parameters that are of the string schema type must have a pattern set, using a
  regex to define the shape of parameter data passed in with a request. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#parameter-object">parameters
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-parameter-types.html"
  target="_blank">OpenAPI parameter types</a> via API Evangelist guidance.
message: Parameter Schema Type String Pattern
given:
  - $.components.parameters.[?(@.type=='string')]
severity: warn
then:
  field: pattern
  function: truthy
```
## Components MUST Have a Examples Property (openapi-components-examples-error)
Utilizing an example object in the centralized OpenAPI components library helps make examples reusable across API requests and responses. Having examples centralized makes it easier to define, use, but also govern and analyze the examples provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-examples.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing an example object in the centralized OpenAPI components library
  helps make examples reusable across API requests and responses. Having
  examples centralized makes it easier to define, use, but also govern and
  analyze the examples provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-examples.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components MUST Have a Examples Property
severity: error
given: $.components
then:
  field: examples
  function: truthy
```
## Components Have a Examples Property (openapi-components-examples-info)
Utilizing an example object in the centralized OpenAPI components library helps make examples reusable across API requests and responses. Having examples centralized makes it easier to define, use, but also govern and analyze the examples provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-examples.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing an example object in the centralized OpenAPI components library
  helps make examples reusable across API requests and responses. Having
  examples centralized makes it easier to define, use, but also govern and
  analyze the examples provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-examples.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components Have a Examples Property
severity: info
given: $.components
then:
  field: examples
  function: falsy
```
## Components MUST Have a Schema Property (openapi-components-schemas-error)
Utilizing the schema object in the centralized OpenAPI components library helps make schema reusable across API requests and responses. Having schema centralized makes it easier to define, use, but also govern and analyze the schema provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-schema.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing the schema object in the centralized OpenAPI components library
  helps make schema reusable across API requests and responses. Having schema
  centralized makes it easier to define, use, but also govern and analyze the
  schema provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-schema.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components MUST Have a Schema Property
severity: error
given: $.components
then:
  field: schemas
  function: truthy
```
## Components Have a Schema Property (openapi-components-schemas-info)
Utilizing the schema object in the centralized OpenAPI components library helps make schema reusable across API requests and responses. Having schema centralized makes it easier to define, use, but also govern and analyze the schema provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-schema.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing the schema object in the centralized OpenAPI components library
  helps make schema reusable across API requests and responses. Having schema
  centralized makes it easier to define, use, but also govern and analyze the
  schema provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-schema.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components Have a Schema Property
severity: info
given: $.components
then:
  field: schemas
  function: falsy
```
## Components MUST Have a Headers Property (openapi-components-headers-error)
Utilizing the headers object in the centralized OpenAPI components library helps make headers reusable across API requests and responses. Having headers centralized makes it easier to define, use, but also govern and analyze the headers provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-headers.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing the headers object in the centralized OpenAPI components library
  helps make headers reusable across API requests and responses. Having headers
  centralized makes it easier to define, use, but also govern and analyze the
  headers provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-headers.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components MUST Have a Headers Property
severity: error
given: $.components
then:
  field: headers
  function: truthy
```
## Components Have a Headers Property (openapi-components-headers-info)
Utilizing the headers object in the centralized OpenAPI components library helps make headers reusable across API requests and responses. Having headers centralized makes it easier to define, use, but also govern and analyze the headers provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components example object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-headers.html" target="_blank">components examples</a> via API Evangelist guidance.

```
description: >-
  Utilizing the headers object in the centralized OpenAPI components library
  helps make headers reusable across API requests and responses. Having headers
  centralized makes it easier to define, use, but also govern and analyze the
  headers provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  example object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-headers.html"
  target="_blank">components examples</a> via API Evangelist guidance.
message: Components Have a Headers Property
severity: info
given: $.components
then:
  field: headers
  function: falsy
```
## Components MUST Have Rate Limit Headers (openapi-components-headers-rate-limit-error)
Utilizing centralized headers rate limits allows you to reuse headers across all API requests and responses, enabling a more organized approach to handling the transport and rate limits applied consistently across all APIs You can find details about the <a href="https://spec.openapis.org/oas/latest.html#header-object">header object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/headers-rate-limits.html" target="_blank">rate limit headers</a> via API Evangelist guidance.

```
description: >-
  Utilizing centralized headers rate limits allows you to reuse headers across
  all API requests and responses, enabling a more organized approach to handling
  the transport and rate limits applied consistently across all APIs You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#header-object">header object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/headers-rate-limits.html"
  target="_blank">rate limit headers</a> via API Evangelist guidance.
message: Components MUST Have Rate Limit Headers
severity: error
given: $.components.headers
then:
  field: RateLimit
  function: truthy
```
## Components Have Rate Limit Headers (openapi-components-headers-rate-limit-info)
Utilizing centralized headers rate limits allows you to reuse headers across all API requests and responses, enabling a more organized approach to handling the transport and rate limits applied consistently across all APIs You can find details about the <a href="https://spec.openapis.org/oas/latest.html#header-object">header object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/headers-rate-limits.html" target="_blank">rate limit headers</a> via API Evangelist guidance.

```
description: >-
  Utilizing centralized headers rate limits allows you to reuse headers across
  all API requests and responses, enabling a more organized approach to handling
  the transport and rate limits applied consistently across all APIs You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#header-object">header object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/headers-rate-limits.html"
  target="_blank">rate limit headers</a> via API Evangelist guidance.
message: Components Have Rate Limit Headers
severity: info
given: $.components.headers
then:
  field: RateLimit
  function: falsy
```
## Components MUST have a retry after headers. (openapi-components-headers-retry-after-error)
Utilizing centralized retry after headers allows you to reuse headers across all API requests and responses, enabling a more organized approach to handling the transport and rate limiting applied consistently across all APIs You can find details about the <a href="https://spec.openapis.org/oas/latest.html#header-object">header object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/headers-retry-after.html" target="_blank">retry after headers</a> via API Evangelist guidance.

```
description: >-
  Utilizing centralized retry after headers allows you to reuse headers across
  all API requests and responses, enabling a more organized approach to handling
  the transport and rate limiting applied consistently across all APIs You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#header-object">header object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/headers-retry-after.html"
  target="_blank">retry after headers</a> via API Evangelist guidance.
message: Components MUST have a retry after headers.
severity: error
given: $.components.headers
then:
  field: Retry-After
  function: truthy
```
## Components has a retry after header. (openapi-components-headers-retry-after-info)
Utilizing centralized retry after headers allows you to reuse headers across all API requests and responses, enabling a more organized approach to handling the transport and rate limiting applied consistently across all APIs You can find details about the <a href="https://spec.openapis.org/oas/latest.html#header-object">header object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/headers-retry-after.html" target="_blank">retry after headers</a> via API Evangelist guidance.

```
description: >-
  Utilizing centralized retry after headers allows you to reuse headers across
  all API requests and responses, enabling a more organized approach to handling
  the transport and rate limiting applied consistently across all APIs You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#header-object">header object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/headers-retry-after.html"
  target="_blank">retry after headers</a> via API Evangelist guidance.
message: Components has a retry after header.
severity: info
given: $.components.headers
then:
  field: Retry-After
  function: falsy
```
## Components MUST have a responses property. (openapi-components-responses-error)
Utilizing the responses object in the centralized OpenAPI components library helps make responses reusable across API requests. Having responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-responses.html" target="_blank">components responses</a> via API Evangelist guidance.

```
description: >-
  Utilizing the responses object in the centralized OpenAPI components library
  helps make responses reusable across API requests. Having responses
  centralized makes it easier to define, use, but also govern and analyze the
  responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-responses.html"
  target="_blank">components responses</a> via API Evangelist guidance.
message: Components MUST have a responses property.
severity: error
given: $.components
then:
  field: responses
  function: truthy
```
## Components has a responses property. (openapi-components-responses-info)
Utilizing the responses object in the centralized OpenAPI components library helps make responses reusable across API requests. Having responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-responses.html" target="_blank">components responses</a> via API Evangelist guidance.

```
description: >-
  Utilizing the responses object in the centralized OpenAPI components library
  helps make responses reusable across API requests. Having responses
  centralized makes it easier to define, use, but also govern and analyze the
  responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-responses.html"
  target="_blank">components responses</a> via API Evangelist guidance.
message: Components has a responses property.
severity: info
given: $.components
then:
  field: responses
  function: falsy
```
## Components MUST have a bad request response. (openapi-components-responses-bad-request-error)
Having a bad request responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-bad-request.html" target="_blank">bad request responses</a> via API Evangelist guidance.

```
description: >-
  Having a bad request responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-bad-request.html"
  target="_blank">bad request responses</a> via API Evangelist guidance.
message: Components MUST have a bad request response.
severity: error
given: $.components.responses
then:
  field: BadRequest
  function: truthy
```
## Components has a bad request response. (openapi-components-responses-bad-request-info)
Having a bad request responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-bad-request.html" target="_blank">bad request responses</a> via API Evangelist guidance.

```
description: >-
  Having a bad request responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-bad-request.html"
  target="_blank">bad request responses</a> via API Evangelist guidance.
message: Components has a bad request response.
severity: info
given: $.components.responses
then:
  field: BadRequest
  function: falsy
```
## Components MUST have a conflict response. (openapi-components-responses-conflict-error)
Having a conflict responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-conflict.html" target="_blank">conflict responses</a> via API Evangelist guidance.

```
description: >-
  Having a conflict responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-conflict.html"
  target="_blank">conflict responses</a> via API Evangelist guidance.
message: Components MUST have a conflict response.
severity: error
given: $.components.responses
then:
  field: Conflict
  function: truthy
```
## Components has a conflict response. (openapi-components-responses-conflict-info)
Having a conflict responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-conflict.html" target="_blank">conflict responses</a> via API Evangelist guidance.

```
description: >-
  Having a conflict responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-conflict.html"
  target="_blank">conflict responses</a> via API Evangelist guidance.
message: Components has a conflict response.
severity: info
given: $.components.responses
then:
  field: Conflict
  function: falsy
```
## Components MUST have a forbidden response. (openapi-components-responses-forbidden-error)
Having a forbidden responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-forbidden.html" target="_blank">forbidden responses</a> via API Evangelist guidance.

```
description: >-
  Having a forbidden responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-forbidden.html"
  target="_blank">forbidden responses</a> via API Evangelist guidance.
message: Components MUST have a forbidden response.
severity: error
given: $.components.responses
then:
  field: Forbidden
  function: truthy
```
## Components has a forbidden response. (openapi-components-responses-forbidden-info)
Having a forbidden responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-forbidden.html" target="_blank">forbidden responses</a> via API Evangelist guidance.

```
description: >-
  Having a forbidden responses in the centralized OpenAPI components library
  helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-forbidden.html"
  target="_blank">forbidden responses</a> via API Evangelist guidance.
message: Components has a forbidden response.
severity: info
given: $.components.responses
then:
  field: Forbidden
  function: falsy
```
## Components MUST have a internal server error response. (openapi-components-responses-internal-server-error-error)
Having a internal server error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-internal-server-error.html" target="_blank">internal server error responses</a> via API Evangelist guidance.

```
description: >-
  Having a internal server error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-internal-server-error.html"
  target="_blank">internal server error responses</a> via API Evangelist
  guidance.
message: Components MUST have a internal server error response.
severity: error
given: $.components.responses
then:
  field: InternalServerError
  function: truthy
```
## Components has a internal server error response. (openapi-components-responses-internal-server-error-info)
Having a internal server error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-internal-server-error.html" target="_blank">internal server error responses</a> via API Evangelist guidance.

```
description: >-
  Having a internal server error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-internal-server-error.html"
  target="_blank">internal server error responses</a> via API Evangelist
  guidance.
message: Components has a internal server error response.
severity: info
given: $.components.responses
then:
  field: InternalServerError
  function: falsy
```
## Components MUST have a not found response. (openapi-components-responses-not-found-error)
Having a not found error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-not-found-error.html" target="_blank">not found error responses</a> via API Evangelist guidance.

```
description: >-
  Having a not found error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-not-found-error.html"
  target="_blank">not found error responses</a> via API Evangelist guidance.
message: Components MUST have a not found response.
severity: error
given: $.components.responses
then:
  field: NotFound
  function: truthy
```
## Components has a not found response. (openapi-components-responses-not-found-info)
Having a not found error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-not-found-error.html" target="_blank">not found error responses</a> via API Evangelist guidance.

```
description: >-
  Having a not found error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-not-found-error.html"
  target="_blank">not found error responses</a> via API Evangelist guidance.
message: Components has a not found response.
severity: info
given: $.components.responses
then:
  field: NotFound
  function: falsy
```
## Components MUST have a too many requests response. (openapi-components-responses-too-many-requests-error)
Having a too many requests error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-too-man-requests-error.html" target="_blank">too many requests error responses</a> via API Evangelist guidance.

```
description: >-
  Having a too many requests error responses in the centralized OpenAPI
  components library helps make error responses reusable across API requests.
  Having error responses centralized makes it easier to define, use, but also
  govern and analyze the responses provided across APIs. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-too-man-requests-error.html"
  target="_blank">too many requests error responses</a> via API Evangelist
  guidance.
message: Components MUST have a too many requests response.
severity: error
given: $.components.responses
then:
  field: TooManyRequests
  function: truthy
```
## Components has a too many requests response. (openapi-components-responses-too-many-requests-info)
Having a too many requests error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-too-man-requests-error.html" target="_blank">too many requests error responses</a> via API Evangelist guidance.

```
description: >-
  Having a too many requests error responses in the centralized OpenAPI
  components library helps make error responses reusable across API requests.
  Having error responses centralized makes it easier to define, use, but also
  govern and analyze the responses provided across APIs. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-too-man-requests-error.html"
  target="_blank">too many requests error responses</a> via API Evangelist
  guidance.
message: Components has a too many requests response.
severity: info
given: $.components.responses
then:
  field: TooManyRequests
  function: falsy
```
## Components MUST have a unauthorized response. (openapi-components-responses-unauthorized-error)
Having a unauthorized error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-unauthorized-error.html" target="_blank">unauthorized error responses</a> via API Evangelist guidance.

```
description: >-
  Having a unauthorized error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-unauthorized-error.html"
  target="_blank">unauthorized error responses</a> via API Evangelist guidance.
message: Components MUST have a unauthorized response.
severity: error
given: $.components.responses
then:
  field: Unauthorized
  function: truthy
```
## Components has a unauthorized response. (openapi-components-responses-unauthorized-info)
Having a unauthorized error responses in the centralized OpenAPI components library helps make error responses reusable across API requests. Having error responses centralized makes it easier to define, use, but also govern and analyze the responses provided across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/responses-unauthorized-error.html" target="_blank">unauthorized error responses</a> via API Evangelist guidance.

```
description: >-
  Having a unauthorized error responses in the centralized OpenAPI components
  library helps make error responses reusable across API requests. Having error
  responses centralized makes it easier to define, use, but also govern and
  analyze the responses provided across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  responses object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/responses-unauthorized-error.html"
  target="_blank">unauthorized error responses</a> via API Evangelist guidance.
message: Components has a unauthorized response.
severity: info
given: $.components.responses
then:
  field: Unauthorized
  function: falsy
```
## OpenAPI MUST Have External Documentation (openapi-external-docs-error)
Having an external documentation link present in the OpenAPI for an API, makes it easy for API producers or consumers to find their way to the rest of the operations and resources available around an API. External docs link should take consumers straight to the documentation for whatever API is defined by the OpenAPI, which gets rendered in any services or tooling using the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#external-documentation-object">external docs object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/external-docs.html" target="_blank">external documentation</a> via API Evangelist guidance.

```
description: >-
  Having an external documentation link present in the OpenAPI for an API, makes
  it easy for API producers or consumers to find their way to the rest of the
  operations and resources available around an API. External docs link should
  take consumers straight to the documentation for whatever API is defined by
  the OpenAPI, which gets rendered in any services or tooling using the OpenAPI.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#external-documentation-object">external
  docs object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/external-docs.html"
  target="_blank">external documentation</a> via API Evangelist guidance.
message: OpenAPI MUST Have External Documentation
severity: error
given: $
then:
  field: externalDocs
  function: truthy
```
## OpenAPI Has External Documentation (openapi-external-docs-info)
Having an external documentation link present in the OpenAPI for an API, makes it easy for API producers or consumers to find their way to the rest of the operations and resources available around an API. External docs link should take consumers straight to the documentation for whatever API is defined by the OpenAPI, which gets rendered in any services or tooling using the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#external-documentation-object">external docs object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/external-docs.html" target="_blank">external documentation</a> via API Evangelist guidance.

```
description: >-
  Having an external documentation link present in the OpenAPI for an API, makes
  it easy for API producers or consumers to find their way to the rest of the
  operations and resources available around an API. External docs link should
  take consumers straight to the documentation for whatever API is defined by
  the OpenAPI, which gets rendered in any services or tooling using the OpenAPI.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#external-documentation-object">external
  docs object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/external-docs.html"
  target="_blank">external documentation</a> via API Evangelist guidance.
message: OpenAPI Has External Documentation
severity: info
given: $
then:
  field: externalDocs
  function: falsy
```
## Info MUST Have Contact Email (openapi-info-contact-email-error)
Having a contact email address associated with the technical contract ensures that anyone who comes across the API has someone to email and get more information. Ideally the email is a general email, but in some situations an individual email is acceptable. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact email</a> via API Evangelist guidance.

```
description: >-
  Having a contact email address associated with the technical contract ensures
  that anyone who comes across the API has someone to email and get more
  information. Ideally the email is a general email, but in some situations an
  individual email is acceptable. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact email</a> via API Evangelist guidance.
message: Info MUST Have Contact Email
given: $.info.contact
severity: error
then:
  field: email
  function: truthy
```
## Info Has Contact Email (openapi-info-contact-email-info)
Having a contact email address associated with the technical contract ensures that anyone who comes across the API has someone to email and get more information. Ideally the email is a general email, but in some situations an individual email is acceptable. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact email</a> via API Evangelist guidance.

```
description: >-
  Having a contact email address associated with the technical contract ensures
  that anyone who comes across the API has someone to email and get more
  information. Ideally the email is a general email, but in some situations an
  individual email is acceptable. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact email</a> via API Evangelist guidance.
message: Info Has Contact Email
given: $.info.contact
severity: info
then:
  field: email
  function: falsy
```
## Info MUST Have Contact Object (openapi-info-contact-error)
Having a contact object associated with the technical contract ensures that anyone who comes across the API has someone to contact and get more information. A contact object can nave a name, email, and URL that consumers of the API can use to get more information. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact info</a> via API Evangelist guidance.

```
description: >-
  Having a contact object associated with the technical contract ensures that
  anyone who comes across the API has someone to contact and get more
  information. A contact object can nave a name, email, and URL that consumers
  of the API can use to get more information. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact info</a> via API Evangelist guidance.
message: Info MUST Have Contact Object
severity: error
given: $.info
then:
  field: contact
  function: truthy
```
## Info Has Contact Object (openapi-info-contact-info)
Having a contact object associated with the technical contract ensures that anyone who comes across the API has someone to contact and get more information. A contact object can nave a name, email, and URL that consumers of the API can use to get more information. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact info</a> via API Evangelist guidance.

```
description: >-
  Having a contact object associated with the technical contract ensures that
  anyone who comes across the API has someone to contact and get more
  information. A contact object can nave a name, email, and URL that consumers
  of the API can use to get more information. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact info</a> via API Evangelist guidance.
message: Info Has Contact Object
severity: info
given: $.info
then:
  field: contact
  function: falsy
```
## Info MUST Have Contact Name (openapi-info-contact-name-error)
Having a contact name associated with the technical contract ensures that anyone who comes across the API knows who to contact. Ideally the name is a general domain, line of business, or team name, but in some situations an individual name is acceptable. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact name</a> via API Evangelist guidance.

```
description: >-
  Having a contact name associated with the technical contract ensures that
  anyone who comes across the API knows who to contact. Ideally the name is a
  general domain, line of business, or team name, but in some situations an
  individual name is acceptable. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact name</a> via API Evangelist guidance.
message: Info MUST Have Contact Name
given: $.info.contact
severity: error
then:
  field: name
  function: truthy
```
## Info Has Contact Name (openapi-info-contact-name-info)
Having a contact name associated with the technical contract ensures that anyone who comes across the API knows who to contact. Ideally the name is a general domain, line of business, or team name, but in some situations an individual name is acceptable. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact name</a> via API Evangelist guidance.

```
description: >-
  Having a contact name associated with the technical contract ensures that
  anyone who comes across the API knows who to contact. Ideally the name is a
  general domain, line of business, or team name, but in some situations an
  individual name is acceptable. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact name</a> via API Evangelist guidance.
message: Info Has Contact Name
given: $.info.contact
severity: info
then:
  field: name
  function: falsy
```
## Info MUST Have Contact URL (openapi-info-contact-url-error)
Having a contact url associated with the technical contract ensures that anyone who comes across the API knows where to go to contact someone. The URL could be to a contact form, support page, chat, forum, or other channel. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact url</a> via API Evangelist guidance.

```
description: >-
  Having a contact url associated with the technical contract ensures that
  anyone who comes across the API knows where to go to contact someone. The URL
  could be to a contact form, support page, chat, forum, or other channel. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact url</a> via API Evangelist guidance.
message: Info MUST Have Contact URL
given: $.info.contact
severity: error
then:
  field: url
  function: truthy
```
## Info Has Contact URL (openapi-info-contact-url-info)
Having a contact url associated with the technical contract ensures that anyone who comes across the API knows where to go to contact someone. The URL could be to a contact form, support page, chat, forum, or other channel. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#contact-object">contact object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html" target="_blank">contact url</a> via API Evangelist guidance.

```
description: >-
  Having a contact url associated with the technical contract ensures that
  anyone who comes across the API knows where to go to contact someone. The URL
  could be to a contact form, support page, chat, forum, or other channel. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#contact-object">contact object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-contact.html"
  target="_blank">contact url</a> via API Evangelist guidance.
message: Info Has Contact URL
given: $.info.contact
severity: info
then:
  field: url
  function: falsy
```
## Info MUST Have Description (openapi-info-description-error)
Having a detailed description as part of the OpenAPI info object helps describe what a collection of paths and operations does for consumers, providing a short, concise, and relevant couple of paragraphs about the value that is represented as the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-description.html" target="_blank">OpenAPI info description</a> via API Evangelist guidance.

```
description: >-
  Having a detailed description as part of the OpenAPI info object helps
  describe what a collection of paths and operations does for consumers,
  providing a short, concise, and relevant couple of paragraphs about the value
  that is represented as the OpenAPI. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-description.html"
  target="_blank">OpenAPI info description</a> via API Evangelist guidance.
message: Info MUST Have Description
severity: error
given: $.info
then:
  field: description
  function: truthy
```
## Info Has Description (openapi-info-description-info)
Having a detailed description as part of the OpenAPI info object helps describe what a collection of paths and operations does for consumers, providing a short, concise, and relevant couple of paragraphs about the value that is represented as the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-description.html" target="_blank">OpenAPI info description</a> via API Evangelist guidance.

```
description: >-
  Having a detailed description as part of the OpenAPI info object helps
  describe what a collection of paths and operations does for consumers,
  providing a short, concise, and relevant couple of paragraphs about the value
  that is represented as the OpenAPI. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-description.html"
  target="_blank">OpenAPI info description</a> via API Evangelist guidance.
message: Info Has Description
severity: info
given: $.info
then:
  field: description
  function: falsy
```
## Info description MUST be less than 500 characters. (openapi-info-description-length-error)
Having a restriction on the length of the API description expressed as the OpenAPI info description helps provide constraints for consumers when adding a description, and keeps portals, landing pages, documentation, and discovery results more consistent. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-description.html" target="_blank">OpenAPI info description</a> via API Evangelist guidance.

```
description: >-
  Having a restriction on the length of the API description expressed as the
  OpenAPI info description helps provide constraints for consumers when adding a
  description, and keeps portals, landing pages, documentation, and discovery
  results more consistent. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-description.html"
  target="_blank">OpenAPI info description</a> via API Evangelist guidance.
message: Info description MUST be less than 500 characters.
severity: error
given: $.info
then:
  field: description
  function: length
  functionOptions:
    max: 500
```
## Info Object MUST Exist (openapi-info-error)
Having an info object provides much of the metadata needed for the collection of APIs described in an OpenAPI. Title, description, tags, version, and other properties are available for describing what value APIs provide to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info.html" target="_blank">info object</a> via API Evangelist guidance.

```
description: >-
  Having an info object provides much of the metadata needed for the collection
  of APIs described in an OpenAPI. Title, description, tags, version, and other
  properties are available for describing what value APIs provide to consumers.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info.html"
  target="_blank">info object</a> via API Evangelist guidance.
message: Info Object MUST Exist
severity: error
given: $
then:
  field: info
  function: truthy
```
## Info Object Exists (openapi-info-info)
Having an info object provides much of the metadata needed for the collection of APIs described in an OpenAPI. Title, description, tags, version, and other properties are available for describing what value APIs provide to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info.html" target="_blank">info object</a> via API Evangelist guidance.

```
description: >-
  Having an info object provides much of the metadata needed for the collection
  of APIs described in an OpenAPI. Title, description, tags, version, and other
  properties are available for describing what value APIs provide to consumers.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info.html"
  target="_blank">info object</a> via API Evangelist guidance.
message: Info Object Exists
severity: info
given: $
then:
  field: info
  function: truthy
```
## Info MUST Have License (openapi-info-license-error)
Having a license associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license associated with an OpenAPI using the info licensing property
  ensures that the legal aspects of licensing the API always travel with the
  technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info MUST Have License
severity: error
given: $.info
then:
  field: license
  function: truthy
```
## Info Has License (openapi-info-license-info)
Having a license associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license associated with an OpenAPI using the info licensing property
  ensures that the legal aspects of licensing the API always travel with the
  technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info Has License
severity: info
given: $.info
then:
  field: license
  function: falsy
```
## Info MUST Have CC-BY-NC-SA 4.0 License (openapi-info-license-identifier-cc-by-nc-sa-error)
Having a Create Commons CC BY NC SA license associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a Create Commons CC BY NC SA license associated with an OpenAPI using
  the info licensing property ensures that the legal aspects of licensing the
  API always travel with the technical contract for an API. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info MUST Have CC-BY-NC-SA 4.0 License
given: $.info.license
severity: error
then:
  field: identifier
  function: pattern
  functionOptions:
    match: ^\b(CC-BY-NC-SA-4.0)\b
```
## Info Has CC-BY-NC-SA 4.0 License (openapi-info-license-identifier-cc-by-nc-sa-info)
Having a Create Commons CC BY NC SA license associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a Create Commons CC BY NC SA license associated with an OpenAPI using
  the info licensing property ensures that the legal aspects of licensing the
  API always travel with the technical contract for an API. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info Has CC-BY-NC-SA 4.0 License
given: $.info.license
severity: info
then:
  field: identifier
  function: pattern
  functionOptions:
    match: ^\b(CC-BY-NC-SA-4.0)\b
```
## Info MUST Have License Identifier (openapi-info-license-identifier-error)
Having a license identifier associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license identifier associated with an OpenAPI using the info
  licensing property ensures that the legal aspects of licensing the API always
  travel with the technical contract for an API. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#license-object">license
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info MUST Have License Identifier
given: $.info.license
severity: error
then:
  field: identifier
  function: truthy
```
## Info Has License Identifier (openapi-info-license-identifier-info)
Having a license identifier associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license identifier associated with an OpenAPI using the info
  licensing property ensures that the legal aspects of licensing the API always
  travel with the technical contract for an API. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#license-object">license
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info Has License Identifier
given: $.info.license
severity: info
then:
  field: identifier
  function: falsy
```
## Info MUST Have License Name (openapi-info-license-name-error)
Having a license name associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license name associated with an OpenAPI using the info licensing
  property ensures that the legal aspects of licensing the API always travel
  with the technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info MUST Have License Name
given: $.info.license
severity: error
then:
  field: name
  function: truthy
```
## Info License Name (openapi-info-license-name-info)
Having a license name associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license name associated with an OpenAPI using the info licensing
  property ensures that the legal aspects of licensing the API always travel
  with the technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info License Name
given: $.info.license
severity: info
then:
  field: name
  function: falsy
```
## Info MUST Have License URL (openapi-info-license-url-error)
Having a license url associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license url associated with an OpenAPI using the info licensing
  property ensures that the legal aspects of licensing the API always travel
  with the technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info MUST Have License URL
given: $.info.license
severity: error
then:
  field: url
  function: truthy
```
## Info Has License URL (openapi-info-license-url-info)
Having a license url associated with an OpenAPI using the info licensing property ensures that the legal aspects of licensing the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#license-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-license.html" target="_blank">API license</a> via API Evangelist guidance.

```
description: >-
  Having a license url associated with an OpenAPI using the info licensing
  property ensures that the legal aspects of licensing the API always travel
  with the technical contract for an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#license-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-license.html"
  target="_blank">API license</a> via API Evangelist guidance.
message: Info Has License URL
given: $.info.license
severity: info
then:
  field: url
  function: falsy
```
## Info MUST Have Terms of Service (openapi-info-terms-of-service-error)
Having a terms of service associated with an OpenAPI using the info terms of service property ensures that the legal aspects of legal side of the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-terms-of-service.html" target="_blank">API terms of service</a> via API Evangelist guidance.

```
description: >-
  Having a terms of service associated with an OpenAPI using the info terms of
  service property ensures that the legal aspects of legal side of the API
  always travel with the technical contract for an API. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-terms-of-service.html"
  target="_blank">API terms of service</a> via API Evangelist guidance.
message: Info MUST Have Terms of Service
severity: error
given: $.info
then:
  field: termsOfService
  function: truthy
```
## Info Has Terms of Service (openapi-info-terms-of-service-info)
Having a terms of service associated with an OpenAPI using the info terms of service property ensures that the legal aspects of legal side of the API always travel with the technical contract for an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">license object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-terms-of-service.html" target="_blank">API terms of service</a> via API Evangelist guidance.

```
description: >-
  Having a terms of service associated with an OpenAPI using the info terms of
  service property ensures that the legal aspects of legal side of the API
  always travel with the technical contract for an API. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">license object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-terms-of-service.html"
  target="_blank">API terms of service</a> via API Evangelist guidance.
message: Info Has Terms of Service
severity: info
given: $.info
then:
  field: termsOfService
  function: falsy
```
## Info MUST Have Title (openapi-info-title-error)
Having a intuitive and helpful title for your API using the OpenAPI info title is the first impression you will make on the consumers of your API. Your title should be about what the API does and not how you built the API, focusing on how the consumers will see things. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-title.html" target="_blank">API title</a> via API Evangelist guidance.

```
description: >-
  Having a intuitive and helpful title for your API using the OpenAPI info title
  is the first impression you will make on the consumers of your API. Your title
  should be about what the API does and not how you built the API, focusing on
  how the consumers will see things. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-title.html"
  target="_blank">API title</a> via API Evangelist guidance.
message: Info MUST Have Title
severity: error
given: $.info
then:
  field: title
  function: truthy
```
## Info Has Title (openapi-info-title-info)
Having a intuitive and helpful title for your API using the OpenAPI info title is the first impression you will make on the consumers of your API. Your title should be about what the API does and not how you built the API, focusing on how the consumers will see things. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-title.html" target="_blank">API title</a> via API Evangelist guidance.

```
description: >-
  Having a intuitive and helpful title for your API using the OpenAPI info title
  is the first impression you will make on the consumers of your API. Your title
  should be about what the API does and not how you built the API, focusing on
  how the consumers will see things. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-title.html"
  target="_blank">API title</a> via API Evangelist guidance.
message: Info Has Title
severity: info
given: $.info
then:
  field: title
  function: falsy
```
## Info Title MUST Be Less Than 50 Characters (openapi-info-title-length-error)
Having a limitation on the length of the title for your API helps provide constraints for teams naming it, but also keep consistent with other APIs from across teams. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-title.html" target="_blank">API title length</a> via API Evangelist guidance.

```
description: >-
  Having a limitation on the length of the title for your API helps provide
  constraints for teams naming it, but also keep consistent with other APIs from
  across teams. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-title.html"
  target="_blank">API title length</a> via API Evangelist guidance.
message: Info Title MUST Be Less Than 50 Characters
severity: error
given: $.info
then:
  field: title
  function: length
  functionOptions:
    max: 50
```
## Info Title Has First Characters Capitalized (openapi-info-title-upper-case-error)
Having a consistent casing for the title for your API helps provide constraints for teams naming the API, but also keep consistent with other APIs from across teams. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-title.html" target="_blank">API title casing</a> via API Evangelist guidance.

```
description: >-
  Having a consistent casing for the title for your API helps provide
  constraints for teams naming the API, but also keep consistent with other APIs
  from across teams. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-title.html"
  target="_blank">API title casing</a> via API Evangelist guidance.
message: Info Title Has First Characters Capitalized
severity: error
given: $.info.title
then:
  function: pattern
  functionOptions:
    match: '[A-Z]\w*'
```
## Info Title MUST Have First Characters Capitalized (openapi-info-title-upper-case-info)
Having a consistent casing for the title for your API helps provide constraints for teams naming the API, but also keep consistent with other APIs from across teams. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-title.html" target="_blank">API title casing</a> via API Evangelist guidance.

```
description: >-
  Having a consistent casing for the title for your API helps provide
  constraints for teams naming the API, but also keep consistent with other APIs
  from across teams. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-title.html"
  target="_blank">API title casing</a> via API Evangelist guidance.
message: Info Title MUST Have First Characters Capitalized
severity: info
given: $.info.title
then:
  function: pattern
  functionOptions:
    notMatch: '[A-Z]\w*'
```
## Info MUST Have Version (openapi-info-version-error)
Publishing a version for your OpenAPI technical contract helps you communicate change with consumers using Semantic or date-based versioning published to the info version property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-version.html" target="_blank">API versioning</a> via API Evangelist guidance.

```
description: >-
  Publishing a version for your OpenAPI technical contract helps you communicate
  change with consumers using Semantic or date-based versioning published to the
  info version property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-version.html"
  target="_blank">API versioning</a> via API Evangelist guidance.
message: Info MUST Have Version
given: $.info
severity: error
then:
  field: version
  function: truthy
```
## Info Has Version (openapi-info-version-info)
Publishing a version for your OpenAPI technical contract helps you communicate change with consumers using Semantic or date-based versioning published to the info version property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-version.html" target="_blank">API versioning</a> via API Evangelist guidance.

```
description: >-
  Publishing a version for your OpenAPI technical contract helps you communicate
  change with consumers using Semantic or date-based versioning published to the
  info version property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-version.html"
  target="_blank">API versioning</a> via API Evangelist guidance.
message: Info Has Version
given: $.info
severity: info
then:
  field: version
  function: falsy
```
## Date Versioning (openapi-version-date-info)
Publishing a version for your OpenAPI technical contract helps you communicate change with consumers using date-based versioning published to the info version property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-version.html" target="_blank">API versioning</a> via API Evangelist guidance.

```
description: >-
  Publishing a version for your OpenAPI technical contract helps you communicate
  change with consumers using date-based versioning published to the info
  version property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-version.html"
  target="_blank">API versioning</a> via API Evangelist guidance.
message: Date Versioning
severity: info
given: $.info.version
then:
  function: pattern
  functionOptions:
    notMatch: ^([12]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01]))?$
```
## Semantic Versioning (openapi-version-semantic-info)
Publishing a version for your OpenAPI technical contract helps you communicate change with consumers using Semantic versioning published to the info version property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#info-object">info object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/info-version.html" target="_blank">API versioning</a> via API Evangelist guidance.

```
description: >-
  Publishing a version for your OpenAPI technical contract helps you communicate
  change with consumers using Semantic versioning published to the info version
  property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#info-object">info object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/info-version.html"
  target="_blank">API versioning</a> via API Evangelist guidance.
message: Semantic Versioning
severity: info
given: $.info.version
then:
  function: pattern
  functionOptions:
    notMatch: >-
      ^(0|[1-9][0-9]*)\.(0|[1-9][0-9]*)\.(0|[1-9][0-9]*)(-(0|[1-9A-Za-z-][0-9A-Za-z-]*)(\.[0-9A-Za-z-]+)*)?(\+[0-9A-Za-z-]+(\.[0-9A-Za-z-]+)*)?$      
```
## No API in Path (openapi-no-api-in-path-error)
There are very few situations where you actually want the acronym API in the path of your API. An API is an API, and doesn't need to described as one, leaving the path segments for more meaningful nouns and verbs that impact how consumers will use an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  There are very few situations where you actually want the acronym API in the
  path of your API. An API is an API, and doesn't need to described as one,
  leaving the path segments for more meaningful nouns and verbs that impact how
  consumers will use an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
message: No API in Path
severity: error
given: $.paths.*~
then:
  function: pattern
  functionOptions:
    match: ^\b(API|api)\b
```
## undefined (openapi-no-api-in-path-info)
There are very few situations where you actually want the acronym API in the path of your API. An API is an API, and doesn't need to described as one, leaving the path segments for more meaningful nouns and verbs that impact how consumers will use an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  There are very few situations where you actually want the acronym API in the
  path of your API. An API is an API, and doesn't need to described as one,
  leaving the path segments for more meaningful nouns and verbs that impact how
  consumers will use an API. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
severity: info
given: $.paths.*~
then:
  function: pattern
  functionOptions:
    notMatch: \b(API|api)\b
```
## Path Trailing Slash (openapi-no-path-trailing-slash-error)
It is common to be explicit and consistent about whether or not to have a trailing slack on each API path. This property checks whether or not there is a trailing slash for each of the paths expressed in the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  It is common to be explicit and consistent about whether or not to have a
  trailing slack on each API path. This property checks whether or not there is
  a trailing slash for each of the paths expressed in the OpenAPI. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
message: Path Trailing Slash
severity: error
given: $.paths.*~
then:
  function: pattern
  functionOptions:
    notMatch: /$
```
## Path Trailing Slash (openapi-no-path-trailing-slash-info)
It is common to be explicit and consistent about whether or not to have a trailing slack on each API path. This property checks whether or not there is a trailing slash for each of the paths expressed in the OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  It is common to be explicit and consistent about whether or not to have a
  trailing slack on each API path. This property checks whether or not there is
  a trailing slash for each of the paths expressed in the OpenAPI. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
message: Path Trailing Slash
severity: info
given: $.paths.*~
then:
  function: pattern
  functionOptions:
    match: /$
```
## Version in Path (openapi-version-in-path-error)
The majority of public APIs available on the Web today put the major version of the API as part of the path for each API. Recommended guidance for versioning is to put in headers, but this rules checks whether or not you have in the path. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  The majority of public APIs available on the Web today put the major version
  of the API as part of the path for each API. Recommended guidance for
  versioning is to put in headers, but this rules checks whether or not you have
  in the path. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
message: Version in Path
severity: error
given: $.paths[*]~
then:
  function: pattern
  functionOptions:
    notMatch: /((?:/)(v|version)?[0-9]{1,3}(?:/)?)/i
```
## Version in Path (openapi-version-in-path-info)
The majority of public APIs available on the Web today put the major version of the API as part of the path for each API. Recommended guidance for versioning is to put in headers, but this rules checks whether or not you have in the path. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/paths.html" target="_blank">paths</a> via API Evangelist guidance.

```
description: >-
  The majority of public APIs available on the Web today put the major version
  of the API as part of the path for each API. Recommended guidance for
  versioning is to put in headers, but this rules checks whether or not you have
  in the path. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#paths-object">paths object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/paths.html"
  target="_blank">paths</a> via API Evangelist guidance.
message: Version in Path
severity: info
given: $.paths[*]~
then:
  function: pattern
  functionOptions:
    match: /((?:/)(v|version)?[0-9]{1,3}(?:/)?)/i
```
## Operations MUST Have a Security Definition (openapi-operation-security-definitions-error)
Each API operation should have a security definition referencing the central security scheme express for an OpenAPI. This property configures the gateway for any API being published. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security schemes object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-security.html" target="_blank">operation security</a> via API Evangelist guidance.

```
description: >-
  Each API operation should have a security definition referencing the central
  security scheme express for an OpenAPI. This property configures the gateway
  for any API being published. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security
  schemes object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-security.html"
  target="_blank">operation security</a> via API Evangelist guidance.
message: Operations MUST Have a Security Definition
severity: error
given: $.paths.*[get,post,patch,put,delete]
then:
  field: security
  function: truthy
```
## Operations MUST Have a Security Definition (openapi-operation-security-definitions-info)
Each API operation should have a security definition referencing the central security scheme express for an OpenAPI. This property configures the gateway for any API being published. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security schemes object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-security.html" target="_blank">operation security</a> via API Evangelist guidance.

```
description: >-
  Each API operation should have a security definition referencing the central
  security scheme express for an OpenAPI. This property configures the gateway
  for any API being published. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#security-scheme-object">security
  schemes object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-security.html"
  target="_blank">operation security</a> via API Evangelist guidance.
message: Operations MUST Have a Security Definition
severity: info
given: $.paths.*[get,post,patch,put,delete]
then:
  field: security
  function: falsy
```
## Operation MUST Have Description (openapi-operations-description-error)
Having a paragraph or two description of each API operation helps API consumers understand what is possible with each API request. Keep the description as narrative and plain languge as possible, relying on examples and other operation properties to share the full story. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation descriptions</a> via API Evangelist guidance.

```
description: >-
  Having a paragraph or two description of each API operation helps API
  consumers understand what is possible with each API request. Keep the
  description as narrative and plain languge as possible, relying on examples
  and other operation properties to share the full story. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation descriptions</a> via API Evangelist guidance.
message: Operation MUST Have Description
severity: error
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: description
    function: truthy
```
## Operation Has Description (openapi-operations-description-info)
Having a paragraph or two description of each API operation helps API consumers understand what is possible with each API request. Keep the description as narrative and plain languge as possible, relying on examples and other operation properties to share the full story. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation descriptions</a> via API Evangelist guidance.

```
description: >-
  Having a paragraph or two description of each API operation helps API
  consumers understand what is possible with each API request. Keep the
  description as narrative and plain languge as possible, relying on examples
  and other operation properties to share the full story. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation descriptions</a> via API Evangelist guidance.
message: Operation Has Description
severity: info
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: description
    function: falsy
```
## Operation Description MUST Be Less Than 250 Characters (openapi-operations-description-length-error)
Having a length limitation for each description of each API operation helps apply constraints to how you describe your APIs, while helping drive consistency across APIs when it comes to search, documentation, and other ways an API is made available. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation descriptions</a> via API Evangelist guidance.

```
description: >-
  Having a length limitation for each description of each API operation helps
  apply constraints to how you describe your APIs, while helping drive
  consistency across APIs when it comes to search, documentation, and other ways
  an API is made available. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation descriptions</a> via API Evangelist guidance.
message: Operation Description MUST Be Less Than 250 Characters
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: description
    function: length
    functionOptions:
      max: 250
```
## Operation MUST Have Identifier (openapi-operations-operation-ids-error)
Operation identifiers provide a unique way to identify each individual API, which then used for SDK generation and other automation. The operation identifier for each of your APIs should be unique across your operations. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html" target="_blank">operation identifier</a> via API Evangelist guidance.

```
description: >-
  Operation identifiers provide a unique way to identify each individual API,
  which then used for SDK generation and other automation. The operation
  identifier for each of your APIs should be unique across your operations. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html"
  target="_blank">operation identifier</a> via API Evangelist guidance.
message: Operation MUST Have Identifier
severity: error
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: operationId
    function: truthy
```
## Operation Has Identifier (openapi-operations-operation-ids-info)
Operation identifiers provide a unique way to identify each individual API, which then used for SDK generation and other automation. The operation identifier for each of your APIs should be unique across your operations. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html" target="_blank">operation identifier</a> via API Evangelist guidance.

```
description: >-
  Operation identifiers provide a unique way to identify each individual API,
  which then used for SDK generation and other automation. The operation
  identifier for each of your APIs should be unique across your operations. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html"
  target="_blank">operation identifier</a> via API Evangelist guidance.
message: Operation Has Identifier
severity: info
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: operationId
    function: falsy
```
## Operation Identifier MUST Be camelCase (openapi-operations-operation-ids-camel-case-error)
Operation identifiers provide a unique way to identify each individual API, and requiring them to have consistent casing reduces friction when generating SDKs and automating around APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html" target="_blank">operation identifier</a> via API Evangelist guidance.

```
description: >-
  Operation identifiers provide a unique way to identify each individual API,
  and requiring them to have consistent casing reduces friction when generating
  SDKs and automating around APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html"
  target="_blank">operation identifier</a> via API Evangelist guidance.
message: Operation Identifier MUST Be camelCase
severity: error
given: $.paths.*[get,post,patch,put,delete].operationId
then:
  - function: pattern
    functionOptions:
      notMatch: ^[a-z]+(?:[A-Z][a-z]+)*$
  - function: pattern
    functionOptions:
      match: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Operation Identifier Is camelCase (openapi-operations-operation-ids-camel-case-info)
Operation identifiers provide a unique way to identify each individual API, and requiring them to have consistent casing reduces friction when generating SDKs and automating around APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html" target="_blank">operation identifier</a> via API Evangelist guidance.

```
description: >-
  Operation identifiers provide a unique way to identify each individual API,
  and requiring them to have consistent casing reduces friction when generating
  SDKs and automating around APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-identifier.html"
  target="_blank">operation identifier</a> via API Evangelist guidance.
message: Operation Identifier Is camelCase
severity: info
given: $.paths.*[get,post,patch,put,delete].operationId
then:
  - function: pattern
    functionOptions:
      notMatch: ^[a-z]+(?:[A-Z][a-z]+)*$
  - function: pattern
    functionOptions:
      match: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Operation MUST Have a Summary (openapi-operations-summary-error)
Having short and intuitive summary for each API operation helps API consumers understand what is possible with each API request. Keep the summary reflecting a combination of nouns and verbs that reflect what is possible with each API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation summaries</a> via API Evangelist guidance.

```
description: >-
  Having short and intuitive summary for each API operation helps API consumers
  understand what is possible with each API request. Keep the summary reflecting
  a combination of nouns and verbs that reflect what is possible with each API.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation summaries</a> via API Evangelist guidance.
message: Operation MUST Have a Summary
severity: error
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: summary
    function: truthy
```
## Operation Has a Summary (openapi-operations-summary-info)
Having short and intuitive summary for each API operation helps API consumers understand what is possible with each API request. Keep the summary reflecting a combination of nouns and verbs that reflect what is possible with each API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation summaries</a> via API Evangelist guidance.

```
description: >-
  Having short and intuitive summary for each API operation helps API consumers
  understand what is possible with each API request. Keep the summary reflecting
  a combination of nouns and verbs that reflect what is possible with each API.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation summaries</a> via API Evangelist guidance.
message: Operation Has a Summary
severity: info
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: summary
    function: falsy
```
## Operation Summary MUST Be Less Than 50 Characters (openapi-operations-summary-length-error)
Apply length constraints to the operation summary helps keep them consistent for publishing in documentation. This is something that also should be reflected in the names of the paths used for each operation. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation summaries</a> via API Evangelist guidance.

```
description: >-
  Apply length constraints to the operation summary helps keep them consistent
  for publishing in documentation. This is something that also should be
  reflected in the names of the paths used for each operation. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation summaries</a> via API Evangelist guidance.
message: Operation Summary MUST Be Less Than 50 Characters
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: summary
    function: length
    functionOptions:
      max: 50
type: style
```
## Operation MUST Not Have a Period. (openapi-operations-summary-period-none-error)
Operation summaries should not have a period, keeping the primary summary for each API as consistent as possible for publishing in documentation. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation summaries</a> via API Evangelist guidance.

```
description: >-
  Operation summaries should not have a period, keeping the primary summary for
  each API as consistent as possible for publishing in documentation. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation summaries</a> via API Evangelist guidance.
message: Operation MUST Not Have a Period.
severity: error
given: $.paths[*][*].summary
then:
  function: pattern
  functionOptions:
    notMatch: \.$
```
## Operation Has a Period. (openapi-operations-summary-period-none-info)
Operation summaries should not have a period, keeping the primary summary for each API as consistent as possible for publishing in documentation. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#operation-object">operation object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html" target="_blank">operation summaries</a> via API Evangelist guidance.

```
description: >-
  Operation summaries should not have a period, keeping the primary summary for
  each API as consistent as possible for publishing in documentation. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#operation-object">operation
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-description.html"
  target="_blank">operation summaries</a> via API Evangelist guidance.
message: Operation Has a Period.
severity: info
given: $.paths[*][*].summary
then:
  function: pattern
  functionOptions:
    match: \.$
```
## Operations MUST Have Tags (openapi-operations-tags-error)
Having tags applied to each API operations helps organize and group APIs in portals, documentation, search, and other ways in which APIs are made available. Each API should have at least one tag available describing what the API does for a consumer. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html" target="_blank">operation tags</a> via API Evangelist guidance.

```
description: >-
  Having tags applied to each API operations helps organize and group APIs in
  portals, documentation, search, and other ways in which APIs are made
  available. Each API should have at least one tag available describing what the
  API does for a consumer. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html"
  target="_blank">operation tags</a> via API Evangelist guidance.
message: Operations MUST Have Tags
severity: error
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: tags
    function: truthy
```
## Operations Has Tags (openapi-operations-tags-info)
Having tags applied to each API operations helps organize and group APIs in portals, documentation, search, and other ways in which APIs are made available. Each API should have at least one tag available describing what the API does for a consumer. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html" target="_blank">operation tags</a> via API Evangelist guidance.

```
description: >-
  Having tags applied to each API operations helps organize and group APIs in
  portals, documentation, search, and other ways in which APIs are made
  available. Each API should have at least one tag available describing what the
  API does for a consumer. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html"
  target="_blank">operation tags</a> via API Evangelist guidance.
message: Operations Has Tags
severity: info
given: $.paths.*[get,post,patch,put,delete]
then:
  - field: tags
    function: falsy
```
## MUST Be At Least One Operation Tag (openapi-operations-tags-one-error)
Having tags applied to each API operations helps organize and group APIs in portals, documentation, search, and other ways in which APIs are made available. Each API should have at least one tag available describing what the API does for a consumer. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html" target="_blank">operation tags</a> via API Evangelist guidance.

```
description: >-
  Having tags applied to each API operations helps organize and group APIs in
  portals, documentation, search, and other ways in which APIs are made
  available. Each API should have at least one tag available describing what the
  API does for a consumer. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html"
  target="_blank">operation tags</a> via API Evangelist guidance.
message: MUST Be At Least One Operation Tag
given: $.paths.*[get,post,patch,put,delete]
severity: error
then:
  field: tags
  function: length
  functionOptions:
    min: 1
```
## Operation Tag Names MUST Have First Letter in Each Word Capitalized (openapi-operations-tags-upper-case-error)
Having the first letter of each word applied as a tag to API operations helps keep a consistent layout when published via search, documentation, and other ways APIs are made available. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html" target="_blank">operation tags</a> via API Evangelist guidance.

```
description: >-
  Having the first letter of each word applied as a tag to API operations helps
  keep a consistent layout when published via search, documentation, and other
  ways APIs are made available. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html"
  target="_blank">operation tags</a> via API Evangelist guidance.
message: Operation Tag Names MUST Have First Letter in Each Word Capitalized
severity: error
given: $.paths.*[get,post,patch,put,delete].tags.*
then:
  function: pattern
  functionOptions:
    match: '[A-Z]\w*'
```
## Operation Tag Names Have First Letter in Each Word Capitalized (openapi-operations-tags-upper-case-info)
Having the first letter of each word applied as a tag to API operations helps keep a consistent layout when published via search, documentation, and other ways APIs are made available. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html" target="_blank">operation tags</a> via API Evangelist guidance.

```
description: >-
  Having the first letter of each word applied as a tag to API operations helps
  keep a consistent layout when published via search, documentation, and other
  ways APIs are made available. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-tags.html"
  target="_blank">operation tags</a> via API Evangelist guidance.
message: Operation Tag Names Have First Letter in Each Word Capitalized
severity: info
given: $.paths.*[get,post,patch,put,delete].tags.*
then:
  function: pattern
  functionOptions:
    notMatch: '[A-Z]\w*'
```
## Parameters MUST use components $ref. (openapi-parameters-componentized-error)
Having all parameters using the central OpenAPI components parameters object helps increase the reusability of parameters across API operations, but it also help standardize parameter across all APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-parameters.html" target="_blank">components parameters</a> via API Evangelist guidance.

```
description: >-
  Having all parameters using the central OpenAPI components parameters object
  helps increase the reusability of parameters across API operations, but it
  also help standardize parameter across all APIs. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-parameters.html"
  target="_blank">components parameters</a> via API Evangelist guidance.
message: Parameters MUST use components $ref.
severity: error
resolved: false
given: $.paths.*.*.parameters.*
then:
  field: $ref
  function: truthy
```
## Parameters use components $ref. (openapi-parameters-componentized-info)
Having all parameters using the central OpenAPI components parameters object helps increase the reusability of parameters across API operations, but it also help standardize parameter across all APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#components-object">components object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/components-parameters.html" target="_blank">components parameters</a> via API Evangelist guidance.

```
description: >-
  Having all parameters using the central OpenAPI components parameters object
  helps increase the reusability of parameters across API operations, but it
  also help standardize parameter across all APIs. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#components-object">components
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/components-parameters.html"
  target="_blank">components parameters</a> via API Evangelist guidance.
message: Parameters use components $ref.
severity: info
resolved: false
given: $.paths.*.*.parameters.*
then:
  field: $ref
  function: falsy
```
## DELETE Request Body (openapi-no-request-body-on-delete-error)
DELETE HTTP methods should not have a request body, keeping API requests compliant with the HTTP standard. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request-bodies</a> via API Evangelist guidance.

```
description: >-
  DELETE HTTP methods should not have a request body, keeping API requests
  compliant with the HTTP standard. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request-bodies</a> via API Evangelist guidance.
message: DELETE Request Body
given: $.paths.*.delete
severity: error
then:
  field: requestBody
  function: falsy
```
## DELETE Request Body (openapi-no-request-body-on-delete-info)
DELETE HTTP methods should not have a request body, keeping API requests compliant with the HTTP standard. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request-bodies</a> via API Evangelist guidance.

```
description: >-
  DELETE HTTP methods should not have a request body, keeping API requests
  compliant with the HTTP standard. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request-bodies</a> via API Evangelist guidance.
message: DELETE Request Body
given: $.paths.*.delete
severity: info
then:
  field: requestBody
  function: truthy
```
## GET Request Body (openapi-no-request-body-on-get-error)
GET HTTP methods should not have a request body, keeping API requests compliant with the HTTP standard. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request-bodies</a> via API Evangelist guidance.

```
description: >-
  GET HTTP methods should not have a request body, keeping API requests
  compliant with the HTTP standard. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request-bodies</a> via API Evangelist guidance.
message: GET Request Body
given: $.paths.*.get
severity: error
then:
  field: requestBody
  function: falsy
```
## GET Request Body (openapi-no-request-body-on-get-info)
GET HTTP methods should not have a request body, keeping API requests compliant with the HTTP standard. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request-bodies</a> via API Evangelist guidance.

```
description: >-
  GET HTTP methods should not have a request body, keeping API requests
  compliant with the HTTP standard. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request-bodies</a> via API Evangelist guidance.
message: GET Request Body
given: $.paths.*.get
severity: info
then:
  field: requestBody
  function: truthy
```
## Request Bodies MUST Have a Description (openapi-request-bodies-description-error)
It is helpful to provide a description for request bodies, providing a simple explanation of what can be configured as part of the request payload.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  It is helpful to provide a description for request bodies, providing a simple
  explanation of what can be configured as part of the request payload.  You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Bodies MUST Have a Description
severity: error
given: $.paths.*.requestBody
then:
  field: description
  function: truthy
```
## Request Bodies Have a Description (openapi-request-bodies-description-info)
It is helpful to provide a description for request bodies, providing a simple explanation of what can be configured as part of the request payload.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  It is helpful to provide a description for request bodies, providing a simple
  explanation of what can be configured as part of the request payload.  You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Bodies Have a Description
severity: info
given: $.paths.*.requestBody
then:
  field: description
  function: falsy
```
## REQUEST BODIES Required (openapi-request-bodies-required-property-error)
It is important to be explicit about whether or not the request body for an API operation is required or not.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  It is important to be explicit about whether or not the request body for an
  API operation is required or not.  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: REQUEST BODIES Required
severity: error
given: $.paths.*.requestBody
then:
  field: required
  function: falsy
```
## REQUEST BODIES Required (openapi-request-bodies-required-property-info)
It is important to be explicit about whether or not the request body for an API operation is required or not.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  It is important to be explicit about whether or not the request body for an
  API operation is required or not.  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: REQUEST BODIES Required
severity: info
given: $.paths.*.requestBody
then:
  field: required
  function: truthy
```
## Request Body Content POST (openapi-request-body-content-on-post-error)
POST requests with a request body should have content defined, providing more detail on what is contained within the API request body. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST requests with a request body should have content defined, providing more
  detail on what is contained within the API request body. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Content POST
given: $.paths.*.post.requestBody
severity: error
then:
  field: content
  function: truthy
```
## Request Body Content POST (openapi-request-body-content-on-post-info)
POST requests with a request body should have content defined, providing more detail on what is contained within the API request body. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST requests with a request body should have content defined, providing more
  detail on what is contained within the API request body. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Content POST
given: $.paths.*.post.requestBody
severity: info
then:
  field: content
  function: falsy
```
## Request Body Content PUT (openapi-request-body-content-on-put-error)
PUT requests with a request body should have content defined, providing more detail on what is contained within the API request body. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  PUT requests with a request body should have content defined, providing more
  detail on what is contained within the API request body. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Content PUT
given: $.paths.*.put.requestBody
severity: error
then:
  field: content
  function: truthy
```
## Request Body Content PUT (openapi-request-body-content-on-put-info)
PUT requests with a request body should have content defined, providing more detail on what is contained within the API request body. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  PUT requests with a request body should have content defined, providing more
  detail on what is contained within the API request body. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Content PUT
given: $.paths.*.put.requestBody
severity: info
then:
  field: content
  function: falsy
```
## Request Body Application JSON (openapi-request-body-have-application-json-info)
Request bodies use the application/json media type to encode the request payload is a common data format. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-media-type.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  Request bodies use the application/json media type to encode the request
  payload is a common data format. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-media-type.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Application JSON
given: $.paths.*.*.requestBody.content
severity: info
then:
  field: application/json
  function: falsy
```
## Request Body Application X WWW Form URL Encoded (openapi-request-body-have-application-x-www-form-url-encoded-info)
Request bodies use the application/x-www-form-urlencoded media type to encode the request payload is a common data format. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-media-type.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  Request bodies use the application/x-www-form-urlencoded media type to encode
  the request payload is a common data format. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-media-type.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Application X WWW Form URL Encoded
given: $.paths.*.*.requestBody.content
severity: info
then:
  field: application/x-www-form-urlencoded
  function: falsy
```
## Request Body Schema (openapi-request-body-have-schema-error)
POST, PUT, and PATCH request bodies should have schema defined, providing more detail on what the structure of the API request body should be. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have schema defined, providing more
  detail on what the structure of the API request body should be. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Schema
given: $.paths.*.*.requestBody.content.*
severity: error
then:
  field: schema
  function: truthy
```
## Request Body Schema (openapi-request-body-have-schema-info)
POST, PUT, and PATCH request bodies should have schema defined, providing more detail on what the structure of the API request body should be. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have schema defined, providing more
  detail on what the structure of the API request body should be. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Body Schema
given: $.paths.*.*.requestBody.content.*
severity: info
then:
  field: schema
  function: falsy
```
## Request Bodies MUST Use Schema Reference (openapi-request-body-have-schema-ref-error)
POST, PUT, and PATCH request bodies should have schema reference defined, providing more detail on what the structure of the API request body should be. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have schema reference defined,
  providing more detail on what the structure of the API request body should be.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Bodies MUST Use Schema Reference
severity: error
given: $.paths.*.*.requestBody.content.*.schema
then:
  field: $ref
  function: falsy
```
## Request Bodies Use Schema Reference (openapi-request-body-have-schema-ref-info)
POST, PUT, and PATCH request bodies should have schema reference defined, providing more detail on what the structure of the API request body should be. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have schema reference defined,
  providing more detail on what the structure of the API request body should be.
  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: Request Bodies Use Schema Reference
severity: info
given: $.paths.*.*.requestBody.content.*.schema
then:
  field: $ref
  function: truthy
```
## Request Bodies MUST Have Examples (openapi-request-body-have-examples-error)
POST, PUT, and PATCH request bodies should have examples, providing one or more examples of what should be submitted for different types of requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies examples</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have examples, providing one or
  more examples of what should be submitted for different types of requests. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies examples</a> via API Evangelist guidance.
message: Request Bodies MUST Have Examples
given: $.paths.*.*.requestBody.content.*
severity: error
then:
  field: examples
  function: truthy
```
## Request Bodies Have Examples (openapi-request-body-have-examples-info)
POST, PUT, and PATCH request bodies should have examples, providing one or more examples of what should be submitted for different types of requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies examples</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have examples, providing one or
  more examples of what should be submitted for different types of requests. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies examples</a> via API Evangelist guidance.
message: Request Bodies Have Examples
given: $.paths.*.*.requestBody.content.*
severity: info
then:
  field: examples
  function: falsy
```
## Request Bodies MUST Use Examples Reference (openapi-request-body-have-examples-ref-error)
POST, PUT, and PATCH request bodies should have examples using references to centralized component examples, providing one or more examples of what should be submitted for different types of requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies examples</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have examples using references to
  centralized component examples, providing one or more examples of what should
  be submitted for different types of requests. You can find details about the
  <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies examples</a> via API Evangelist guidance.
message: Request Bodies MUST Use Examples Reference
severity: error
given: $.paths.*.*.requestBody.content.*.examples
then:
  field: $ref
  function: falsy
```
## Request Bodies Use Examples Reference (openapi-request-body-have-examples-ref-info)
POST, PUT, and PATCH request bodies should have examples using references to centralized component examples, providing one or more examples of what should be submitted for different types of requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request body object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html" target="_blank">request bodies examples</a> via API Evangelist guidance.

```
description: >-
  POST, PUT, and PATCH request bodies should have examples using references to
  centralized component examples, providing one or more examples of what should
  be submitted for different types of requests. You can find details about the
  <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  body object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-request-bodies-schema.html"
  target="_blank">request bodies examples</a> via API Evangelist guidance.
message: Request Bodies Use Examples Reference
severity: info
given: $.paths.*.*.requestBody.content.*.examples
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 200 Status Codes (openapi-response-get-200-status-code-error)
GET responses should have a 200 success HTTP status codes, communicating a successful response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 200 success HTTP status codes, communicating a
  successful response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 200 Status Codes
severity: error
given: $.paths.*.get.responses
then:
  field: '200'
  function: truthy
```
## GET Responses Has 200 Status Codes (openapi-response-get-200-status-code-info)
GET responses should have a 200 success HTTP status codes, communicating a successful response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 200 success HTTP status codes, communicating a
  successful response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET Responses Has 200 Status Codes
severity: info
given: $.paths.*.get.responses
then:
  field: '200'
  function: falsy
```
## GET 200 Response MUST have description. (openapi-response-get-200-description-error)
GET 200 success HTTP status codes should have a description, describing what an API consumer can expect as a result. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes should have a description, describing what
  an API consumer can expect as a result. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET 200 Response MUST have description.
severity: error
given: $.paths.*.get.responses.200
then:
  field: description
  function: truthy
```
## GET 200 Response has description. (openapi-response-get-200-description-info)
GET 200 success HTTP status codes should have a description, describing what an API consumer can expect as a result. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes should have a description, describing what
  an API consumer can expect as a result. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET 200 Response has description.
severity: info
given: $.paths.*.get.responses.200
then:
  field: description
  function: falsy
```
## GET 200 Response MUST Have Content. (openapi-response-get-200-content-error)
GET 200 success HTTP status codes should have content property that provides the ability to describe the response content. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes should have content property that provides
  the ability to describe the response content. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET 200 Response MUST Have Content.
severity: error
given: $.paths.*.get.responses.200
then:
  field: content
  function: truthy
```
## GET 200 Response Has Content. (openapi-response-get-200-content-info)
GET 200 success HTTP status codes should have content property that provides the ability to describe the response content. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes should have content property that provides
  the ability to describe the response content. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: GET 200 Response Has Content.
severity: info
given: $.paths.*.get.responses.200
then:
  field: content
  function: falsy
```
## GET 200 Response MUST Have Media Type. (openapi-response-get-200-media-type-error)
GET 200 success HTTP status codes have a application/json media type, standardizing the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html" target="_blank">operation 2xx media types</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a application/json media type,
  standardizing the response payload returned for a successful response. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html"
  target="_blank">operation 2xx media types</a> via API Evangelist guidance.
message: GET 200 Response MUST Have Media Type.
severity: error
given: $.paths.*.get.responses.200.content
then:
  field: application/json
  function: truthy
```
## GET 200 Response Has Media Type. (openapi-response-get-200-media-type-info)
GET 200 success HTTP status codes have a application/json media type, standardizing the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html" target="_blank">operation 2xx media types</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a application/json media type,
  standardizing the response payload returned for a successful response. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html"
  target="_blank">operation 2xx media types</a> via API Evangelist guidance.
message: GET 200 Response Has Media Type.
severity: info
given: $.paths.*.get.responses.200.content
then:
  field: application/json
  function: falsy
```
## GET 200 Response MUST Have Schema (openapi-response-get-200-media-type-schema-error)
GET 200 success HTTP status codes have a schema to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a schema to standardize the response
  payload returned for a successful response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: GET 200 Response MUST Have Schema
severity: error
given: $.paths.*.get.responses.200.content['application/json']
then:
  field: schema
  function: truthy
```
## GET 200 Response Has Schema (openapi-response-get-200-media-type-schema-info)
GET 200 success HTTP status codes have a schema to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a schema to standardize the response
  payload returned for a successful response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: GET 200 Response Has Schema
severity: info
given: $.paths.*.get.responses.200.content['application/json']
then:
  field: schema
  function: falsy
```
## GET 200 Responses MUST Use Schema Reference (openapi-response-get-200-media-type-schema-ref-error)
GET 200 success HTTP status codes have a schema references to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a schema references to standardize the
  response payload returned for a successful response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: GET 200 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.200.content['application/json'].schema
then:
  field: $ref
  function: falsy
```
## GET 200 Responses Uses Schema Reference (openapi-response-get-200-media-type-schema-ref-info)
GET 200 success HTTP status codes have a schema references to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have a schema references to standardize the
  response payload returned for a successful response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: GET 200 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.200.content['application/json'].schema
then:
  field: $ref
  function: truthy
```
## GET 200 Response MUST Have Examples (openapi-response-get-200-media-type-examples-error)
GET 200 success HTTP status codes have examples to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have examples to show one or many examples
  of responses for different types of API requests. You can find details about
  the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: GET 200 Response MUST Have Examples
severity: error
given: $.paths.*.get.responses.200.content['application/json']
then:
  field: examples
  function: truthy
```
## GET 200 ResponseHas Examples (openapi-response-get-200-media-type-examples-info)
GET 200 success HTTP status codes have examples to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have examples to show one or many examples
  of responses for different types of API requests. You can find details about
  the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: GET 200 ResponseHas Examples
severity: info
given: $.paths.*.get.responses.200.content['application/json']
then:
  field: examples
  function: falsy
```
## GET 200 Responses MUST Use Examples Reference (openapi-response-get-200-media-type-examples-ref-error)
GET 200 success HTTP status codes have example references to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have example references to show one or many
  examples of responses for different types of API requests. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: GET 200 Responses MUST Use Examples Reference
severity: error
given: $.paths.*.get.responses.200.content['application/json'].examples.*
then:
  field: $ref
  function: falsy
```
## GET 200 Responses Uses Examples Reference (openapi-response-get-200-media-type-examples-ref-info)
GET 200 success HTTP status codes have example references to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  GET 200 success HTTP status codes have example references to show one or many
  examples of responses for different types of API requests. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: GET 200 Responses Uses Examples Reference
severity: info
given: $.paths.*.get.responses.200.content['application/json'].examples.*
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 400 Status Codes (openapi-response-get-400-status-code-error)
GET responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 400 Status Codes
severity: error
given: $.paths.*.get.responses
then:
  field: '400'
  function: truthy
```
## GET Responses Has 400 Status Codes (openapi-response-get-400-status-code-info)
GET responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 400 Status Codes
severity: info
given: $.paths.*.get.responses
then:
  field: '400'
  function: falsy
```
## GET 400 Responses MUST Use Schema Reference (openapi-response-get-400-schema-ref-error)
GET 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 400 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.400
then:
  field: $ref
  function: falsy
```
## GET 400 Responses Uses Schema Reference (openapi-response-get-400-schema-ref-info)
GET 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 400 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.400
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 401 Status Code (openapi-response-get-401-status-code-info)
GET responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 401 Status Code
severity: info
given: $.paths.*.get.responses
then:
  field: '401'
  function: falsy
```
## GET Responses Has 401 Status Code (openapi-response-get-401-status-code-error)
GET responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 401 Status Code
severity: error
given: $.paths.*.get.responses
then:
  field: '401'
  function: truthy
```
## GET 401 Responses MUST Use Schema Reference (openapi-response-get-401-schema-ref-error)
GET 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 401 unauthorized HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 401 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.401
then:
  field: $ref
  function: falsy
```
## GET 401 Responses Has Schema Reference (openapi-response-get-401-schema-ref-info)
GET 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 401 unauthorized HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 401 Responses Has Schema Reference
severity: info
given: $.paths.*.get.responses.401
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 403 Status Code (openapi-response-get-403-status-code-info)
GET responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 403 forbidden HTTP status code, communicating that
  consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 403 Status Code
severity: info
given: $.paths.*.get.responses
then:
  field: '403'
  function: falsy
```
## GET Responses Has 403 Status Code (openapi-response-get-403-status-code-error)
GET responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 403 forbidden HTTP status code, communicating that
  consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 403 Status Code
severity: error
given: $.paths.*.get.responses
then:
  field: '403'
  function: truthy
```
## GET 403 Responses MUST Use Schema Reference (openapi-response-get-403-schema-ref-error)
GET 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 403 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.403
then:
  field: $ref
  function: falsy
```
## GET 403 Responses Uses Schema Reference (openapi-response-get-403-schema-ref-info)
GET 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 403 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.403
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 404 Status Code (openapi-response-get-404-status-code-error)
GET responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 404 not found HTTP status code, communicating that
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 404 Status Code
severity: error
given: $.paths.*.get[?(@.properties)]
then:
  field: '404'
  function: truthy
```
## GET Responses Has 404 Status Code (openapi-response-get-404-status-code-info)
GET responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 404 not found HTTP status code, communicating that
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 404 Status Code
severity: info
given: $.paths.*.get[?(@.properties)]
then:
  field: '404'
  function: falsy
```
## GET 404 Responses MUST Use Schema Reference (openapi-response-get-404-schema-ref-error)
GET 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 404 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.404
then:
  field: $ref
  function: falsy
```
## GET 404 Responses Uses Schema Reference (openapi-response-get-404-schema-ref-info)
GET 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 404 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.404
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 429 Status Code (openapi-response-get-429-status-code-info)
GET responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 429 Status Code
severity: info
given: $.paths.*.get.responses
then:
  field: '429'
  function: falsy
```
## GET Responses Has 429 Status Code (openapi-response-get-429-status-code-error)
GET responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 429 Status Code
severity: error
given: $.paths.*.get.responses
then:
  field: '429'
  function: truthy
```
## GET 429 Responses MUST Use Schema Reference (openapi-response-get-429-schema-ref-error)
GET 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 429 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.429
then:
  field: $ref
  function: falsy
```
## GET 429 Responses Uses Schema Reference (openapi-response-get-429-schema-ref-info)
GET 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: GET 429 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.429
then:
  field: $ref
  function: truthy
```
## GET Responses MUST Have 500 Status Code (openapi-response-get-500-status-code-error)
GET responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses MUST Have 500 Status Code
severity: error
given: $.paths.*.get.responses
then:
  field: '500'
  function: truthy
```
## GET Responses Has 500 Status Code (openapi-response-get-500-status-code-info)
GET responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  GET responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: GET Responses Has 500 Status Code
severity: info
given: $.paths.*.get.responses
then:
  field: '500'
  function: falsy
```
## GET 500 Responses MUST Use Schema Reference (openapi-response-get-500-schema-ref-error)
GET 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: GET 500 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.get.responses.500
then:
  field: $ref
  function: falsy
```
## GET 500 Responses Uses Schema Reference (openapi-response-get-500-schema-ref-info)
GET 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  GET 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: GET 500 Responses Uses Schema Reference
severity: info
given: $.paths.*.get.responses.500
then:
  field: $ref
  function: truthy
```
## POST Requests MUST Have a Body (openapi-request-body-on-post-error)
POST HTTP methods can have a request body, providing a structured payload for configuring each API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST HTTP methods can have a request body, providing a structured payload for
  configuring each API request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: POST Requests MUST Have a Body
given: $.paths.*.post
severity: error
then:
  field: requestBody
  function: truthy
```
## POST Requests Has a Body (openapi-request-body-on-post-info)
POST HTTP methods can have a request body, providing a structured payload for configuring each API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  POST HTTP methods can have a request body, providing a structured payload for
  configuring each API request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: POST Requests Has a Body
given: $.paths.*.post
severity: info
then:
  field: requestBody
  function: falsy
```
## POST Responses MUST Have 201 Status Codes (openapi-response-post-201-status-code-error)
POST responses should have a 201 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 201 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 201 Status Codes
severity: error
given: $.paths[*].post.responses
then:
  field: '201'
  function: truthy
```
## POST Responses Has 201 Status Codes (openapi-response-post-201-status-code-info)
POST responses should have a 201 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 201 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST Responses Has 201 Status Codes
severity: info
given: $.paths[*].post.responses
then:
  field: '201'
  function: falsy
```
## POST 201 Responses MUST Have Description (openapi-response-post-201-description-error)
POST 201 success HTTP status codes should have a description, describing what an API consumer can expect as a result. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes should have a description, describing what
  an API consumer can expect as a result. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST 201 Responses MUST Have Description
severity: error
given: $.paths.*.post.responses.201
then:
  field: description
  function: truthy
```
## POST 201 Responses Has Description (openapi-response-post-201-description-info)
POST 201 success HTTP status codes should have a description, describing what an API consumer can expect as a result. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes should have a description, describing what
  an API consumer can expect as a result. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST 201 Responses Has Description
severity: info
given: $.paths.*.post.responses.201
then:
  field: description
  function: falsy
```
## POST 201 Responses MUST Have Content (openapi-response-post-201-content-error)
POST 201 success HTTP status codes should have content property that provides the ability to describe the response content. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes should have content property that provides
  the ability to describe the response content. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST 201 Responses MUST Have Content
severity: error
given: $.paths.*.post.responses.201
then:
  field: content
  function: truthy
```
## POST 201 Responses Has Content (openapi-response-post-201-content-info)
POST 201 success HTTP status codes should have content property that provides the ability to describe the response content. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes should have content property that provides
  the ability to describe the response content. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: POST 201 Responses Has Content
severity: info
given: $.paths.*.post.responses.201
then:
  field: content
  function: falsy
```
## POST 201 Responses MUST Have Media Type (openapi-response-post-201-media-type-error)
POST 201 success HTTP status codes have a application/json media type, standardizing the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html" target="_blank">operation 2xx media types</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a application/json media type,
  standardizing the response payload returned for a successful response. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html"
  target="_blank">operation 2xx media types</a> via API Evangelist guidance.
message: POST 201 Responses MUST Have Media Type
severity: error
given: $.paths.*.post.responses.201.content
then:
  field: application/json
  function: truthy
```
## POST 201 Responses Has Media Type (openapi-response-post-201-media-type-info)
POST 201 success HTTP status codes have a application/json media type, standardizing the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html" target="_blank">operation 2xx media types</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a application/json media type,
  standardizing the response payload returned for a successful response. You can
  find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-media-types.html"
  target="_blank">operation 2xx media types</a> via API Evangelist guidance.
message: POST 201 Responses Has Media Type
severity: info
given: $.paths.*.post.responses.201.content
then:
  field: application/json
  function: falsy
```
## POST 201 Responses MUST Have Schema (openapi-response-post-201-media-type-schema-error)
POST 201 success HTTP status codes have a schema to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a schema to standardize the response
  payload returned for a successful response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: POST 201 Responses MUST Have Schema
severity: error
given: $.paths.*.post.responses.201.content.application/json
then:
  field: schema
  function: truthy
```
## POST 201 Responses Has Schema (openapi-response-post-201-media-type-schema-info)
POST 201 success HTTP status codes have a schema to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a schema to standardize the response
  payload returned for a successful response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: POST 201 Responses Has Schema
severity: info
given: $.paths.*.post.responses.201.content.application/json
then:
  field: schema
  function: falsy
```
## POST 201 Responses MUST Use Schema Reference (openapi-response-post-201-schema-ref-error)
POST 201 success HTTP status codes have a schema references to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a schema references to standardize the
  response payload returned for a successful response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: POST 201 Responses MUST Use Schema Reference
given: $.paths.*.post.responses.201.content.*.schema
severity: error
then:
  field: $ref
  function: falsy
```
## POST 201 Responses Has Schema Reference (openapi-response-post-201-schema-ref-info)
POST 201 success HTTP status codes have a schema references to standardize the response payload returned for a successful response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html" target="_blank">operation 2xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have a schema references to standardize the
  response payload returned for a successful response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-schema.html"
  target="_blank">operation 2xx schema</a> via API Evangelist guidance.
message: POST 201 Responses Has Schema Reference
given: $.paths.*.post.responses.201.content.*.schema
severity: info
then:
  field: $ref
  function: truthy
```
## POST 201 Responses MUST Have Examples (openapi-response-post-201-media-type-examples-error)
POST 201 success HTTP status codes have examples to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have examples to show one or many examples
  of responses for different types of API requests. You can find details about
  the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: POST 201 Responses MUST Have Examples
severity: error
given: $.paths.*.post.responses.201.content.application/json
then:
  field: examples
  function: truthy
```
## POST 201 Responses Has Examples (openapi-response-post-201-media-type-examples-info)
POST 201 success HTTP status codes have examples to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have examples to show one or many examples
  of responses for different types of API requests. You can find details about
  the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: POST 201 Responses Has Examples
severity: info
given: $.paths.*.post.responses.201.content.application/json
then:
  field: examples
  function: falsy
```
## POST 201 Responses MUST Use Examples Reference (openapi-response-post-201-examples-ref-error)
POST 201 success HTTP status codes have example references to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have example references to show one or many
  examples of responses for different types of API requests. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: POST 201 Responses MUST Use Examples Reference
given: $.paths.*.post.responses.201.content.*.examples
severity: error
then:
  field: $ref
  function: falsy
```
## POST 201 Responses Has Examples Reference (openapi-response-post-201-examples-ref-info)
POST 201 success HTTP status codes have example references to show one or many examples of responses for different types of API requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html" target="_blank">operation 2xx examples</a> via API Evangelist guidance.

```
description: >-
  POST 201 success HTTP status codes have example references to show one or many
  examples of responses for different types of API requests. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx-examples.html"
  target="_blank">operation 2xx examples</a> via API Evangelist guidance.
message: POST 201 Responses Has Examples Reference
given: $.paths.*.post.responses.201.content.*.examples
severity: info
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 400 Status Codes (openapi-response-post-400-status-code-info)
POST responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 400 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '400'
  function: falsy
```
## POST Responses Has 400 Status Codes (openapi-response-post-400-status-code-error)
POST responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 400 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '400'
  function: truthy
```
## POST 400 Responses MUST Use Schema Reference (openapi-response-post-400-schema-ref-error)
POST 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 400 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.400
then:
  field: $ref
  function: falsy
```
## POST 400 Responses Uses Schema Reference (openapi-response-post-400-schema-ref-info)
POST 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 400 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.400
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 401 Status Codes (openapi-response-post-401-status-code-info)
POST responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 401 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '401'
  function: falsy
```
## POST Responses Has 401 Status Codes (openapi-response-post-401-status-code-error)
POST responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 401 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '401'
  function: truthy
```
## POST 401 Responses MUST Use Schema Reference (openapi-response-post-401-schema-ref-error)
POST 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 401 unauthorized HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 401 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.401
then:
  field: $ref
  function: falsy
```
## POST 401 Responses Uses Schema Reference (openapi-response-post-401-schema-ref-info)
POST 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 401 unauthorized HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 401 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.401
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 403 Status Codes (openapi-response-post-403-status-code-info)
POST responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 403 forbidden HTTP status code, communicating
  that consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 403 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '403'
  function: falsy
```
## POST Responses Has 403 Status Codes (openapi-response-post-403-status-code-error)
POST responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 403 forbidden HTTP status code, communicating
  that consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 403 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '403'
  function: truthy
```
## POST 403 Responses MUST Use Schema Reference (openapi-response-post-403-schema-ref-error)
POST 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 403 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.403
then:
  field: $ref
  function: falsy
```
## POST 403 Responses Uses Schema Reference (openapi-response-post-403-schema-ref-info)
POST 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 403 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.403
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 404 Status Codes (openapi-response-post-404-status-code-info)
POST responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 404 not found HTTP status code, communicating
  that nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 404 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '404'
  function: falsy
```
## POST Responses Has 404 Status Codes (openapi-response-post-404-status-code-error)
POST responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 404 not found HTTP status code, communicating
  that nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 404 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '404'
  function: truthy
```
## POST 404 Responses MUST Use Schema Reference (openapi-response-post-404-schema-ref-error)
POST 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 404 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.404
then:
  field: $ref
  function: falsy
```
## POST 404 Responses Uses Schema Reference (openapi-response-post-404-schema-ref-info)
POST 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 404 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.404
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 429 Status Codes (openapi-response-post-429-status-code-error)
POST responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 429 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '429'
  function: truthy
```
## POST Responses Has 429 Status Codes (openapi-response-post-429-status-code-info)
POST responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 429 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '429'
  function: falsy
```
## POST 429 Responses MUST Use Schema Reference (openapi-response-post-429-schema-ref-error)
POST 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 429 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.429
then:
  field: $ref
  function: falsy
```
## POST 429 Responses Uses Schema Reference (openapi-response-post-429-schema-ref-info)
POST 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: POST 429 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.429
then:
  field: $ref
  function: truthy
```
## POST Responses MUST Have 500 Status Codes (openapi-response-post-500-status-code-error)
POST responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses MUST Have 500 Status Codes
severity: error
given: $.paths.*.post.responses
then:
  field: '500'
  function: truthy
```
## POST Responses Has 500 Status Codes (openapi-response-post-500-status-code-info)
POST responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  POST responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: POST Responses Has 500 Status Codes
severity: info
given: $.paths.*.post.responses
then:
  field: '500'
  function: falsy
```
## POST 500 Responses MUST Use Schema Reference (openapi-response-post-500-schema-ref-error)
POST 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: POST 500 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.post.responses.500
then:
  field: $ref
  function: falsy
```
## POST 500 Responses Uses Schema Reference (openapi-response-post-500-schema-ref-info)
POST 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  POST 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: POST 500 Responses Uses Schema Reference
severity: info
given: $.paths.*.post.responses.500
then:
  field: $ref
  function: truthy
```
## PUT Requests MUST Have a Body (openapi-request-body-on-put-error-info)
PUT HTTP methods can have a request body, providing a structured payload for configuring each API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  PUT HTTP methods can have a request body, providing a structured payload for
  configuring each API request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: PUT Requests MUST Have a Body
given: $.paths.*.put
severity: error
then:
  field: requestBody
  function: truthy
```
## PUT Requests Has a Body (openapi-request-body-on-put-info)
PUT HTTP methods can have a request body, providing a structured payload for configuring each API request. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#request-body-object">request bodies object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html" target="_blank">request bodies</a> via API Evangelist guidance.

```
description: >-
  PUT HTTP methods can have a request body, providing a structured payload for
  configuring each API request. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#request-body-object">request
  bodies object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/request-bodies.html"
  target="_blank">request bodies</a> via API Evangelist guidance.
message: PUT Requests Has a Body
given: $.paths.*.put
severity: error
then:
  field: requestBody
  function: falsy
```
## PUT 204 Status Code (openapi-response-put-204-status-code-error)
PUT responses should have a 204 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 204 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: PUT 204 Status Code
severity: error
given: $.paths.*.put.responses
then:
  field: '204'
  function: truthy
```
## PUT 204 Status Code (openapi-response-put-204-status-code-info)
PUT responses should have a 204 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 204 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: PUT 204 Status Code
severity: info
given: $.paths.*.put.responses
then:
  field: '204'
  function: falsy
```
## PUT Responses MUST Have 400 Status Codes (openapi-response-put-400-status-code-error)
PUT responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST Have 400 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '400'
  function: truthy
```
## PUT Responses Has 400 Status Codes (openapi-response-put-400-status-code-info)
PUT responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 400 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '400'
  function: falsy
```
## PUT 400 Responses MUST Use Schema Reference (openapi-response-put-400-schema-ref-error)
PUT 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 400 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.400
then:
  field: $ref
  function: falsy
```
## PUT 400 Responses Uses Schema Reference (openapi-response-put-400-schema-ref-info)
PUT 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 400 bad request HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 400 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.400
then:
  field: $ref
  function: truthy
```
## PUT Responses MUST 401 Status Codes (openapi-response-put-401-status-code-error)
PUT responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST 401 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '401'
  function: truthy
```
## PUT Responses Has 401 Status Codes (openapi-response-put-401-status-code-info)
PUT responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 401 unauthorized HTTP status code, communicating
  that consumers do not have access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 401 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '401'
  function: falsy
```
## PUT 401 Responses MUST Use Schema Reference (openapi-response-put-401-schema-ref-error)
PUT 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 401 unauthorized HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 401 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.401
then:
  field: $ref
  function: falsy
```
## PUT 401 Responses Uses Schema Reference (openapi-response-put-401-schema-ref-info)
PUT 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 401 unauthorized HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 401 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.401
then:
  field: $ref
  function: truthy
```
## PUT Responses MUST Have 403 Status Codes (openapi-response-put-403-status-code-error)
PUT responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 403 forbidden HTTP status code, communicating that
  consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST Have 403 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '403'
  function: truthy
```
## PUT Responses Has 403 Status Codes (openapi-response-put-403-status-code-info)
PUT responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 403 forbidden HTTP status code, communicating that
  consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 403 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '403'
  function: falsy
```
## PUT 403 Responses MUST Use Schema Reference (openapi-response-put-403-schema-ref-error)
PUT 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 403 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.403
then:
  field: $ref
  function: falsy
```
## PUT 403 Responses Uses Schema Reference (openapi-response-put-403-schema-ref-info)
PUT 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 403 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.403
then:
  field: $ref
  function: truthy
```
## PUT Responses MUST Have 404 Status Codes (openapi-response-put-404-status-code-error)
PUT responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 404 not found HTTP status code, communicating that
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST Have 404 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '404'
  function: truthy
```
## PUT Responses Has 404 Status Codes (openapi-response-put-404-status-code-info)
PUT responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 404 not found HTTP status code, communicating that
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 404 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '404'
  function: falsy
```
## PUT 404 Responses MUST Use Schema Reference (openapi-response-put-404-schema-ref-error)
PUT 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 404 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.404
then:
  field: $ref
  function: falsy
```
## PUT 404 Responses Uses Schema Reference (openapi-response-put-404-schema-ref-info)
PUT 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 404 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.404
then:
  field: $ref
  function: truthy
```
## PUT Responses MUST Have 429 Status Codes (openapi-response-put-429-status-code-error)
PUT responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST Have 429 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '429'
  function: truthy
```
## PUT Responses Has 429 Status Codes (openapi-response-put-429-status-code-info)
PUT responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 429 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '429'
  function: falsy
```
## PUT 429 Responses MUST Use Schema Reference (openapi-response-put-429-schema-ref-error)
PUT 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 429 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.429
then:
  field: $ref
  function: falsy
```
## PUT 429 Responses Uses Schema Reference (openapi-response-put-429-schema-ref-info)
PUT 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: PUT 429 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.429
then:
  field: $ref
  function: truthy
```
## PUT Responses MUST Have 500 Status Codes (openapi-response-put-500-status-code-error)
PUT responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses MUST Have 500 Status Codes
severity: error
given: $.paths.*.put.responses
then:
  field: '500'
  function: truthy
```
## PUT Responses Has 500 Status Codes (openapi-response-put-500-status-code-info)
PUT responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  PUT responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: PUT Responses Has 500 Status Codes
severity: info
given: $.paths.*.put.responses
then:
  field: '500'
  function: falsy
```
## PUT 500 Responses MUST Use Schema Reference (openapi-response-put-500-schema-ref-error)
PUT 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: PUT 500 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.put.responses.500
then:
  field: $ref
  function: falsy
```
## PUT 500 Responses Uses Schema Reference (openapi-response-put-500-schema-ref-info)
PUT 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  PUT 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: PUT 500 Responses Uses Schema Reference
severity: info
given: $.paths.*.put.responses.500
then:
  field: $ref
  function: truthy
```
## DELETE 204 Status Code (openapi-response-delete-204-status-code-error)
DELETE responses should have a 204 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 204 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: DELETE 204 Status Code
severity: info
given: $.paths.*.delete.responses
then:
  field: '204'
  function: truthy
```
## DELETE 204 Status Code (openapi-response-delete-204-status-code-info)
DELETE responses should have a 204 success HTTP status codes, communicating a success created response to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html" target="_blank">operation 2xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 204 success HTTP status codes, communicating a
  success created response to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-2xx.html"
  target="_blank">operation 2xx responses</a> via API Evangelist guidance.
message: DELETE 204 Status Code
severity: info
given: $.paths.*.delete.responses
then:
  field: '204'
  function: falsy
```
## DELETE Responses MUST Have 400 Status Codes (openapi-response-delete-400-status-code-error)
DELETE responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 400 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '400'
  function: truthy
```
## DELETE Responses Has 400 Status Codes (openapi-response-delete-400-status-code-info)
DELETE responses should have a 400 not found HTTP status code, communicating nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 400 not found HTTP status code, communicating
  nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses Has 400 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '400'
  function: falsy
```
## DELETE 400 Responses MUST Use Schema Reference (openapi-response-delete-400-schema-ref-error)
DELETE 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 400 bad request HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 400 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.400
then:
  field: $ref
  function: falsy
```
## DELETE 400 Responses Use Schema Reference (openapi-response-delete-400-schema-ref-info)
DELETE 400 bad request HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 400 bad request HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 400 Responses Use Schema Reference
severity: info
given: $.paths.*.delete.responses.400
then:
  field: $ref
  function: truthy
```
## DELETE Responses MUST Have 401 Status Codes (openapi-response-delete-401-status-code-error)
DELETE responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 401 unauthorized HTTP status code,
  communicating that consumers do not have access. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 401 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '401'
  function: truthy
```
## DELETE Responses Has 401 Status Codes (openapi-response-delete-401-status-code-info)
DELETE responses should have a 401 unauthorized HTTP status code, communicating that consumers do not have access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 401 unauthorized HTTP status code,
  communicating that consumers do not have access. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses Has 401 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '401'
  function: falsy
```
## DELETE 401 Responses MUST Use Schema Reference (openapi-response-delete-401-schema-ref-error)
DELETE 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 401 unauthorized HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 401 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.401
then:
  field: $ref
  function: falsy
```
## DELETE 401 Responses Uses Schema Reference (openapi-response-delete-401-schema-ref-info)
DELETE 401 unauthorized HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 401 unauthorized HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 401 Responses Uses Schema Reference
severity: info
given: $.paths.*.delete.responses.401
then:
  field: $ref
  function: truthy
```
## DELETE Responses MUST Have 403 Status Codes (openapi-response-delete-403-status-code-error)
DELETE responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 403 forbidden HTTP status code, communicating
  that consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 403 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '403'
  function: truthy
```
## DELETE Responses Has 403 Status Codes (openapi-response-delete-403-status-code-info)
DELETE responses should have a 403 forbidden HTTP status code, communicating that consumers are not allowed to access. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 403 forbidden HTTP status code, communicating
  that consumers are not allowed to access. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses Has 403 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '403'
  function: falsy
```
## DELETE 403 Responses MUST Use Schema Reference (openapi-response-delete-403-schema-ref-error)
DELETE 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 403 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.403
then:
  field: $ref
  function: falsy
```
## DELETE 403 Responses Uses Schema Reference (openapi-response-delete-403-schema-ref-info)
DELETE 403 forbidden HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 403 forbidden HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 403 Responses Uses Schema Reference
severity: info
given: $.paths.*.delete.responses.403
then:
  field: $ref
  function: truthy
```
## DELETE Responses MUST Have 404 Status Codes (openapi-response-delete-404-status-code-error)
DELETE responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 404 not found HTTP status code, communicating
  that nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 404 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '404'
  function: truthy
```
## DELETE Responses Has 404 Status Codes (openapi-response-delete-404-status-code-info)
DELETE responses should have a 404 not found HTTP status code, communicating that nothing was found to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 404 not found HTTP status code, communicating
  that nothing was found to consumers. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses Has 404 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '404'
  function: falsy
```
## DELETE 404 Responses MUST Use Schema Reference (openapi-response-delete-404-schema-ref-error)
DELETE 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 404 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.404
then:
  field: $ref
  function: falsy
```
## DELETE 404 Responses Uses Schema Reference (openapi-response-delete-404-schema-ref-info)
DELETE 404 not found HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 404 not found HTTP status codes have a schema references to standardize
  the response payload returned for the error response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 404 Responses Uses Schema Reference
severity: info
given: $.paths.*.delete.responses.404
then:
  field: $ref
  function: truthy
```
## DELETE Responses MUST Have 429 Status Codes (openapi-response-delete-429-status-code-error)
DELETE responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 429 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '429'
  function: truthy
```
## DELETE Responses Has 429 Status Codes (openapi-response-delete-429-status-code-info)
DELETE responses should have a 429 too many requests HTTP status code, communicating a consumer has made too may requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 429 too many requests HTTP status code,
  communicating a consumer has made too may requests. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses Has 429 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '429'
  function: falsy
```
## DELETE 429 Responses MUST Use Schema Reference (openapi-response-delete-429-schema-ref-error)
DELETE 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 429 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.429
then:
  field: $ref
  function: falsy
```
## DELETE 429 Responses Uses Schema Reference (openapi-response-delete-429-schema-ref-info)
DELETE 429 too many requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html" target="_blank">operation 4xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 429 too many requests HTTP status codes have a schema references to
  standardize the response payload returned for the error response. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx-schema.html"
  target="_blank">operation 4xx schema</a> via API Evangelist guidance.
message: DELETE 429 Responses Uses Schema Reference
severity: info
given: $.paths.*.delete.responses.429
then:
  field: $ref
  function: truthy
```
## DELETE Responses MUST Have 500 Status Codes (openapi-response-delete-500-status-code-error)
DELETE responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 500 Status Codes
severity: error
given: $.paths.*.delete.responses
then:
  field: '500'
  function: truthy
```
## DELETE Responses MUST Have 500 Status Codes (openapi-response-delete-500-status-code-info)
DELETE responses should have a 500 internal server erorr HTTP status code, communicating the API had a problem to consumers. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#responses-object">responses object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html" target="_blank">operation 4xx responses</a> via API Evangelist guidance.

```
description: >-
  DELETE responses should have a 500 internal server erorr HTTP status code,
  communicating the API had a problem to consumers. You can find details about
  the <a
  href="https://spec.openapis.org/oas/latest.html#responses-object">responses
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-4xx.html"
  target="_blank">operation 4xx responses</a> via API Evangelist guidance.
message: DELETE Responses MUST Have 500 Status Codes
severity: info
given: $.paths.*.delete.responses
then:
  field: '500'
  function: falsy
```
## DELETE 500 Responses MUST Use Schema Reference (openapi-response-delete-500-schema-ref-error)
DELETE 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: DELETE 500 Responses MUST Use Schema Reference
severity: error
given: $.paths.*.delete.responses.500
then:
  field: $ref
  function: falsy
```
## DELETE 500 Responses Uses Schema Reference (openapi-response-delete-500-schema-ref-info)
DELETE 500 internal server error requests HTTP status codes have a schema references to standardize the response payload returned for the error response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html" target="_blank">operation 5xx schema</a> via API Evangelist guidance.

```
description: >-
  DELETE 500 internal server error requests HTTP status codes have a schema
  references to standardize the response payload returned for the error
  response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/operation-response-5xx-schema.html"
  target="_blank">operation 5xx schema</a> via API Evangelist guidance.
message: DELETE 500 Responses Uses Schema Reference
severity: info
given: $.paths.*.delete.responses.500
then:
  field: $ref
  function: truthy
```
## Schema MUST Have a Description. (openapi-schema-description-error)
Schema should have descriptions that provide a narrative of what a schema object is for, and how it can be used, leaving examples to demonstrate what can actually be expected.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html" target="_blank">schema descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema should have descriptions that provide a narrative of what a schema
  object is for, and how it can be used, leaving examples to demonstrate what
  can actually be expected.  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html"
  target="_blank">schema descriptions</a> via API Evangelist guidance.
message: Schema MUST Have a Description.
severity: error
given: $.components.schemas.*
then:
  field: description
  function: truthy
```
## Schemas Has a Description. (openapi-schema-description-info)
Schema should have descriptions that provide a narrative of what a schema object is for, and how it can be used, leaving examples to demonstrate what can actually be expected.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html" target="_blank">schema descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema should have descriptions that provide a narrative of what a schema
  object is for, and how it can be used, leaving examples to demonstrate what
  can actually be expected.  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html"
  target="_blank">schema descriptions</a> via API Evangelist guidance.
message: Schemas Has a Description.
severity: info
given: $.components.schemas.*
then:
  field: description
  function: falsy
```
## Schema Description MUST be Less Than 250 Characters (openapi-schema-description-length-error)
Schema should have a length limit applied, restricting how long schema descriptions can be, helping keep them concise and consistent. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html" target="_blank">schema descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema should have a length limit applied, restricting how long schema
  descriptions can be, helping keep them concise and consistent. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-descriptions.html"
  target="_blank">schema descriptions</a> via API Evangelist guidance.
message: Schema Description MUST be Less Than 250 Characters
severity: error
given: $.components.schemas.*
then:
  field: description
  function: length
  functionOptions:
    max: 250
```
## Schema Names MUST Be PascalCase. (openapi-schema-names-pascal-case-error)
Schema names are pascal case, keeping the naming of them consistent across APIs, standardizing how consumers can use in their applications. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html" target="_blank">schema names</a> via API Evangelist guidance.

```
description: >-
  Schema names are pascal case, keeping the naming of them consistent across
  APIs, standardizing how consumers can use in their applications. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html"
  target="_blank">schema names</a> via API Evangelist guidance.
message: Schema Names MUST Be PascalCase.
severity: error
given: $.components.schemas
then:
  - field: '@key'
    function: pattern
    functionOptions:
      match: ^[A-Z](([a-z]+[A-Z]?)*)$
  - field: '@key'
    function: pattern
    functionOptions:
      match: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Schema Names Are PascalCase. (openapi-schema-names-pascal-case-info)
Schema names are pascal case, keeping the naming of them consistent across APIs, standardizing how consumers can use in their applications. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html" target="_blank">schema names</a> via API Evangelist guidance.

```
description: >-
  Schema names are pascal case, keeping the naming of them consistent across
  APIs, standardizing how consumers can use in their applications. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html"
  target="_blank">schema names</a> via API Evangelist guidance.
message: Schema Names Are PascalCase.
severity: info
given: $.components.schemas
then:
  - field: '@key'
    function: pattern
    functionOptions:
      notMatch: ^[A-Z](([a-z]+[A-Z]?)*)$
  - field: '@key'
    function: pattern
    functionOptions:
      notMatch: ^[A-Z](([a-z0-9]+[A-Z]?)*)$
```
## Schema Names MUST Be Less Than 25 Characters (openapi-schema-names-length-error)
Schema should have a length limit applied keeping the names of schema consistent across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html" target="_blank">schema names</a> via API Evangelist guidance.

```
description: >-
  Schema should have a length limit applied keeping the names of schema
  consistent across APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-names.html"
  target="_blank">schema names</a> via API Evangelist guidance.
message: Schema Names MUST Be Less Than 25 Characters
severity: error
given: $.components.schemas
then:
  field: '@key'
  function: length
  functionOptions:
    max: 25
```
## Type Format MUST Be int32 or int64. (openapi-schema-properties-allowed-integer-format-error)
Schema integer properties should have a format property with int32 or int64 applied. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema integer properties should have a format property with int32 or int64
  applied. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Type Format MUST Be int32 or int64.
severity: hint
given: $.components.schemas.*.properties[?(@.type=="integer")]
then:
  field: format
  function: enumeration
  functionOptions:
    values:
      - int32
      - int64
```
## Schema Properties MUST Have Format (openapi-schema-properties-allowed-number-format-error)
Schema integer properties should have a format property with int32 or int64 applied. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema integer properties should have a format property with int32 or int64
  applied. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Properties MUST Have Format
severity: hint
given: $.components.schemas.*.properties[?(@.type=="number")]
then:
  field: format
  function: enumeration
  functionOptions:
    values:
      - decimal32
      - decimal64
      - float
      - double
      - decimal128
```
## Schema Array Properties MUST Have Items (openapi-schema-properties-array-items-error)
Schema properties that are of the type array must have an items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array must have an items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties MUST Have Items
severity: error
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  field: items
  function: truthy
```
## Schema Array Properties Has Items (openapi-schema-properties-array-items-info)
Schema properties that are of the type array must have an items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array must have an items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties Has Items
severity: info
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  field: items
  function: falsy
```
## Schema Array Properties MUST Have Max Items (openapi-schema-properties-array-maxitems-error)
Schema properties that are of the type array should have a max items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array should have a max items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties MUST Have Max Items
severity: error
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  - field: maxItems
    function: truthy
```
## Schema Array Properties Have Max Items (openapi-schema-properties-array-maxitems-info)
Schema properties that are of the type array should have a max items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array should have a max items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties Have Max Items
severity: info
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  - field: maxItems
    function: truthy
```
## Schema Array Properties MUST Have Min Items (openapi-schema-properties-array-minitems-error)
Schema properties that are of the type array should have a min items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array should have a min items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties MUST Have Min Items
severity: error
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  - field: minItems
    function: truthy
```
## Schema Array Properties Have Min Items (openapi-schema-properties-array-minitems-info)
Schema properties that are of the type array should have a min items property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type array should have a min items property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Array Properties Have Min Items
severity: info
given: $.components.schemas.*.properties[?(@.type=="array")]
then:
  - field: minItems
    function: falsy
```
## Schema Number Properties MUST Have Maximum (openapi-schema-properties-define-number-maximum-error)
Schema properties that are of the type number should have a maximum property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type number should have a maximum property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Number Properties MUST Have Maximum
severity: error
given: $.components.schemas.*.properties[?(@.type=="number")]
then:
  - field: maximum
    function: defined
```
## Schema Number Properties MUST Have Minimum (openapi-schema-properties-define-number-minimum-error)
Schema properties that are of the type number should have a minimum property defined. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the type number should have a minimum property
  defined. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema Number Properties MUST Have Minimum
severity: error
given: $.components.schemas.*.properties[?(@.type=="number")]
then:
  - field: minimum
    function: defined
```
## Schema Properties MUST Have Description (openapi-schema-properties-descriptions-error)
Schema properties should have descriptions that provide a narrative of the property contains, and how it can be used. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html" target="_blank">schema property descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema properties should have descriptions that provide a narrative of the
  property contains, and how it can be used. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html"
  target="_blank">schema property descriptions</a> via API Evangelist guidance.
message: Schema Properties MUST Have Description
severity: error
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: description
  function: truthy
```
## Schema Properties Have Description (openapi-schema-properties-descriptions-info)
Schema properties should have descriptions that provide a narrative of the property contains, and how it can be used. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html" target="_blank">schema property descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema properties should have descriptions that provide a narrative of the
  property contains, and how it can be used. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html"
  target="_blank">schema property descriptions</a> via API Evangelist guidance.
message: Schema Properties Have Description
severity: info
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: description
  function: falsy
```
## Schema Properties Description MUST Have 250 Characters (openapi-schema-properties-descriptions-length-error)
Schema property descriptions should have a length limit applied, applying constraints to writing descriptions, and keeping consistent across APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html" target="_blank">schema property descriptions</a> via API Evangelist guidance.

```
description: >-
  Schema property descriptions should have a length limit applied, applying
  constraints to writing descriptions, and keeping consistent across APIs. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-descriptions.html"
  target="_blank">schema property descriptions</a> via API Evangelist guidance.
message: Schema Properties Description MUST Have 250 Characters
severity: error
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: description
  function: length
  functionOptions:
    max: 250
```
## Schema Property Enum MUST Be Upper Snake Case (openapi-schema-properties-enum-casing-error)
Schema property enumerators are consistent casing, keeping all entries upper snake case, and consistent across all APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html" target="_blank">schema property enum</a> via API Evangelist guidance.

```
description: >-
  Schema property enumerators are consistent casing, keeping all entries upper
  snake case, and consistent across all APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html"
  target="_blank">schema property enum</a> via API Evangelist guidance.
message: Schema Property Enum MUST Be Upper Snake Case
severity: error
given: $.components.schemas.*.properties.*.enum.*
then:
  function: pattern
  functionOptions:
    match: ^[A-Z]+(?:_[A-Z]+)*$
```
## Schema Property Enum Are Upper Snake Case (openapi-schema-properties-enum-casing-info)
Schema property enumerators are consistent casing, keeping all entries upper snake case, and consistent across all APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html" target="_blank">schema property enum</a> via API Evangelist guidance.

```
description: >-
  Schema property enumerators are consistent casing, keeping all entries upper
  snake case, and consistent across all APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html"
  target="_blank">schema property enum</a> via API Evangelist guidance.
message: Schema Property Enum Are Upper Snake Case
severity: error
given: $.components.schemas.*.properties.*.enum.*
then:
  function: pattern
  functionOptions:
    notMatch: ^[A-Z]+(?:_[A-Z]+)*$
```
## Schema Property Have Enum (openapi-schema-properties-enum-info)
Schema property has enumerators, providing consistent values chosen by consumers when making requests. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html" target="_blank">schema property enum</a> via API Evangelist guidance.

```
description: >-
  Schema property has enumerators, providing consistent values chosen by
  consumers when making requests. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-enums.html"
  target="_blank">schema property enum</a> via API Evangelist guidance.
message: Schema Property Have Enum
severity: info
given: $.components.schemas.*.properties.*
then:
  - field: enum
    function: falsy
```
## Schema MUST Have Properties (openapi-schema-properties-error)
Schema has properties, providing more detail regarding the structure of each schema being applied as part of a request or a response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-properties.html" target="_blank">schema properties</a> via API Evangelist guidance.

```
description: >-
  Schema has properties, providing more detail regarding the structure of each
  schema being applied as part of a request or a response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-properties.html"
  target="_blank">schema properties</a> via API Evangelist guidance.
message: Schema MUST Have Properties
severity: error
given: $.components.schemas[?(@.type=="object")]
then:
  field: properties
  function: truthy
```
## Schema Have Properties (openapi-schema-properties-info)
Schema has properties, providing more detail regarding the structure of each schema being applied as part of a request or a response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-properties.html" target="_blank">schema properties</a> via API Evangelist guidance.

```
description: >-
  Schema has properties, providing more detail regarding the structure of each
  schema being applied as part of a request or a response. You can find details
  about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-properties.html"
  target="_blank">schema properties</a> via API Evangelist guidance.
message: Schema Have Properties
severity: info
given: $.components.schemas[?(@.type=="object")]
then:
  field: properties
  function: falsy
```
## Schema Property Names MUST Be camelCase. (openapi-schema-properties-names-camel-case-error)
Schema property names are camel case, providing consistent casing across all the schema properties used by APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html" target="_blank">schema property names</a> via API Evangelist guidance.

```
description: >-
  Schema property names are camel case, providing consistent casing across all
  the schema properties used by APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html"
  target="_blank">schema property names</a> via API Evangelist guidance.
message: Schema Property Names MUST Be camelCase.
severity: error
given: $.components.schemas.*.properties
then:
  - field: '@key'
    function: pattern
    functionOptions:
      notMatch: ^[A-Z][a-z0-9]*[A-Z0-9][a-z0-9]+[A-Za-z0-9]*$
```
## Schema Property Names Are camelCase. (openapi-schema-properties-names-camel-case-info)
Schema property names are camel case, providing consistent casing across all the schema properties used by APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html" target="_blank">schema property names</a> via API Evangelist guidance.

```
description: >-
  Schema property names are camel case, providing consistent casing across all
  the schema properties used by APIs. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html"
  target="_blank">schema property names</a> via API Evangelist guidance.
message: Schema Property Names Are camelCase.
severity: info
given: $.components.schemas.*.properties
then:
  - field: '@key'
    function: pattern
    functionOptions:
      match: ^[A-Z][a-z0-9]*[A-Z0-9][a-z0-9]+[A-Za-z0-9]*$
```
## Schema Properties Name Length (openapi-schema-properties-names-length-error)
Schema property names have a length restriction applied, keeping names consistent, and avoiding being too long.  You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html" target="_blank">schema property names</a> via API Evangelist guidance.

```
description: >-
  Schema property names have a length restriction applied, keeping names
  consistent, and avoiding being too long.  You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-names.html"
  target="_blank">schema property names</a> via API Evangelist guidance.
message: Schema Properties Name Length
severity: error
given: $.components.schemas.*.properties
then:
  field: '@key'
  function: length
  functionOptions:
    max: 25
```
## Schema String Properties MUST Have Maximum Length (openapi-schema-properties-string-maxlength-error)
Schema properties that are of the string type have the max length applied defining the shape of the property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the string type have the max length applied
  defining the shape of the property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema String Properties MUST Have Maximum Length
severity: error
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: maxLength
  function: truthy
```
## Schema String Properties Has Maximum Length (openapi-schema-properties-string-maxlength-info)
Schema properties that are of the string type have the max length applied defining the shape of the property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the string type have the max length applied
  defining the shape of the property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema String Properties Has Maximum Length
severity: info
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: maxLength
  function: falsy
```
## Schema String Properties MUST Have Minimum Length (openapi-schema-properties-string-minlength-error)
Schema properties that are of the string type have the min length applied defining the shape of the property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the string type have the min length applied
  defining the shape of the property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema String Properties MUST Have Minimum Length
severity: error
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: minLength
  function: truthy
```
## Schema String Properties Has Minimum Length (openapi-schema-properties-string-minlength-info)
Schema properties that are of the string type have the min length applied defining the shape of the property. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html" target="_blank">schema property shapes</a> via API Evangelist guidance.

```
description: >-
  Schema properties that are of the string type have the min length applied
  defining the shape of the property. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-property-shapes.html"
  target="_blank">schema property shapes</a> via API Evangelist guidance.
message: Schema String Properties Has Minimum Length
severity: info
given: $.components.schemas.*.properties[?(@.type == 'string')]
then:
  field: minLength
  function: falsy
```
## Schema MUST Have Required Property (openapi-schema-required-error)
Schema should have a required property defined, being explicit about which properties have to be included with the schema when it is used as part of a request or response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-required.html" target="_blank">schema required</a> via API Evangelist guidance.

```
description: >-
  Schema should have a required property defined, being explicit about which
  properties have to be included with the schema when it is used as part of a
  request or response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-required.html"
  target="_blank">schema required</a> via API Evangelist guidance.
message: Schema MUST Have Required Property
severity: error
given: $.components.schemas[?(@.type=="object")]
then:
  field: required
  function: truthy
```
## Schema Has Required Property (openapi-schema-required-info)
Schema should have a required property defined, being explicit about which properties have to be included with the schema when it is used as part of a request or response. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-required.html" target="_blank">schema required</a> via API Evangelist guidance.

```
description: >-
  Schema should have a required property defined, being explicit about which
  properties have to be included with the schema when it is used as part of a
  request or response. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-required.html"
  target="_blank">schema required</a> via API Evangelist guidance.
message: Schema Has Required Property
severity: info
given: $.components.schemas[?(@.type=="object")]
then:
  field: required
  function: falsy
```
## Schema MUST Have Type Property (openapi-schema-type-error)
Schema should have a type defined, being explicit about type of data a schema describes and can be used to validate, helping standardize the type of data being made available. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-types.html" target="_blank">schema types</a> via API Evangelist guidance.

```
description: >-
  Schema should have a type defined, being explicit about type of data a schema
  describes and can be used to validate, helping standardize the type of data
  being made available. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-types.html"
  target="_blank">schema types</a> via API Evangelist guidance.
message: Schema MUST Have Type Property
severity: error
given: $.components.schemas.*
then:
  field: type
  function: truthy
```
## Schema Has Type Property (openapi-schema-type-info)
Schema should have a type defined, being explicit about type of data a schema describes and can be used to validate, helping standardize the type of data being made available. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#schema-object">schema object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/schema-types.html" target="_blank">schema types</a> via API Evangelist guidance.

```
description: >-
  Schema should have a type defined, being explicit about type of data a schema
  describes and can be used to validate, helping standardize the type of data
  being made available. You can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#schema-object">schema object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/schema-types.html"
  target="_blank">schema types</a> via API Evangelist guidance.
message: Schema Has Type Property
severity: info
given: $.components.schemas.*
then:
  field: type
  function: falsy
```
## Tags MUST Have a Description (openapi-tags-description-error)
Tags used as part of an OpenAPI should have descriptions, providing more of a narrative behind what a tag means when it is applied to an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  Tags used as part of an OpenAPI should have descriptions, providing more of a
  narrative behind what a tag means when it is applied to an API. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: Tags MUST Have a Description
given: $.tags[*]
severity: error
then:
  field: description
  function: truthy
```
## Tags Have a Description (openapi-tags-description-info)
Tags used as part of an OpenAPI should have descriptions, providing more of a narrative behind what a tag means when it is applied to an API. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  Tags used as part of an OpenAPI should have descriptions, providing more of a
  narrative behind what a tag means when it is applied to an API. You can find
  details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: Tags Have a Description
given: $.tags[*]
severity: info
then:
  field: description
  function: falsy
```
## Tags MUST Have a Name (openapi-tags-name-error)
Tags used as part of an OpenAPI should have names, providing a simple key word or phrase that represents the tag being applied to APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  Tags used as part of an OpenAPI should have names, providing a simple key word
  or phrase that represents the tag being applied to APIs. You can find details
  about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: Tags MUST Have a Name
given: $.tags[*]
severity: error
then:
  field: name
  function: truthy
```
## Tags Have a Name (openapi-tags-name-info)
Tags used as part of an OpenAPI should have names, providing a simple key word or phrase that represents the tag being applied to APIs. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  Tags used as part of an OpenAPI should have names, providing a simple key word
  or phrase that represents the tag being applied to APIs. You can find details
  about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag
  object for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: Tags Have a Name
given: $.tags[*]
severity: info
then:
  field: name
  function: falsy
```
## OpenAPIs MUST Have a Tag Object (openapi-tags-object-error)
There needs to be a central tags object applied to the OpenAPI, providing central tags that can be applied across all operations within an OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  There needs to be a central tags object applied to the OpenAPI, providing
  central tags that can be applied across all operations within an OpenAPI. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: OpenAPIs MUST Have a Tag Object
given: $
severity: error
then:
  field: tags
  function: truthy
```
## OpenAPIs Have a Tag Object (openapi-tags-object-info)
There needs to be a central tags object applied to the OpenAPI, providing central tags that can be applied across all operations within an OpenAPI. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  There needs to be a central tags object applied to the OpenAPI, providing
  central tags that can be applied across all operations within an OpenAPI. You
  can find details about the <a
  href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: OpenAPIs Have a Tag Object
given: $
severity: info
then:
  field: tags
  function: falsy
```
## MUST Be At Least One Tag (openapi-tags-one-error)
There needs to be at least one tag applied to an OpenAPI, providing a key word or phrase that can be applied to API operations. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  There needs to be at least one tag applied to an OpenAPI, providing a key word
  or phrase that can be applied to API operations. You can find details about
  the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object
  for OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: MUST Be At Least One Tag
given: $
severity: error
then:
  field: tags
  function: length
  functionOptions:
    min: 1
```
## Tag Names MUST Have First Letter in Each Word Capitalized (openapi-tags-upper-case-error)
The first letter of each word in a tag being applied to APIs needs to be capitalized, keeping the tags being applied across APIs the same look and feel for organizing and publishing to documentation. You can find details about the <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for OpenAPI</a>, and explore <a href="https://guidance.apievangelist.com/guidance/openapi/tags.html" target="_blank">tags</a> via API Evangelist guidance.

```
description: >-
  The first letter of each word in a tag being applied to APIs needs to be
  capitalized, keeping the tags being applied across APIs the same look and feel
  for organizing and publishing to documentation. You can find details about the
  <a href="https://spec.openapis.org/oas/latest.html#tag-object">tag object for
  OpenAPI</a>, and explore <a
  href="https://guidance.apievangelist.com/guidance/openapi/tags.html"
  target="_blank">tags</a> via API Evangelist guidance.
message: Tag Names MUST Have First Letter in Each Word Capitalized
severity: error
given: $.tags.*.name
then:
  function: pattern
  functionOptions:
    match: '[A-Z]\w*'
```
