---
layout: layouts/page.njk
title: Frontend workflow
pageTitle: Frontend workflow
pageDescription: Describing an approach & workflow for the design and development of the HEE National Website Frontend. 
path: /blueprint
permalink: /blueprint/poc-spikes/frontend-workflow.html
eleventyNavigation:
  subgroup: Platform Spikes
  parent: Proof of concept spikes
  key: Frontend workflow
  order: 2
---
## Questions to answer / Assumptions to validate

- What tools will be required to support a component based front end workflow?
- Where will our component library be published?


## Constraints

- Source code is managed in GitHub
- Source code is made available under an open source license
- Options that support a component first workflow are preferred
- Options that are compatible with the NHSUK Frontend Framework are preferred
- Options that provide a clear integration with the Content Management Platform are preferred


## Outcomes

**q.** What tools will be required to support a component based front end workflow?
**a.** Storybook.js provides the best choice currently to support an open source component based, front end framework and workflow

**q.** Where will our component library be published?
**a.** We will use NPM to publish out component library

## Narrative

With an understanding and recognition that the front end of our application should be built and managed to facilitate re-use across multiple platforms, not just BloomReach, we looked to identify tools that would help us to create a frontend framework that enabled a component based workflow.

There are a range of these sorts of tools available and to a certain extent the choice is determined somewhat by the choice of javascript/component framework, however given that we hadn't at this point chosen a templating/rendering framework - we favoured tools that could be used across a range of template langugages/javascript frameworks.  

### Component development tools

Of the three tools described below we think StoryBook.js provides the best choice. It provides excellent support for React, Vue and Angular javascript frameworks and can also be used with vanilla HTML and Web Components.

#### Styleguidist - https://github.com/styleguidist/react-styleguidist

**Pros:**
- Provides great styleguide documentation
**Cons:** 
- Is restricted to React or Vue (for which there is an alternative project)

#### StoryBook.js - https://storybook.js.org/

**Pros:**
- Has support for a wide range of templating languages including HTML and Web Components as well as React and Vue
**Cons:** 
- Isn't really setup for serving associated documentation (ie less of a Design System tool)


#### PatternLab - https://patternlab.io/

**Pros:**
- Provides out of the box support for PHP templating such as Twig and Javascript templates such as Handlebars
**Cons:**
- Has taken a very long time to move from version 2 to version 3 and still doesn't appear to be stable

### Front end component publishing

In order to make the components available both to our applications, we believe our packages should be published to NPM


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
