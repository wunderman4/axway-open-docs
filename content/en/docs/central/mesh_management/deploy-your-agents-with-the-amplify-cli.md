---
title: Deploy your agents with AMPLIFY CLI
linkTitle: Deploy your agents
weight: 160
date: 2020-12-0
description: Use the AMPLIFY CLI to deploy Axway mesh agents 
---
{{< alert title="Public beta" color="warning" >}}This is a preview of the new mesh discovery agents that run separately from the current mesh governance agents, which provide full governance of your hybrid environment. The new agents are deployed and configured from the Axway CLI, and they allow for updated visibility to the mesh discovery process.{{< /alert >}}

## Before you begin

Ensure you have the following tools installed:

* AMPLIFY Central CLI 0.1.17 or later
* Helm 3.2.4 or later
* Istioctl 1.6.8
* Kubectl 1.16 or later
* Node.js 10.13.0 or later
* OpenSSL 2.8.3 or later

For more information about installing the CLI, see [Install AMPLIFY Central CLI](/docs/central/cli_central/cli_install/).

## Log in to the AMPLIFY Central CLI

Run the following command to log into the Central CLI with your AMPLIFY Platform credentials:

```shell
amplify auth login --client-id apicentral
```

A dialog box is shown. Enter your valid credentials (email address and password), and after the authorization successful message is displayed, go back to the AMPLIFY CLI.

If you are a member of multiple AMPLIFY organizations, select an organization and continue.

## Install Axway mesh agents

1. Run the `install` command to begin the installation of the Axway mesh agents. The first section of the installation collects information about the Istio deployment, such as the domain name to use for the gateway, the protocol, and the TLS certificate details.

    ```bash
    amplify central install agents
    ```

    The installation displays the following prompts.

    ```bash
    Select the type of gateway you want to connect:
    API Gateway v7
    Amazon API Gateway
    Kubernetes
    ```

2. Select `Kubernetes` as your gateway. The next prompts are related to the deployment of Istio in your cluster.

3. Enter the domain name of the cluster:

    ```bash
    Enter the fully qualified domain name (URL) of your Kubernetes cluster:
    ```

4. Enter the protocol to use for the Istio gateway:

    ```bash
    Enter the protocol to use for the ingress gateway:
    HTTP
    HTTPS
    ```

5. Enter the port on which you want to expose the gateway. If you choose `HTTPS`, the default port will be `443`. If you choose `HTTP`, the default port will be `8080`.

    ```bash
    Enter the Kubernetes cluster port: (443)
    ```

6. Enter the name of the Kubernetes secret to store the certificate. By default, Istio gets deployed in the `istio-system` namespace, and the secret for the gateway certificate is saved to this namespace. The creation of this namespace is handled by the deployment of Istio, if it does not exists yet.

   ```bash
   Enter the name of the secret to store the Istio gateway certificate: (gateway-cert)
   ```

7. Choose if you would like to generate a self-signed certificate or provide your own certificate.

    If you choose to generate a certificate, the AMPLIFY CLI will use OpenSSL to create the private key and the certificate, which will be placed in the current directory where you are running the AMPLIFY CLI. If you choose to provide an existing certificate, you will be prompted with the file path to the private key and the certificate.

### Generate a self-signed certificate

To generate a self-signed certificate, select `Generate self signed certificate` and press `enter`.

```bash
Would you like to generate a self signed certificate, or provide your own?: (Use arrow keys)
Generate self signed certificate
Provide certificate
```

The console displays two lines of text indicating that the certificate and key were created and that a Kubernetes secret was created in the `istio-system` namespace.

```bash
Would you like to generate a self signed certificate, or provide your own?: Generate self signed certificate
Created gateway-cert.crt and gateway-cert.key in /Users/axway
Created secret/gateway-cert in the istio-system namespace.
```

### Provide certificate

To provide your own certificate, select `Provide certificate` and press `enter`.

The next prompt asks for the file path to the private key. The path is relative to the directory where you invoked the AMPLIFY CLI command from. If your certificate and key are stored in another directory from where you are running the CLI, then you must provide the full path to the files.

After you provide the path for both the private key and the certificate, the CLI creates the secret in the `istio-system` namespace.

```bash
Enter the name of the secret to store the Istio gateway certificate: gateway-cert
Would you like to generate a self signed certificate, or provide your own?: Provide certificate
Enter the file path to the private key: /Users/axway/private_key.key
Enter the file path to the certificate: /Users/axway/certificate.crt
Created secret/gateway-cert in the istio-system namespace.
```

## Select the agents to install

The following prompts are related to the details about the mesh agents.

1. Select what you would like to install. You can install only one of the agents, or both. The discovery agent option deploys the API Discovery Agent and the Resource Discovery Agent.

    ```bash
    Select which agents to install: (Use arrow keys)
    All agents
    Discovery agent
    Traceability agent
    ```

2. Enter the namespace where you would like to deploy the agents or accept the default option by pressing `enter`. The CLI collects a list of all your existing namespaces and provides an option to deploy to one of those. You can also choose to create a new Kubernetes namespace and deploy there instead.

    ```bash
    Create a new namespace
    ──────────────
    default
    istio-system
    kube-node-lease
    ```

    In this example we will create a new namespace.

    ```bash
    Enter a new namespace name: (apic-control)
    ```

After the namespace is created, you are asked for the DevOps Service Account (DOSA) to use, so the agents can authenticate with AMPLIFY Central. You can create a new DOSA account or select an existing one.

{{< alert title="Note">}} If you choose to use an existing DOSA account, you must provide the same public and private keys that were used to create the DOSA account you have selected. Failure to do so will cause the agents to fail to authenticate with AMPLIFY Central.{{< /alert >}}

### Create a new DOSA account

To create a new DOSA account, follow these steps:

1. Select `Create a new account` and press `enter`.

    ```bash
    Select a service account (DOSA): (Use arrow keys)
    Create a new account
    ──────────────
    mesh
    ──────────────
    ```

2. Enter a name for the new DOSA account name. Creating a new DOSA account will override any file named `public_key.pem` or `private_key.pem` in the directory where you invoked the AMPLIFY CLI from.

    ```bash
    Select a service account (DOSA):  Create a new account
    WARNING: Creating a new DOSA account will overwrite any existing "private_key.pem" and "public_key.pem" files in this directory
    Enter a new service account name:  mesh-dosa
    ```

    After you enter the name of the account and press `enter`, an output is shown with the client ID of the account and the directory where the keys were placed.

    ```bash
    Enter a new service account name: mesh-dosa
    Creating a new service account.
    New service account "mesh-dosa" with clientId "DOSA_cb46caebd35f4e8689b56ee5f813b576" has been successfully created.
    The private key has been placed at /Users/axway/private_key.pem
    The public key has been placed at /Users/axway/public_key.pem
    ```

3. Enter a name for the Kubernetes secret to store the keys. The CLI will create the secret automatically in the namespace that you selected for the mesh agent installation.

    ```bash
    The secret will be created with the same `private_key.pem` and `public_key.pem` that was auto generated to create the DOSA Account.
    Enter the name of the secret to store your public and private keys: (agent-secrets)
    Created agent-secrets in the apic-control namespace.
    ```

### Use an existing DOSA account

To use an existing DOSA account for the mesh agents, follow these steps:

1. Select the DOSA account from the list and press `enter`.

    ```bash
    Select a service account (DOSA):  (Use arrow keys)
    Create a new account
    ──────────────
    mesh
    ──────────────
    ```

2. Enter the keys that were used to create the account. They must be the **same** keys that were used to create this DOSA account. It is recommended to provide the full file path to the location of the keys.

    ```bash
    Select a service account (DOSA):  mesh
    Please provide the the same "private_key.pem" and "public_key.pem" that was used to create the selected DOSA Account.
    Enter the file path to the public key:  /Users/axway/public_key.pem
    Enter the file path to the private key:  /Users/axway/private_key.pem
    ```

3. Enter the name of the Kubernetes secret that will store the keys. The AMPLIFY CLI will create the Kubernetes secret for you in the namespace you selected for the mesh agent installation.

    ```bash
    Enter the name of the secret to store your public and private keys:  (agent-secrets)
    Created agent-secrets in the apic-control namespace.
    ```

## Provide a K8S cluster resource

After the details of the DOSA account have been provided you will be asked to either create a new K8S Cluster resource or provide the name of an existing K8S Cluster resource.

```bash
Create a new K8S Cluster
──────────────
mesh-env
──────────────
```

If you chose to create a new K8S Cluster, type the name and press `enter`.

```bash
Enter a new K8S Cluster name:  mesh-demo
Creating a new K8SCluster
New k8scluster "mesh-demo" has been successfully created.
```

A message indicating that the new cluster has been created is shown.

At this point, the CLI will create two files (`istio-override.yaml` and `hybrid-override.yaml`) and place them in your current directory. The CLI will also create three resources (one `SpecDiscovery` and two `ResourceDiscoveries`) to discover the demo service that is packaged along with the `apicentral-hybrid` helm chart.

## Install Istio

Run the following command to install Istio:

```bash
istioctl install --set profile=demo -f istio-override.yaml
```

## Finish the installation of the agents

After the Istio installation is complete, run the following command to finish the installation of the agents:

```bash
helm repo update
helm upgrade --install --namespace apic-control apic-hybrid axway/apicentral-hybrid -f hybrid-override.yaml
```

Note that the discovery agents polls every 10 seconds for the discovery resources by default. To change this, you must pass a helm override in the form of `--set ada.poll.interval` or `--set rda.poll.interval` accordingly with the desired agents.

For example, if you want the API Discovery agent to poll every 2 seconds for the discovery resources, you must run the following command to install the agents:

```bash
helm upgrade --install --namespace apic-control apic-hybrid axway/apicentral-hybrid -f hybrid-override.yaml --set ada.poll.interval=2s
```

## Verify that the pods are running

1. After the installation is complete, run the command below with the namespace you selected for the mesh agent location and confirm that the pods are all in a running status.

    ```bash
    kgp -n apic-control
    NAME                               READY   STATUS    RESTARTS   AGE
    apic-hybrid-ada-bc5fcd58-6ghvb     1/1     Running   0          18s
    apic-hybrid-als-76b499bc7c-d4566   1/1     Running   0          17s
    apic-hybrid-als-76b499bc7c-rgtqb   1/1     Running   0          17s
    apic-hybrid-rda-64cfdb558b-7kz2s   1/1     Running   0          17s
    ```

2. The `apicentral-hybrid` helm installation creates a namespace named `apic-demo` and deploys a service called `apic-hybrid-list`. Run the following command to verify this demo service is running.

    ```bash
    kgp -n apic-demo
    NAME                                READY   STATUS    RESTARTS   AGE
    apic-hybrid-list-598f8f9b4b-9wsc6   2/2     Running   0          90s
    ```

3. The installation creates resources, which provide configuration to the API Discovery Agent and the Resource Discovery Agent. You can use the AMPLIFY CLI to verify the agents are configured and running, and to list the resources that are expect to exist as a result of the agents discovering the `apic-hybrid-list` service.

    ```bash
    amplify central get apispecs -s mesh-demo
    ✔ Resource(s) has successfully been retrieved

    NAME              AGE            TITLE   SCOPE KIND  SCOPE NAME
    mylist100swagger  5 minutes ago  mylist  K8SCluster  mesh-demo
    ```

    If you see one resource after running this command, that confirms that the API Discovery Agent is working.

    ```bash
    amplify central get k8sresources -s mesh-demo
    ✔ Resource(s) has successfully been retrieved

    NAME                                             AGE            TITLE                      SCOPE KIND  SCOPE NAME
    service.apic-demo.apic-hybrid-list               6 minutes ago  service-cli-1605812140608  K8SCluster  mesh-demo
    pod.apic-demo.apic-hybrid-list-598f8f9b4b-9wsc6  6 minutes ago  pod-cli-1605812140608      K8SCluster  mesh-demo
    ```

    If you see two resources after running this command, that confirms that the Resource Discovery Agent is working.

## Where to go next

For more information on the details of the resources and how the discovery process works, see [Discover APIs and Services](/docs/central/mesh_management/discover-apis-and-services).