---
title: Environment and Gateway Management
linkTitle: Environment and Gateway Management
weight: 15
date: 2020-11-18
description: Overview of Environments, what are they, what are they for, what can I do with them, a glossary of basic terms, a few pictures.
---

{{< alert title="Public beta" color="warning" >}}This feature is currently in **public beta** and not yet available for production use.{{< /alert >}}

## Environments

![AMPLIFY Central Environment Details](/Images/central/env_and_gateway_mgmt/EnvironmentDetailsPage.png)

Within Topology, Environments play a key role in maintaining the integrity of the catalog by grouping a set of assets that are discovered from or belong to a similar source. Environments can represent assets discovered from a runtime environment, a repository, or things manually added to the catalog. Environments are at the highest hierarchical level. All assets are linked to an environment and have a hard dependency to their environment. This gives you the ability to control assets as a group. For example, if you delete the environment all assets scoped within will also be deleted. Another example is configuring a customized subscription flow for all assets in this group published in the catalog using the same webhook and secret. Continue reading below for more information around environment use cases.

### Connected vs Manual Sync

Getting assets into your environment is a process that you will have to do at least once and depending on how quickly those assets evolve over their lifecycle, may need to be updated quite frequently. To automate the discovery of assets and keep discovered assets up to date, Agents were created which handle this process and other advanced functionality.

-   Connected
    -   Agents are installed in your environment to handle the discovery of assets or to send log information about APIs to AMPLIFY Central.
    -   [Agent docs for API Manager V7](/docs/central/connect-api-manager/)
    -   [Agent docs for AWS Gateway](/docs/central/connect-aws-gateway/)
-   Manual Sync
    -   Environment assets can be updated manually through the [AMPLIFY Central CLI](/docs/central/cli_getstarted/) or the AMPLIFY Central APIs, changes in your deployment will not be automatically synced with Central.

---

## Asset Definitions

### Services

Service assets are the primary asset within an environment. These services can take many shapes (API, MFT, Protobuff, docs, etc) and can be added manually or discovered and auto-added by Axway agents. However the service is added, the intent of a service is the same in how it represents a physical deployment of a resource. Later, these services can be combined and packaged together to create catalog items (products) for your consumers to access.

#### Versions

Services have a specification based on the type (OAS3, WSDL, protobuf, etc). Whenever this specification changes a new version should be created. This helps account for different stages in the lifecycle of the service. Each version has a direct dependency on the services they are associated with and are able to be individually configured for differing consumer access needs.

#### Endpoints

Since services represent a physical deployment, you need a way to associate the spec found in the version to the actual endpoint. Endpoints contain the host and port information used to access the service. Endpoints have a hard dependency on the version they are associated with.

#### Catalog Items

Contains all the discoverable and consumable APIs available in Unified Catalog, to which consumers can subscribe. For more information about the catalog please see [AMPLIFY Unified Catalog](/docs/catalog/).

---

### Webhooks

Webhook assets are used for enabling subscription flows when a catalog user wants to subscribe to your service. Because these are scoped to the environment level they are reusable with other assets within the environment.

### Secrets

Secrets are a special kind of asset used with webhooks for securing subscription flows, the use cases for secrets is expected to grow.
