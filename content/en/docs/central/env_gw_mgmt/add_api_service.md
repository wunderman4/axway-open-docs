---
title: Add an API Service
linkTitle: Add an API Service
weight: 20
date: 2021-02-09
description: How to create an api service.
---

## Add an API Service

Follow these steps to create an API Service.

1. From the details page of your environment, select the plus ( + ) button located at the top right of the **Activity Dashboard**
2. To define the API specification, **upload a file**, or **fetch from URL**.
3. Confirm the information about your API service and click **Save**.

> If you want to add an API service using the amplify Central CLI, please refer to these [docs](/docs/central/cli_central/cli_apiservices) instead.

### Import Service Specification

Define the API specification by uploading a file or by fetching the specification from a URL. If you chose to upload a file, the accepted file extensions are listed below by accepted file type versus service specification type. Any uploaded specification file can be assigned as an unstructured specification type; this is useful if your specification type is not officially supported.

|           |   OAS2   |           |   OAS3   |           | Protobuf |           |   WSDL   |           |
| --------- | :------: | :-------: | :------: | :-------: | :------: | :-------: | :------: | :-------: |
| File Type | Expected | Supported | Expected | Supported | Expected | Supported | Expected | Supported |
| .json     |   YES    |    YES    |   YES    |    YES    |    NO    |    NO     |    NO    |    NO     |
| .yml/yaml |   YES    |    NO     |   YES    |    NO     |    NO    |    NO     |    NO    |    NO     |
| .wsdl     |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |
| .proto    |    NO    |    NO     |    NO    |    NO     |   YES    |    YES    |    NO    |    NO     |
| .xml      |    NO    |    NO     |    NO    |    NO     |    NO    |    NO     |    NO    |    YES    |

On upload, the file is automatically parsed and the recommended `Specification Type' set. Optionally, if the recommended specification type is incorrect, you can override the selection by choosing a different specification type.

### Confirm Information

* **Title** represents a friendly name for the service. The title will be displayed first and is searchable but does not need to be unique.
* **Logical Name** represents the unique id for the service and must be unique within the scope of the environment. The logical name is referenced in any dependencies of the API service.
* **Description** is limited to 1000 characters.
* **Tags** are used to group assets, making it easier to find assets faster.
* **Attributes** are key and value pairs used for extending functionality and integrations with third-party systems.
* **API Service Image** now has an improved crop that will resize the selection and maintain the correct aspect ratio.

### Errors and debugging

In the event, there is an error while saving the API service. The form page will have a large error box explaining what caused the error. The error may contain references to objects only found when using the CLI or API directly. In this case please refer to the [amplify CLI](/docs/central/cli_central/cli_apiservices) documentation for further guidance.
