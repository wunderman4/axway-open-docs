---
title: Manage your environments
linkTitle: Manage your environments
weight: 15
date: 2020-11-18
description: Understand environments in a topology, what are they, what are they for, what can you do with them.
---

{{< alert title="Public beta" color="warning" >}}This feature is currently in **public beta** and not yet available for production use.{{< /alert >}}

Within topology, environments help to maintain the integrity of the catalog by grouping a set of assets that are discovered from or belong to a similar source.

Environments are at the highest hierarchical level in the topology, and they can represent assets discovered from a runtime environment, a repository, or things manually added to the catalog. Assets are linked to an environment, which allows you to control them as a group. For example, if you delete an environment, all assets scoped within will also be deleted. Another example, you can configure a customized subscription flow for all assets in a group published in the catalog using the same webhook and secret.

The following image shows the details of an environment in AMPLIFY Central.

![AMPLIFY Central Environment Details](/Images/central/env_and_gateway_mgmt/EnvironmentDetailsPage.png)

## Synchronize your environment

After you add assets to your environment, you can use agents to automate the discovery of assets and keep discovered assets up-to-date, or you can do it manually.

To sync your environment automatically, you must install the agents in your environment and they will handle the discovery of assets and send log information about APIs to AMPLIFY Central. For more information, see:

* [Discovery and Traceability Agents for API Manager](/docs/central/connect-api-manager/).
* [Discovery and Traceability Agents for AWS Gateway](/docs/central/connect-aws-gateway/).

To manually sync your environment, you can use the [AMPLIFY Central CLI](/docs/central/cli_getstarted/) or the AMPLIFY Central APIs. Note that changes in your deployment will not be automatically synced with AMPLIFY Central.

## Asset definitions

This section provides a description of the assets that you can use on your environment.

### Services

A service represents a physical deployment of a resource in an environment. Examples of services are: API, MFT, Protobuf, documentation, and so on. You can manually add services to your environment or they can be discovered and auto-added by Axway agents. Later, these services can be combined and packaged together to create catalog items (products) for your consumers to access.

#### Versions

Services have a specification based on type (OAS3, WSDL, Protobuf, and so on). Whenever this specification changes a new version must be created. This helps account for different stages in the lifecycle of the service. Each version has a direct dependency on their associated services and are able to be individually configured for differing consumer access needs.

#### Endpoints

Since services represent a physical deployment, you need a way to associate the specification found in the version to the actual endpoint. Endpoints contain the host and port information used to access the service. Endpoints have a hard dependency on their associated versions.

#### Catalog items

Contains all the discoverable and consumable APIs available in the [AMPLIFY Unified Catalog](/docs/catalog/), to which consumers can subscribe.

### Webhooks

Webhook assets are used for enabling subscription flows when a catalog user wants to subscribe to your service. Webhooks are scoped to the environment level, which makes them reusable with other assets within the environment.

### Secrets

Secrets are a special kind of asset used with webhooks for securing subscription flows.
