---
layout: layouts/page.njk
title: Infrastructure architecture
pageTitle: Infrastructure architecture
pageDescription: What data does the platform store, how is it modelled and governed?
path: /blueprint
permalink: /blueprint/infrastructure-architecture.html
eleventyNavigation:
  subgroup: Architecture
  parent: Blueprint
  key: Infrastructure architecture
  order: 8
---

- Is there a clear physical architecture?
- What hardware (virtual or physical) does this include across all tiers?
- Does it cater for redundancy, failover and disaster recovery if applicable?
- Is it clear how the chosen hardware components have been sized and selected?
- If multiple servers and sites are used, what are the network links between them?
- Who is responsible for support and maintenance of the infrastructure?
- Are there central teams to look after common infrastructure (e.g. databases, message buses, application servers, networks, routers, switches, load balancers, reverse proxies, internet connections, etc)?
- Who owns the resources?
- Are there sufficient environments for development, testing, acceptance, pre-production, production, etc?