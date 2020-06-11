---
layout: layouts/page.njk
title: Channel and blueprinting
pageTitle: Channel and blueprinting
pageDescription: Using Bloomreach's Channel and Blueprinting functionality to provide ability to create subsites
path: /blueprint
permalink: /blueprint/poc-spikes/channel-blueprinting.html
eleventyNavigation:
  subgroup: Platform Spikes
  parent: Proof of concept spikes
  key: Channel and blueprinting
  order: 5
---
## Questions to answer / Assumptions to validate

- Are Bloomreach's channels suitable for providing and managing required subsites (i.e. Deenary sites)?
- Can Bloomreach's 'blueprinting' functionality be utilised to provide the ability to spin up channels easily and consistently?
- Can a roles and permission model be created to enable segmented channel specific content as well as enable sharing of relevant content between channels? 

## Constraints

- 

## Outcomes

**q.** Are Bloomreach's channels suitable for providing and managing required subsites (i.e. Deenary sites)?
**a.** Yes, Bloomreach's channel functionality is a good logical abstraction of the site model required by HEE. Components and functionality can be made available to channels, and abstract elements can be included that are inherited from channel information (i.e. the region name in the header). For further exploration during implementation would be if there is a way to extend the channel manager UI to include a heirarchical view of content and sites.

**q.** Can Bloomreach's 'blueprinting' functionality be utilised to provide the ability to spin up channels easily and consistently?
**a.** Yes, Bloomreach's blueprinting functionality allows for new channels to be created easily and consistently. Rules can be defined that govern what is created as part of a channel creation. We are also able to set parameters as part of the blueprint operation that allows for us to require certain information to be provided during creation. As part of further investigation or implementation, we would want to look into how far we could extend this parameterisation. 

**q.** Can a roles and permission model be created to enable segmented channel specific content as well as enable sharing of relevant content between channels? 
**a.** We are able to build a permissions model where content can be created and used only on a given channel or group of channels (i.e. content created just for the South West channel, or created for all speciality recruitement channels). We are also able to extend the permissions model to allow for content that is referencable between channels, for example national content that can be brought onto a regional site page in a read only fashion. 


## Narrative

For the proof of concept work delivered here, we were able to explore a few out of the box features offered bythe experience manager - channels and blueprinting. Channels are BR's concept of different destinations for groupings of content - these could be different websites, mobile applications or other consumers of content, whilst blueprinting is a way to create new channels using a consistent set of rules. 

As part of this work, we also explored how permissions tie into the wider requirements in this area, including how we can segregate content to ensure it is only visable and usable in the correct channels, as well as allowing content to be shared between 'levels', for example, how we could create a piece of national content and have it be available to regional sites (channels) in a read-only context. 

Overall, this out of the box functionality worked well, and we feel it will be able to meet the project needs and goals. Some extensability will likely be required, particularly around the blueprinting parameterisation, but these implementation details can be resolved once the full set of requirements is available. 

The following branch provides source code for the implementation of the PoC 

- https://github.com/Manifesto-Digital/hee-content-management-system/tree/feature/HEE-62-separate-global-and-local-channel-setup-approach



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
          <td class="nhsuk-table__cell" style="white-space:nowrap;">ADR-0013</td>
          <td class="nhsuk-table__cell "><a href="/blueprint/adrs/ADR-0013-use-bloomreach-channel-manager.html">Use Bloomreach channel manager</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
