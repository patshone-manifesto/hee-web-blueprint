---
layout: layouts/page.njk
title: Build and deployment automation
pageTitle: Build and deployment automation
pageDescription: Proving the ability to use GitHub actions to successfully build, test and deploy a BloomReach project to brCloud
path: /blueprint
permalink: /blueprint/poc-spikes/build-deployment.html
eleventyNavigation:
  subgroup: Platform Spikes
  parent: Proof of concept spikes
  key: Build and deployment automation
  order: 1
---
## Questions to answer / Assumptions to validate

- Where should our source code be stored?
- What license should our source code be made available under?
- Can GitHub actions be used to automate the full Build -> Test -> Deploy lifecycle of the platform?

## Constraints

- Build is managed with Maven
- Environments are provided by brCloud
- Options with no additional cost are preferred

## Outcomes

**q.** Where should our source code be stored?
**a.** Our source code should be stored in github, given its use across a range of other NHS digital products

**q.** What license should our source code be made available under?
**a.** We should make our code available under a permissive open source license such as MIT

**q.** Can GitHub actions be used to automate the full Build -> Test -> Deploy lifecycle of the platform?
**a.** Yes GitHub actions can be used successfully to automate the build and deployment of BloomReach applications to the BloomReach Cloud


It was straight forward to automate the build and deployment using github actions and given that it reduces the infrastructure that would need to be provisioned to support further automation efforts, we should continue to invest in building on this platform.

As part of the investigative work for this spike we utilised the following project to reduce development time, the project provides a way to execute Github Actions locally on a developers machine.

- https://github.com/nektos/act


## Narrative

We determined to use github to store source code, HEE already have a presence on github which makes this decision a bit easier.

We determined to look at github actions first, given that it's the native offering from github and available without further cost to open source projects.


### Pipeline

The following document describes the pipeline created for deploying to the development environment - https://github.com/Manifesto-Digital/hee-content-management-system/blob/master/.github/workflows/ci-and-cd-dev.yml

#### Items of interest

- The pipeline runs an initial build and test execution in order to catch any compilation or test errors first

- The use of whelk-io/maven-settings-xml-action@v4 action to support the rewriting of the maven settings file so that resources can be requested from the BloomReach enterprise repository 

```
name: CI & CD [DEV]

on:
  push:
    branches: [master]
    # branches: [develop] # can be enabled when ready

jobs:
  buildAndTest:
    name: Build & Test

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8

      - name: Cache maven packages
        uses: actions/cache@v1
        with:
          path: ~/.m2
          key: ${{ runner.os }}-m2-${{ hashFiles('**/pom.xml') }}
          restore-keys: ${{ runner.os }}-m2

      - name: Configure maven settings
        uses: whelk-io/maven-settings-xml-action@v4
        with:
          repositories: '[{ "id": "hippo-maven2-enterprise", "url": "https://maven.onehippo.com/maven2-enterprise/" }]'
          plugin_repositories: '[{ "id": "hippo-maven2-enterprise", "url": "https://maven.onehippo.com/maven2-enterprise/" }]'
          servers: '[{ "id": "hippo-maven2-enterprise", "username": "${{ secrets.BLOOMREACH_MVN_USERNAME }}", "password": "${{ secrets.BLOOMREACH_MVN_PASSWORD }}" }]'

      - name: Compile
        run: mvn -B clean compile -Pdefault --file pom.xml

      - name: Test
        run: mvn -B clean test -Pdefault --file pom.xml

  deploy:
    name: Deploy to Dev. Env. [on brCloud]

    needs: buildAndTest

    env:
      STACK_NAME: hee
      BRC_USERNAME: ${{ secrets.BRC_USERNAME }}
      BRC_PASSWORD: ${{ secrets.BRC_PASSWORD }}

    runs-on: ubuntu-latest

    steps:
      - name: Check out repo.
        uses: actions/checkout@v2

      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8

      - name: Cache maven packages
        uses: actions/cache@v1
        with:
          path: ~/.m2
          key: ${{ runner.os }}-m2-${{ hashFiles('**/pom.xml') }}
          restore-keys: ${{ runner.os }}-m2

      - name: Configure maven settings
        uses: whelk-io/maven-settings-xml-action@v4
        with:
          repositories: '[{ "id": "hippo-maven2-enterprise", "url": "https://maven.onehippo.com/maven2-enterprise/" }]'
          plugin_repositories: '[{ "id": "hippo-maven2-enterprise", "url": "https://maven.onehippo.com/maven2-enterprise/" }]'
          servers: '[{ "id": "hippo-maven2-enterprise", "username": "${{ secrets.BLOOMREACH_MVN_USERNAME }}", "password": "${{ secrets.BLOOMREACH_MVN_PASSWORD }}" }]'

      - name: Package
        # run: mvn -B verify && mvn deploy -Pdist --file pom.xml
        run: mvn -B verify && mvn -Pdist --file pom.xml
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Setting distribution path (distPath) as an output parameter
        id: dist
        run: echo "::set-output name=distPath::$(ls -1 ${{ github.workspace }}/target/$(mvn help:evaluate -Dexpression=project.artifactId -q -DforceStdout)-$(mvn help:evaluate -Dexpression=project.version -q -DforceStdout)-*.tar.gz)"

      - name: Install Deployment Script dependencies
        run: cd $GITHUB_WORKSPACE/.github/workflows/scripts/bloomreach-deployment; npm install

      - name: Login to Bloomreach Cloud
        uses: ./.github/workflows/actions/login/
        id: login

      - name: Upload distribution to Bloomreach Cloud
        uses: ./.github/workflows/actions/upload/
        id: upload
        with:
          accessToken: ${{ steps.login.outputs.accessToken }}
          refreshToken: ${{ steps.login.outputs.refreshToken }}
          distPath: ${{ steps.dist.outputs.distPath }}

      - name: Deploy distribution to 'development' env
        uses: ./.github/workflows/actions/deploy/
        id: deploy
        with:
          accessToken: ${{ steps.upload.outputs.accessToken }}
          refreshToken: ${{ steps.login.outputs.refreshToken }}
          distId: ${{ steps.upload.outputs.distributionId }}
          environmentName: development
```

#### Github actions

The following actions automate the login, upload and package deployment to the BloomReach cloud

- Login - https://github.com/Manifesto-Digital/hee-content-management-system/blob/master/.github/workflows/scripts/bloomreach-deployment/login.js
- Upload - https://github.com/Manifesto-Digital/hee-content-management-system/blob/master/.github/workflows/scripts/bloomreach-deployment/upload.js
- Deploy - https://github.com/Manifesto-Digital/hee-content-management-system/blob/master/.github/workflows/scripts/bloomreach-deployment/deploy.js 

<div class="nhsuk-table__panel-with-heading-tab">
  <h3 class="nhsuk-table__heading-tab">Related Architecture decision records</h3>
  <div class="nhsuk-table-responsive">
    <table class="nhsuk-table">
      <caption class="nhsuk-table__caption">Related Architecture decision records</caption>
      <thead class="nhsuk-table__head">
        <tr class="nhsuk-table__row">
          <th class="nhsuk-table__header" scope="col">ID</th>
          <th class="nhsuk-table__header" scope="col">Name</th>
        </tr>
      </thead>
      <tbody class="nhsuk-table__body">
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0002</td>
          <td class="nhsuk-table__cell "><a href="/blueprint/adrs/ADR-0002-use-github-for-source-control.html">Use Github for Source Control</a></td>
        </tr>
        <tr class="nhsuk-table__row">
          <td class="nhsuk-table__cell">ADR-0003</td>
          <td class="nhsuk-table__cell "><a href="/blueprint/adrs/ADR-0003-use-github-actions-for-automation.html">Use Github Actions for automation</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>