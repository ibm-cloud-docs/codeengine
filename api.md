---

copyright:
  years: 2024
lastupdated: "2024-02-05"

keywords: api reference, api, Kubernetes configuration and code engine, CRD for code engine, CRD, custom resource definition, guid, kubernetes, authenticate, code engine api

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# API reference 
{: #api}

You can use the {{site.data.keyword.codeenginefull}} API to create and manage your {{site.data.keyword.codeengineshort}} entities. To use the CLI, see [Setting up the CLI](/docs/codeengine?topic=codeengine-install-cli). 
{: shortdesc}

## Retrieve your Kubernetes configuration with REST API
{: #api-rest}

To retrieve your Kubernetes configuration with REST API,

1. Authenticate with {{site.data.keyword.iamlong}} (IAM) to receive an IAM access token.
2. Query the {{site.data.keyword.cloud_notm}} catalog and the {{site.data.keyword.cloud_notm}} Resource controller to receive a GUID for your project.
3. Use the {{site.data.keyword.codeenginefull_notm}} API to receive a Kubernetes configuration.

### Authenticate with {{site.data.keyword.iamshort}}
{: #api-iam}

[Create your {{site.data.keyword.cloud_notm}} IAM access token](/docs/account?topic=account-manapikey){: external} by making a POST request to `https://iam.cloud.ibm.com/identity/token`.

### Determine the GUID of your {{site.data.keyword.codeengineshort}} project
{: #api-guid}

Determine the GUID of your {{site.data.keyword.codeengineshort}} project by querying the {{site.data.keyword.cloud_notm}} catalog and the {{site.data.keyword.cloud_notm}}. As this GUID does not change, you need to do this step only one time. If you already know your {{site.data.keyword.codeengineshort}} project GUID, you can skip this step.

#### CLI
{: #api-guid-cli}

1. Log in into {{site.data.keyword.cloud_notm}} and target a region, account, and resource group.

    ```txt
    ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
    ```
    {: pre}

2. Run the **`ibmcloud resource`** command.

    ```txt 
    ibmcloud resource service-instances --service-name codeengine --long
    ```
    {: pre}

Identify the service instance that represents your {{site.data.keyword.codeengineshort}} project and determine the GUID from the output.


#### REST API
{: #api-guid-restapi}

Before you begin, you must have the `access_token` from the previous step.

1. Use following {{site.data.keyword.cloud_notm}} catalog API method: [Returns parent catalog entries](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#list-catalog-entries){: external}.

    Example output

    ```txt 
    curl -X GET \
      'https://globalcatalog.cloud.ibm.com/api/v1?include=*&q=name:codeengine+active:true' \
      -H 'Authorization: Bearer ACCESS_TOKEN'
    ```
    {: pre}

    Identify the unique resource ID in the resources list. The field name is `ID` and the JSON path is `resources[].id`.

2. Query the {{site.data.keyword.cloud_notm}} Resource controller with the {{site.data.keyword.cloud_notm}} Resource controller API method [Get a list of all resource instances](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#list-resource-instances){: external}. You must have the {{site.data.keyword.codeengineshort}} project name, the region that your project resides, and the unique resource ID of {{site.data.keyword.codeengineshort}} in the global catalog. Use the name of your {{site.data.keyword.codeengineshort}} project as the query parameter.

    Example output

    ```txt 
    curl -X GET \
        'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
        -H 'Authorization: Bearer ACCESS_TOKEN'
    ```
    {: pre}

    Identify the {{site.data.keyword.codeengineshort}} project from your region in the result list. Find the `guid` output to use in the next steps.

### Query the IBM {{site.data.keyword.codeengineshort}} API
{: #api-query-api}

Before you begin, you must have the following information.

- The `access_token` and `refresh_token` from previous steps.
- The `guid` of your {{site.data.keyword.codeengineshort}} project.
- The region in which your {{site.data.keyword.codeengineshort}} project is located.

Use the [`get kubeconfig for the specified project`](https://cloud.ibm.com/apidocs/codeengine/v1#get-kubeconfig){: external} {{site.data.keyword.codeengineshort}} API method to get the Kubernetes configuration.

#### Example output
{: #api-query-example}

```txt 
curl -X GET \
    'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
    -H 'Authorization: Bearer ACCESS_TOKEN'
```
{: pre}

## Retrieving your Kubernetes configuration with the {{site.data.keyword.codeengineshort}} CLI
{: #api-cli}

1. Log in into {{site.data.keyword.cloud_notm}} and target a region, account, and resource group.

    ```txt
    ibmcloud login target -r REGION -c ACCOUNT_ID -g RESOURCE_GROUP
    ```
    {: pre}

2. Create your {{site.data.keyword.codeengineshort}} project: 

    ```txt
    ibmcloud ce project create --name PROJECT 
    ```
    {: pre}

3. Select your {{site.data.keyword.codeengineshort}} project as the current context and append the project to the default Kubernetes configuration file. 

    ```txt 
    ibmcloud ce project select --name PROJECT --kubecfg
    ```
    {: pre}

Now you are ready to use **`kubectl`** commands with your project.

For more information about using {{site.data.keyword.codeengineshort}} APIs, Kubernetes API, and `kubectl`, see the following topics,

- [{{site.data.keyword.codeengineshort}} API](https://cloud.ibm.com/apidocs/codeengine){: external}
- [Kubernetes REST API](https://kubernetes.io/docs/reference/using-api){: external}
- [Kubernetes API concepts](https://kubernetes.io/docs/reference/using-api/api-concepts/){: external}
- [API client libraries](https://kubernetes.io/docs/reference/#api-client-libraries){: external}
- [**`kubectl`** command](https://kubernetes.io/docs/reference/#cli-reference){: external}

## Custom resource definition (CRD)
{: #api-crd}

The following sections list the custom resource definition methods to use with {{site.data.keyword.codeengineshort}}.

### Batch CRD methods
{: #api-crd-batch}

| Group | Version | Kind |
| --------- | -------- | -------- |
| `codeengine.cloud.ibm.com` | v1beta1 | `JobDefinition` |
| `codeengine.cloud.ibm.com` | v1beta1 | `JobRun` |
{: caption="Batch CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

After you retrieve the Kubernetes configuration, you can view Batch CRD details by using the following methods.

1. Use `kubectl explain --api-version='codeengine.cloud.ibm.com/v1beta1' <Kind>`.
2. [Download Swagger or `OpenAPI` specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.

Note that you cannot delete a job run without also deleting any associated pods. Any attempt to delete with the `propagationPolicy=Orphan` option is rejected.

### Serving CRD methods
{: #api-crd-serving}

| Group | Version | Kind |
| --------- | -------- | -------- |
| `serving.knative.dev` | v1 | Configuration |
| `serving.knative.dev` | v1 | Revision |
| `serving.knative.dev` | v1 | Route |
| `serving.knative.dev` | v1 | Service |
{: caption="Serving CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

For more information about these CRDs, see [Knative Serving API Specification](https://github.com/knative/specs/blob/main/specs/serving/knative-api-specification-1.0.md){: external}.

### Source-to-image CRD methods
{: #api-crd-s2i}

| Group | Version | Kind |
| --------- | -------- | -------- |
| `shipwright.io` | v1beta1 | `Build` |
| `shipwright.io` | v1beta1 | `BuildRun` |
{: caption="Source-to-image CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

After you retrieve the Kubernetes configuration, you can view the Source-to-image CRD details by using one of the following methods.

- Use `kubectl explain --api-version='shipwright.io/v1beta1' <KIND>`.
- [Download the Swagger or `OpenAPI` specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.

### Subscription CRD methods
{: #api-crd-subscription}

| Group | Version | Kind |
| --------- | -------- | -------- |
| `sources.codeengine.cloud.ibm.com` | v1alpha1 | `CosSource` |
| `sources.knative.dev` | v1 | `PingSource` |
{: caption="Subscription CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

After you retrieve the Kubernetes configuration, you can view the Subscription CRD details by using one of the following methods.

- Use `kubectl explain --api-version='sources.knative.dev/<VERSION>' <KIND>`.
- [Download the Swagger or `OpenAPI` specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.


