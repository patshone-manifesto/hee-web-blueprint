---
layout: layouts/page.njk
title: Search service
pageTitle: Search service
pageDescription: Choosing a search service to provide capabilities required for the HEE NWP 
path: /blueprint
permalink: /blueprint/poc-spikes/search-service.html
eleventyNavigation:
  subgroup: Platform Spikes
  parent: Proof of concept spikes
  key: Search service
  order: 4
---

## Questions to answer / Assumptions to validate

- Is the Bloomreach native search capability sufficient to provide the required capabilities? 
- If no, what should be used to provide the search? 
- How should the search service fit into the system architecture? 

## Constraints

- 

## Outcomes

**q.** Is the Bloomreach native search capability sufficient to provide the required capabilities? 
**a.** We believe that the native OOTB search provided by Bloomreach Experience Manager is insufficient to provide all of the required functionality required, such as synonym search and the level of customisability required. Bloomreach themselves acknowlegde that the search capabilities provided by the OOTB Lucene search is rather basic, and unsuitable for enterprise level search. 

**q.** If no, what should be used to provide the search? 
**a.** An external search as a service tool would be the recommended solution. Given HEE's organisational direction of travel towards the Microsoft suite of tools, this could be implemented using an Azure offering such as Cognative search. However we would recommend Algolia - a powerful and customisable search tool that offers much if not all of the functionality required, and offers a good balance between implementation complexity and configuratbility

**q.** How should the search service fit into the system architecture? 
**a.** We would recommend a service element is introduced to facilitate indexing from Bloomreach. This extends on the architectural patterns outlined when we explored integration with document and authentication providers. The search service can fit into the wider system architecture by recieving events from other sources, providing a searchable index with mulitple sources, which is a likely pattern that would need to be adopted (recieving events from the document platform and other sytems such as Oriel)

## Narrative

For the search service proof of concept, we looked at some examples from Bloomreach about using Apache Camel to create a service that listens for publish/ depublish events, and processes them using a REST API to send the document onto an external search service for indexing

https://developers.bloomreach.com/blog/2019/zero-code-content-search.html

Using Camel, we are able to subscribe to the HippoServiceBus for events (in our example, pub and depub events), and use Camel to transform the message to the appropriate format, and enqueuing for a REST API, which then sends the updated document request (index or delete) to the search POC - in this case Algolia. 

We were able to utilise Algolia's prebuilt React components (https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/react/) to quickly implement a search function/ results onto the site. These components were easy to style in using the work previously undertaken around templating. For the purposes of the POC, Algolia provides examples of much of the core functionality needed for the search, including synonym search and facets. 

We also set up Hawtio (https://hawt.io/) for the purpose of getting a console for visulaing and managing the Camel routing, which we would recommend as the suggested approach. 

This branch on source control contains the POC work for the backend implementation of Camel and the Alogia integration https://github.com/Manifesto-Digital/hee-content-management-system/tree/feature/camel-search-engine-integration


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
          <td class="nhsuk-table__cell">ADR-0012</td>
          <td class="nhsuk-table__cell "><a href="ADR-0012-use-external-search-service.html">Use external search service</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>