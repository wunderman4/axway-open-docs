---
title: Add an API Service
linkTitle: Add an API Service
weight: 20
date: 2021-02-09
description: How to create an api service.
---

{{< alert title="Public beta" color="warning" >}}This feature is currently in **public beta** and not yet available for production use.{{< /alert >}}

To get started creating an api service in the UI, first navigate to the details page of an environment. From the details page there is a plus ( + ) button located at the top right of the `Activity Dashboard`

> If you want to add an api service using the AMPLIFY Central CLI refer to the docs [here](/docs/central/cli_central/cli_apiservices) instead.

![EnvDetailsPage](/Images/central/add_api_service/envDetailsPage.png)

## Step 1: Import your service

![importApiSpec](/Images/central/add_api_service/importApiSpec.png)

The first step in creating your service is to define the api specification, there are a two options available in the UI.

### Upload file

If you chose to upload a file the accepted extensions for spec type are listed below.

|           |   OAS2   |           |   OAS3   |           | Protobuf |           |   WSDL   |           |
| --------- | :------: | :-------: | :------: | :-------: | :------: | :-------: | :------: | :-------: |
| File Type | Expected | Supported | Expected | Supported | Expected | Supported | Expected | Supported |
| .json     |   YES    |    YES    |   YES    |    YES    |    NO    |    NO     |    NO    |    NO     |
| .yml/yaml |   YES    |    NO     |   YES    |    NO     |    NO    |    NO     |    NO    |    NO     |
| .wsdl     |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |
| .proto    |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |    NO    |    NO     |
| .xml      |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |    NO    |    YES    |

We will attempt to parse the file uploaded and will adjust the `Specification Type' to match on upload. You can choose to overwrite this chose by simply selecting a different type.

If your combination is not supported or you have an example of a combination that is incorrectly detected please let us know.

### Fetch from URL

Fetching the api specification from url only supports json at the moment.

## Step 2: Confirm Information

![confirmInformation](/Images/central/add_api_service/confirmInformation.png)

* Title: a friendly name
* Logical Name: must be unique, used as the asset id and will be referenced in dependencies.
* Description: limited to 1000 characters.
* Tags: used to group assets to make easier to find.
* Attributes: are key and value pairs used for extending functionality and integrations with third party systems.
* Image: now with better crop functionality!

## Step 3: Submit

Once the required fields have been met the save button will be enabled and you can submit the form.
