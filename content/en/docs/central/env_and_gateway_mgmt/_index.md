---
title: Environment & Gateway Management
linkTitle: Environment & Gateway Management
weight: 120
date: 2020-11-18
description: Overview of Topology, what is it, what is it for, what can I do with it, glossary of basic terms, a few pictures. The model behind Env and APIService / etc.
---

{{< alert title="Public beta" color="warning" >}}This feature is currently in **public beta** and not yet available for production use.{{< /alert >}}

## Environments

![AMPLIFY Central Environment Details](/Images/central/env_and_gateway_mgmt/EnvironmentDetailsPage.png)

Within Topology, Environments are at the highest scope level. All assets within an environment are scoped to it and share a "hard" dependency with the environment. This means if you delete the environment all assets scoped within will also be deleted. This dependency also allows the reuse of assets throughout the environment, for example you can use the same webhook and secret when creating a catalog item from any service within the same environment. Continue reading below for more information around environment use cases.

### Connected vs Manual Sync

Getting assets into your environment is a process that you will have to do at least once and depending on how quickly those assets evolve over their life you may need to update these assets quite frequently. In order to automate the discovery of assets and keep those assets up to date Agents were created to handle this process.

-   Connected
    -   Agents are installed in your environment which handle discovery of assets.
    -   Agent support for Discovery, Telemetry and Policies. (coming soon)
-   Manual Sync
    -   Environment assets need to be updated manually though the [AMPLIFY Central cli](/docs/central/cli_getstarted/), changes in your deployment will not be automatically synced with Central.

---

## Asset Types and Definitions

### Services

Service assets are the primary asset within an environment. These services can take many shapes (API, MTF, Protobuff, docs, etc) and can be added manually or managed by axway agents. Either way, the intent of a service is to represent a physical deployment of a resource. Later, these services can be combined and packaged together to create catalog items (products) for your consumers to access.

<!-- TODO: Fill in these as subs levels to a service. Mention the hard dependency.
#### Revisions

#### Instances

#### Catalog Items (Consumer Instances) -->

---

### Webhooks

Webhook assets are used for enabling subscription flows when a catalog user wants to subscribe to your service. Because these are scoped to the environment level they are reusable with other assets within the environment.

### Secrets

Secrets are a special kind of asset used with webhooks for securing subscription flows, the use cases for secrets is expected to grow.

<!-- TODO: Expand this when support for webhooks, secrets, gateways, etc is added -->
