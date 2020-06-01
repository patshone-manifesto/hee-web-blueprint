---
layout: layouts/page.njk
title: Document management
pageTitle: Document management
pageDescription: Providing a document management capability for the National Website Platform
path: /blueprint
permalink: /blueprint/poc-spikes/document-management.html
eleventyNavigation:
  subgroup: LKS Spikes
  parent: Proof of concept spikes
  key: Document management
  order: 4
---
## Questions to answer / Assumptions to validate

- Should the platform provide native document management capabilities or should we integration with an external service?
- What platform should be used to provide document management capabilities?
- How should security for the managed documents be managed?

## Constraints

- Options that are used by the team currently are preferred.
- Pre-existing NHS platforms are preferred.
- In the first instance we will look at meeting the needs of the Library and Knowledge services teams.

## Outcomes

**q.** Should the platform provide native document management capabilities or should we integrate with an external service?
**a.** The platform should utilise a thirdparty document management system to provide this set of capabilities. Although NHS Digital utilise BloomReach to publish digital documents, the needs of the Knowledge and Library Services teams are more sophisticated and require provision for a range of document types

**q.** What platform should be used to provide document management capabilities?
**a.** In the first instance Microsoft Office 365 should be used to provide document management capabilities for the platform. FutureNHS could be the platform that is utilised subsequently, however at this moment in time, given that the FutureNHS platform is just about to be rebuilt, we believe that MS Office 365 provides the best choice for the platform. It is noted here though, that particular focus should be given to the ability for users without current Office 365 credentials to successfully use the platform

**q.** How should security for the managed documents be managed?
**a.** For the most part documents available on the site should be publically available, however for documents that require working groups to collaborate on where the content needs to be restricted, permissions for those documents should be managed in the document management system.



## Narrative

For the proof of concept work delivered here we looked to try and balance the validation of principles with the delivery of something practically useful. The principles to be proved here are the integration of a third-party resource provider (in this case documents) and the implementation of authorisation within both the delivered website and the third-party resource provider.

Microsoft Office 365 provides (through the MS Graph APIs) access to a broad range of document management functionality and BloomReach provides through it's CRISP API subsystem a good way of providing a resource-centric API proxy of resources stored and managed in external systems. So for the PoC we described a CRISP based API proxy that mediated access to documents stored in Microsoft Sharepoint Online

The following branch provides source code for the implementation of the PoC 

- https://github.com/Manifesto-Digital/hee-content-management-system/tree/feature/HEE-5-sharepoint-bloomreach-integration/



<div class="nhsuk-table__panel-with-heading-tab">
  <h3 class="nhsuk-table__heading-tab">Related architecture decision records</h3>
  <div class="nhsuk-table-responsive">
    <table class="nhsuk-table">
      <caption class="nhsuk-table__caption">Related architecture decision records</caption>
      <thead class="nhsuk-table__head">
        <tr class="nhsuk-table__row">
          <th class="nhsuk-table__header" scope="col">ID</th>
          <th class="nhsuk-table__header" scope="col">Name</th>
        </tr>
      </thead>
      <tbody class="nhsuk-table__body">
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell" style="white-space:nowrap;">ADR-0010</td>
          <td class="nhsuk-table__cell "><a href="/blueprint/adrs/ADR-0010-use-external-document-management-system.html">Use external document management system</a></td>
        </tr>
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0011</td>
          <td class="nhsuk-table__cell "><a href="/blueprint/adrs/ADR-0011-use-federated-authentication-provider.html">Use federated authentication provider</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
