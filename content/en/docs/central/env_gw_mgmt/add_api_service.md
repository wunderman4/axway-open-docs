---
title: Add an API Service
linkTitle: Add an API Service
weight: 20
date: 2021-02-09
description: How to create an api service.
---

{{< alert title="Public beta" color="warning" >}}This feature is currently in **public beta** and not yet available for production use.{{< /alert >}}

To get started creating an api service in the UI, first navigate to the details page of an environment. From the details page there is a plus ( + ) button located at the top right of the `Activity Dashboard`

> If you want to add an api service using the amplify Central CLI refer to the docs [here](/docs/central/cli_central/cli_apiservices) instead.

![EnvDetailsPage](/Images/central/add_api_service/envDetailsPage.png)

### Step 1: Import your service

Define the api specification by uploading a file, or by fetching the spec from a URL. If you chose to upload a file the accepted file extensions are listed below by file type vs service specification type. Any uploaded file may also be uploaded as an unstructured type, this is useful if your spec type is not officially supported.

|           |   OAS2   |           |   OAS3   |           | Protobuf |           |   WSDL   |           |
| --------- | :------: | :-------: | :------: | :-------: | :------: | :-------: | :------: | :-------: |
| File Type | Expected | Supported | Expected | Supported | Expected | Supported | Expected | Supported |
| .json     |   YES    |    YES    |   YES    |    YES    |    NO    |    NO     |    NO    |    NO     |
| .yml/yaml |   YES    |    NO     |   YES    |    NO     |    NO    |    NO     |    NO    |    NO     |
| .wsdl     |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |
| .proto    |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |    NO    |    NO     |
| .xml      |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |    NO    |    YES    |

![fileUploadTruthTable](/Images/central/add_api_service/fileUploadTruthTable.png)

**REVIEWERS: DO WE WANT THE IMAGE OR THE MARKDOWN TABLE?**

We will automatically parse the file and set the `Specification Type' on upload. You can choose to overwrite this choice by simply selecting a different type. If your combination is not supported or you have an example of a combination that is incorrectly detected please let us know.

![importApiSpec](/Images/central/add_api_service/importApiSpec.png)

### Step 2: Confirm Information

* Title is a friendly name for the service, it will be displayed first and is searchable.
* Logical Name must be unique and is used as the unique id for the service. The logical name will be referenced in dependencies of this service.
* Description is limited to 1000 characters.
* Tags are used to group assets, making it easier to find assets faster.
* Attributes are key and value pairs used for extending functionality and integrations with third party systems.
* Service Image now has an improved crop that will resize the selection and maintain the correct aspect ratio.

![confirmInformation](/Images/central/add_api_service/confirmInformation.png)

### Step 3: Submit

Once the required fields have been met the save button will be enabled and you can submit the form.

### Errors and debugging

In the event there is an error while submitting the form the page will have a large error box above the fields explaining what has happened. The error may contain references to objects only found when using the CLI or API directly, in this case refer to the [amplify CLI](/docs/central/cli_central/cli_apiservices) documentation for further guidance.
