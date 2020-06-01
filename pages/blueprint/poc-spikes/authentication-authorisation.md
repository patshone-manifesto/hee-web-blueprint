---
layout: layouts/page.njk
title: Authentication and authorisation
pageTitle: Authentication and authorisation
pageDescription: Describing an approach to authentication and authorisation for the National Website Platform
path: /blueprint
permalink: /blueprint/poc-spikes/authentication-authorisation.html
eleventyNavigation:
  subgroup: LKS Spikes
  parent: Proof of concept spikes
  key: Authentication and authorisation
  order: 4
---
## Questions to answer / Assumptions to validate

- What platform and/or subsystems should be used to provide end user authentication capabilities?


## Constraints

- Options that are used by Health Education England currently are preferred.
- Pre-existing NHS platforms are preferred.
- In the first instance we will look at meeting the needs of the Library and Knowledge services teams.

## Outcomes

**q.** What platform and/or subsystems should be used to provide end user authentication capabilities?
**a.** In the first instance Microsoft Azure AD should be used to provide end user authentication for the HEE National Website Platform. However it is worth noting that for the majority of Library and Knowledge Services staff, the abilty to use OpenAthens credentials to authenticate with the platform needs to be available 


## Narrative

For the proof of concept we described an integration between BloomReach (configured to use Spring Security 

- https://bloomreach-forge.github.io/hst-spring-security/) 

and Azure AD (https://azure.microsoft.com/en-gb/blog/spring-security-azure-ad/)

Of the other options we reviewed, the most interesting was NHS Identity Service and particularly its Identity Management Service. 

- https://digital.nhs.uk/services/nhs-identity/guidance-for-developers/services-offered-by-nhs-identity/identity-management-service

This NHS provided service appears to offer an existing NHS platform that would meet our current requirements. However at the time of writing, we have been unable to get access to the platform to validate these assumptions. This option should be explored again at a later date.

Development of the integration of Azure AD with BloomReach and Spring Security and then subsequently with the sample BloomReach hosted React application can be found on this branch in source control - 

- https://github.com/Manifesto-Digital/hee-content-management-system/tree/feature/azure-ad-auth-impl-and-bloomreach-react-integration-works




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
