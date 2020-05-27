---
layout: layouts/page.njk
title: Deployment
pageTitle: Deployment
pageDescription: How and where is the platform installed and configured?
path: /blueprint
permalink: /blueprint/deployment.html
eleventyNavigation:
  subgroup: Operations
  parent: Blueprint
  key: Deployment
  order: 9
---

- How and where is the software installed and configured?
- Is it clear how the software will be deployed across the infrastructure elements described in the infrastructure architecture section? (e.g. one-to-one mapping, multiple containers per server, etc)
- If this is still to be decided, what are the options and have they been documented?
- Is it understood how memory and CPU will be partitioned between the processes running on a single piece of infrastructure?
- Are any containers and/or components running in an active-active, active-passive, hot-standby, cold-standby, etc formation?
- Has the deployment and rollback strategy been defined?
- What happens in the event of a software or infrastructure failure?
- Is it clear how data is replicated across sites?
