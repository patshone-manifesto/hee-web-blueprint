---
layout: layouts/page.njk
title: ADR-0009 Use react to manage and develop the components for the HEE frontend framework
pageTitle: ADR-0009 Use react to manage and develop the components for the HEE frontend framework
pageDescription: 
path: /blueprint
permalink: /blueprint/adrs/ADR-0009-use-react-to-manage-and-develop-the-components-for-the-hee-frontend-framework.html
eleventyNavigation:
  parent: Architecture decisions
  key: ADR-0009 Use react to manage and develop the components for the HEE frontend framework
  order: 9
---

# 9. Use react to manage and develop the components for the HEE frontend framework

Date: 2020-04-04

## Status

Pending

## Context

We sought to identify a single templating language that would provide a source of truth across our frontend & content management platforms. This aim seeks to reduce the effort in developing on the content management platform by mitigating the burden of markup integration. We also aimed to find a templating language that allowed us to utilise the components already created as part of the NHSUK frontend framework.

### Options

We identified three main candidates to use as our templating language:

#### Freemarker: 

Freemarker is the native templating language used by BloomReach and although there are projects


#### Nunjucks:

We looked at a small PoC that demonstrated nunjucks templates rendering in StoryBook.js, however there is no Java based interpreter for nunjucks so using them with BloomReach would require utilising BloomReach's headless capability and building a custom renderer for it.


#### React:

As part of investigating the use of nunjucks we spent some time looking at BloomReach's headless (SPA) support. The part of the product is quite new although is fully supported and provides out of the box support for React and Angular components.

Following this, we identified some work undertaken by NHS Digital that provides a React based implementation of the NHSUK Frontend project 

- https://github.com/NHSDigital/nhsuk-react-components

Interestingly this set of components provides documentation through the use of StoryBook.js as well 

- https://nhsdigital.github.io/nhsuk-react-components/?path=/story/actionlink--actionlink

## Decision

The change that we're proposing or have agreed to implement.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
