---

copyright:
  years: 2020
lastupdated: "2020-07-21"

keywords: code engine, api reference, api

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# API reference 
{: #api}

You can use the {{site.data.keyword.codeenginefull_notm}} API to create and manage your {{site.data.keyword.codeengineshort}} entities. To use the CLI, see [Setting up the CLI](/docs/codeengine?topic=codeengine-kn-install-cli). 
{: shortdesc}

## Retrieve your Kubernetes configuration with REST API
{: #api-rest}

To retrieve your Kubernetes configuration with REST API, follow these steps:

1. Authenticate with IBM Cloud Identity and Access Management (IAM) to receive an IAM access token.
2. Query the IBM Cloud Catalog and the IBM Cloud Resource Controller to receive a GUID for your project.
3. Use the {{site.data.keyword.codeenginefull_notm}} API to receive a Kubernetes configuration.

### Authenticate with IBM Cloud IAM
{: #api-iam}

[Create your {{site.data.keyword.cloud_notm}} IAM access token](/docs/account?topic=account-manapikey){: external} by making a POST request to `https://iam.cloud.ibm.com/identity/token`.

### Determine the GUID of your project
{: #api-guid}

Determine the GUID of your {{site.data.keyword.codeengineshort}} project by quering the IBM Cloud Catalog and IBM Cloud Resource Controller. As this GUID does not change, you need to do this step only one time. If you already know your {{site.data.keyword.codeengineshort}} project GUID, you can skip this step.

**CLI**

1. Log in into IBM Cloud and target a region, account, and resource group:
   
   ```
   ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
   ```
   {: pre}
 
 2. Run the `ibmcloud resource` command.
    
    ```
    ibmcloud resource service-instances --service-name knative --long
    ```
    {: pre}
    
Identify the service instance that represents your {{site.data.keyword.codeengineshort}} project and determine the GUID from the output.

**REST API**

Before you begin, you must have the `access_token` from the previous step.

1. Use following IBM Cloud Catalog API method: [Returns parent catalog entries](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#returns-parent-catalog-entries){: external}.

   Example:

   ```
   curl -X GET \
     'https://globalcatalog.cloud.ibm.com/api/v1?include=*&q=name:knative+active:true" \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

   Identify the unique resource ID in the resources list. The field name is `ID` and the JSON path is `resources[].id`.
   
2. Query the IBM Cloud Resource Controller with the IBM Cloud Resource Controller API method [Get a list of all resource instances](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#get-a-list-of-all-resource-instances){: external}. You must have the {{site.data.keyword.codeengineshort}} project name, the region that your project resides, and the unique resource ID of {{site.data.keyword.codeengineshort}} in the global catalog. Use the name of your {{site.data.keyword.codeengineshort}} project as query parameter.

   Example:

   ```
   curl -X GET \
     'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

   Identify the {{site.data.keyword.codeengineshort}} project from your region in the result list. Find the `guid` output to use in the following steps.

### Query the IBM {{site.data.keyword.codeengineshort}} API
{: #api-query-api}

Before you begin, you must have the following information.

- The `access_token` and `refresh_token` from previous steps.
- The `guid` of your {{site.data.keyword.codeengineshort}} project.
- The region in which your {{site.data.keyword.codeengineshort}} project is located.

Use the [`get kubeconfig for the specified project`](https://cloud.ibm.com/apidocs/coligo#get-kubeconfig-for-the-specified-project){: external} {{site.data.keyword.codeengineshort}} API method to get the Kubernetes configuration.

   Example:

   ```
   curl -X GET \
     'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
     -H 'Authorization: Bearer ACCESS_TOKEN'
   ```
   {: pre}

## Retrieving your Kubernetes configuration with the CLI
{: #api-cli}

1. Log in into IBM Cloud and target a region, account, and resource group:
   
   ```
   ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
   ```
   {: pre}
   
2. Target your {{site.data.keyword.codeengineshort}} project and export the Kubernetes config: 

   ```
   ibmcloud ce target --name PROJECT --export.
   ```
   {: pre}
   
For more information about using {{site.data.keyword.codeengineshort}} APIs, Kubernetes API, and `kubectl`, see the following topics:

- [{{site.data.keyword.codeengineshort}} API](https://cloud.ibm.com/apidocs/codeengine){: external}
- [Kubernetes REST API](https://kubernetes.io/docs/reference/using-api/api-overview/){: external}
- [Kubernetes API concepts](https://kubernetes.io/docs/reference/using-api/api-concepts/){: external}
- [API client libraries](https://kubernetes.io/docs/reference/#api-client-libraries){: external}
- [`kubectl` command](https://kubernetes.io/docs/reference/#cli-reference){: external}

## Custom resource definition (CRD)
{: #api-crd}

The following sections list the custom resource definition methods to use with {{site.data.keyword.codeengineshort}}.

**Batch CRDs**

| Group | Version | Kind |
| --------- | -------- | -------- |
| codeengine.cloud.ibm.com | v1alpha1 | JobDefinition |
| codeengine.cloud.ibm.com | v1alpha1 | JobRun |
{: caption="Batch CRDs for {{site.data.keyword.codeengineshort}}" caption-side="top"}

After retrieving the Kubernetes configuration, you can view Batch CRD details using the following methods:

1. Use `kubectl explain --api-version='codeengine.cloud.ibm.com/v1alpha1' <Kind>`.
2. [Download Swagger / OpenAPI specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.
  
**Serving CRDs**

| Group | Version | Kind |
| --------- | -------- | -------- |
| serving.knative.dev | v1 | Configuration |
| serving.knative.dev | v1 | Revision |
| serving.knative.dev | v1 | Route |
| serving.knative.dev | v1 | Service |
{: caption="Serving CRDs for {{site.data.keyword.codeengineshort}}" caption-side="top"}

For more information about these CRDS, see [Knative Serving API Specification](https://knative.dev/docs/serving/spec/knative-api-specification-1.0/){: external}.


