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

Within Topology, Environments are at the highest scope level. All assets within an environment are scoped to it and have a "hard" dependency on the environment. This means if you delete the environment all assets scoped within will also be deleted. This dependency also allows the reuse of assets throughout the environment, for example, you can use the same webhook and secret when creating a catalog item from any service within the same environment. Continue reading below for more information around environment use cases.

### Connected vs Manual Sync

Getting assets into your environment is a process that you will have to do at least once and depending on how quickly those assets evolve over their lifecycle, may need to be updated quite frequently. To automate the discovery of assets and keep discovered assets up to date, Agents were created which handle this process and other advanced functionality.

* Connected
    * Agents are installed in your environment which handles the discovery of assets.
    * [Agent docs for API Manager V7](/docs/central/connect-api-manager/)
    * [Agent docs for AWS Gateway](/docs/central/connect-aws-gateway/)
* Manual Sync
    * Environment assets need to be updated manually through the [AMPLIFY Central cli](/docs/central/cli_central/), changes in your deployment will not be automatically synced with Central.

---

## Asset Definitions

### Services

![AMPLIFY Central Service Details](/Images/central/env_and_gateway_mgmt/ServiceDetailsPage.png)

Service assets are the primary asset within an environment. These services can take many shapes (API, MTF, Protobuff, docs, etc) and can be added manually or managed by Axway agents. Either way, the intent of a service is to represent a physical deployment of a resource. Later, these services can be combined and packaged together to create catalog items (products) for your consumers to access.

#### Versions

Services have a specification based on the type (OAS3, WSDL, protobuf, etc). Whenever this specification changes a new version should be created. This helps account for different stages in the lifecycle of the service. Different versions can be configured individually for consumer access. Versions have a hard dependency on the service they are associated with.

#### Endpoints

Since services represent a physical deployment, you need a way to associate the spec found in the version to the actual endpoint. Endpoints contain the host and port information used to access the service. Endpoints have a hard dependency on the version they are associated with.

#### Catalog Items

Contains all the discoverable and consumable APIs available in Unified Catalog, to which consumers can subscribe. For more information about the catalog please see [AMPLIFY Unified Catalog(/docs/catalog/).

---

### Webhooks

Webhook assets are used for enabling subscription flows when a catalog user wants to subscribe to your service. Because these are scoped to the environment level they are reusable with other assets within the environment.

### Secrets

Secrets are a special kind of asset used with webhooks for securing subscription flows, the use cases for secrets is expected to grow.
