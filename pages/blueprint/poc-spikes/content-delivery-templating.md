---
layout: layouts/page.njk
title: Content delivery templating
pageTitle: Content delivery templating
pageDescription: Choosing the templating languages and frameworks to implement the HEE National Website Frontend 
path: /blueprint
permalink: /blueprint/poc-spikes/content-delivery-templating.html
eleventyNavigation:
  subgroup: Platform Spikes
  parent: Proof of concept spikes
  key: Content delivery templating
  order: 3
---

## Questions to answer / Assumptions to validate

- Is it possible to describe a single source of templating truth across the HEE design system and Content Management Platform?


## Constraints

- Source code is managed in GitHub
- Source code is made available under an open source license
- Options that support a component first workflow are preferred
- Options that are compatible with the NHSUK Frontend Framework are preferred
- The platform frontend code should be able to support users on modern browsers, including IE 11 and above

## Outcomes

**q.** Is it possible to describe a single source of templating truth across the HEE design system and Content Management Platform?
**a.** We believe the it is possible to provide a single source of template truth by choosing React as the templating language. React can be used successfully with BloomReach and supports inpage content editing in React component-based pages through the use of an enterprise license.


## Narrative

This question proved particularly tricky to answer adequately and the decision we made does have some trade offs. 

For this PoC we built a simple React based application that provided content management functionality and reused pre-built components provided by the NHSUK Frontend framework.

In order to determine the choice of language/framework we first looked to the major components of our application and assessed their preferences in terms of templating / rendering frameworks.

- **BloomReach**: uses a templating language called Freemarker out of the box
- **NHSUK Frontend**: uses a javascript based templating language called nunjucks out of the box, although it also provides vanilla HTML versions of its components
- **StoryBook.js**: provides native support for a range of templating languages that unfortunately doesn't include Freemarker or nunjucks


Initally we looked to undertake some investigative development work to determine what would be required to support:

#### Freemarker as the core templating language: 

There is an opensource project that makes it possible to compile and utilise Freemarker templates using javascript therefore opening up the possibility of rendering those templates in StoryBook.js. We were able to build a small PoC that showed this working, however we identified some key problems, particularly with attempts to render BloomReach Freemarker templates that contained BloomReach specific tags. 

We were also aware that to reuse the work of the NHSUK Frontend project we would need to create a custom implementation of the provided components as Freemarker templates. This would be a significant piece of work.

We spent a very small amount of time looking at utilising an open source project that provided a way of parsing nunjucks templates into an AST with the view to generating Freemarker templates directly from the NHSUK nunjucks source. And again this would be a significant piece of work.


#### Nunjucks as the core templating language:

We looked at a small PoC that demonstrated nunjucks templates rendering in StoryBook.js, however there is no Java based interpreter for nunjucks so using them with BloomReach would require utilising BloomReach's headless capability and building a custom renderer for it.


#### React as the core templating language:

As part of investigating the use of nunjucks we spent some time looking at BloomReach's headless (SPA) support. The part of the product is quite new although is fully supported and provides out of the box support for React and Angular components.

Following this, we identified some work undertaken by NHS Digital that provides a React based implementation of the NHSUK Frontend project 

- https://github.com/NHSDigital/nhsuk-react-components

Interestingly this set of components provides documentation through the use of StoryBook.js as well 

- https://nhsdigital.github.io/nhsuk-react-components/?path=/story/actionlink--actionlink




<div class="nhsuk-table__panel-with-heading-tab">
  <h3 class="nhsuk-table__heading-tab">Architecture decision records</h3>
  <div class="nhsuk-table-responsive">
    <table class="nhsuk-table">
      <caption class="nhsuk-table__caption">Architecture decision records</caption>
      <thead class="nhsuk-table__head">
        <tr class="nhsuk-table__row">
          <th class="nhsuk-table__header" scope="col">ID</th>
          <th class="nhsuk-table__header" scope="col">Name</th>
        </tr>
      </thead>
      <tbody class="nhsuk-table__body">
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0007</td>
          <td class="nhsuk-table__cell "><a href="ADR-0007-use-storybook-js-to-develop-and-document-screens-and-components.html">Use StoryBook.js to develop and document screens and components</a></td>
        </tr>
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0008</td>
          <td class="nhsuk-table__cell "><a href="ADR-0008-use-npm-to-host-hee-frontend-framework.html">Use NPM to host HEE front end framework</a></td>
        </tr>
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0009</td>
          <td class="nhsuk-table__cell "><a href="ADR-0009-use-react-to-manage-and-develop-the-components-for-the-hee-frontend-framework.html">Use React to manage and develop HEE frontend</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>