---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-11"

keywords: command-line interface, kubernetes and code engine cli, knative and code engine cli, kubectl and code engine cli, kubernetes, knative

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Using Kubernetes with {{site.data.keyword.codeengineshort}} 
{: #kubernetes}

{{site.data.keyword.codeenginefull}} is designed so that you do not need to interact with the underlying technology it is built upon. However, if you have existing tools that are based on Kubernetes or Knative, you can still use it with {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} supports the Kubernetes (and Knative) APIs and their CLI commands. For more information about Knative, see [Using Knative with Code Engine](/docs/codeengine?topic=codeengine-knative).
{: shortdesc}

If you decide to use Kubernetes with {{site.data.keyword.codeengineshort}}, consider the following information:

* Most containers or pods that run on Kubernetes also run on {{site.data.keyword.codeengineshort}}.
* Kubernetes constructs, such as deployments, run on {{site.data.keyword.codeengineshort}} if they do not use cluster-wide capabilities, such as security policies. {{site.data.keyword.codeengineshort}} is scoped to what can run in a Kubernetes namespace.

{{site.data.keyword.codeengineshort}} does not support OpenShift-specific resources or other container orchestration platforms, such as Docker Swarm or Compose Swarm.


## Installing the Kubernetes command-line interface
{: #kubernetes-kubectl} 

To install the Kubernetes CLI, download and install the [`kubectl` CLI](https://kubernetes.io/docs/tasks/tools/){: external}.
{: shortdesc}

Be sure to add the `kubectl` binary to your system's PATH environment variable. 
{: tip}

## Interacting with Kubernetes API
{: #kubectl-kubeconfig}


To interact with your project from the Kubernetes command-line interface, `kubectl`, or with Knative, `kn` you must set up your environment to interact with the Kubernetes API of {{site.data.keyword.codeengineshort}}.

Before you begin

- You must [create your project](/docs/codeengine?topic=codeengine-manage-project#create-a-project) and the project must be in `active` status.
- Install the [Kubernetes CLI (`kubectl`)](#knative-kubectl) and the [Knative CLI (`kn`)](#knative-kubectl).

You can set up your environment in the following ways. 

- You can add the `--kubecfg` option to your **`project select`** command. For example, 

    ```txt
    ibmcloud ce project select --name PROJECT_NAME --kubecfg
    ```
    {: pre}

- You can export the `kubeconfig` file directly. Run the **`ibmcloud ce project current`** command to find the project that you are currently targeting. This command also returns the **`export`** command for your `kubeconfig` file. For example,

    ```txt
    ibmcloud ce project current
    ```
    {: pre}

    Example output

    ```txt
    Getting the current project context...
    OK

    Name:       myproject
    ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Subdomain:  aabon2dfwa0
    Domain:     us-south.codeengine.appdomain.cloud
    Region:     us-south
    Kubectl Context:  4svg40kna19

    Kubernetes Config:
    Context:             aabon2dfwa0
    Environment Variable: export KUBECONFIG=/user/myusername/.bluemix/plugins/code-engine/myproject-01234567-abcd-abcd-abcd-abcdabcd1111.yaml
    ```
    {: screen}

    Then, copy the export command, paste it into your command-line interface, and run it.

Verify that your environment is set correctly by running the **`kubectl config`** command.

```txt
kubectl config current-context
```
{: pre}

If the context is correctly set, the output matches the `Kubectl Context` value of your project. For example, if your `Kubectl Context` value of your project is `4svg40kna19`, the command returns `4svg40kna19`.

For more information about Kubernetes and how it works with {{site.data.keyword.codeengineshort}} architecture, see [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).
{: important}
  
## Required access authorities to work with Kubernetes API
{: #kubectl-api}

After you set up your environment, you can interact with Kubernetes API. You must have the correct level of authority for specific tasks. These roles are set in Identity and access management. See [{{site.data.keyword.cloud_notm}} service roles](/docs/codeengine?topic=codeengine-iam#service).

| Resource |  Manager role | Writer role | Reader role |
| --------- | -------------- | ------------ | ------------ |
| `serviceaccounts` | `get`, `list`, `watch` | `get`, `list`, `watch` | None |
| `secrets` | `get`, `list`, `watch`, `create`, `delete`, `update`, `patch`, `apply`, `edit` | `get`, `list`, `watch`, `create`, `delete`, `update`, `patch`, `apply`, `edit` | None |
| `configmaps` | `get`, `list`, `watch`, `create`, `delete`, `update`, `patch`, `apply`, `edit` | `get`, `list`, `watch`, `create`, `delete`, `update`, `patch`, `apply`, `edit` | None |
| `events` | `get`, `list`, `watch` | `get`, `list`, `watch` | None |
| `pods/log` | `get`, `list`, `watch` | `get`, `list`, `watch` | `get`, `list`, `watch` |
| `pods` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch` |
| `services` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch` |
| `pods/exec` | `create` | `create` | None |
| `pods/portforward` | `create` | `create` | None |
| `pods/attach` | `create` | None | None |
| `pods/status` | `get`, `list` | `get`, `list` | None |
| `resourcequotas` | `get`, `list`, `watch` | `get`, `list`, `watch` | get, list, watch |
| `limitranges` | `get`, `list`, `watch` | `get`, `list`, `watch` | None |
| `deployments` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch`, `create`, `delete`, `patch`, `apply` | `get`, `list`, `watch` |
| `daemonset` | `get`, `list`, `watch` | `get`, `list`, `watch` | `get`, `list`, `watch` |
| `pods.metrics.k8s.io` | list | list | list |
{: caption="Table 1. Kubernetes authorities" caption-side=ottom"}



## Retrieving your Kubernetes configuration
{: #kubernetes-getconfig}

You can retrieve your Kubernetes configuration with the [REST API](#api-rest) or the [{{site.data.keyword.codeengineshort}} CLI](#api-cli).

### Retrieve your Kubernetes configuration with REST API
{: #api-rest}

To retrieve your Kubernetes configuration with REST API,

1. Authenticate with {{site.data.keyword.iamlong}} (IAM) to receive an IAM access token.
2. Query the {{site.data.keyword.cloud_notm}} catalog and the {{site.data.keyword.cloud_notm}} Resource controller to receive a GUID for your project.
3. Use the {{site.data.keyword.codeenginefull_notm}} API to receive a Kubernetes configuration.

#### Authenticate with {{site.data.keyword.iamshort}}
{: #api-iam}

[Create your {{site.data.keyword.cloud_notm}} IAM access token](/docs/account?topic=account-manapikey){: external} by making a POST request to `https://iam.cloud.ibm.com/identity/token`.

#### Determine the GUID of your {{site.data.keyword.codeengineshort}} project
{: #api-guid}

Determine the GUID of your {{site.data.keyword.codeengineshort}} project by querying the {{site.data.keyword.cloud_notm}} catalog and the {{site.data.keyword.cloud_notm}}. As this GUID does not change, you need to do this step only one time. If you already know your {{site.data.keyword.codeengineshort}} project GUID, you can skip this step.


To use the {{site.data.keyword.codeengineshort}} CLI to discover the GUID of your {{site.data.keyword.codeengineshort}} project, complete the following steps. 

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

3. Identify the service instance that represents your {{site.data.keyword.codeengineshort}} project and determine the GUID from the output.



To use the REST API to discover the GUID of your {{site.data.keyword.codeengineshort}} project, complete the following steps. 

Before you begin, you must have the `access_token` from the previous step.

1. Use the following {{site.data.keyword.cloud_notm}} catalog API method: [Returns parent catalog entries](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#list-catalog-entries){: external}.

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

3. Identify the {{site.data.keyword.codeengineshort}} project from your region in the result list. Find the `guid` output to use in the next steps.

#### Query the IBM {{site.data.keyword.codeengineshort}} API
{: #api-query-api}

Before you begin, you must have the following information.

- The `access_token` and `refresh_token` from previous steps.
- The `guid` of your {{site.data.keyword.codeengineshort}} project.
- The region in which your {{site.data.keyword.codeengineshort}} project is located.

Use the [`get kubeconfig for the specified project`](https://cloud.ibm.com/apidocs/codeengine/v1#get-kubeconfig){: external} {{site.data.keyword.codeengineshort}} API method to get the Kubernetes configuration.

Example output

```txt 
curl -X GET \
    'https://resource-controller.cloud.ibm.com/v2/resource_instances?name=MY_PROJECT&resource_id=RESOURCE_ID' \
    -H 'Authorization: Bearer ACCESS_TOKEN'
```
{: pre}


### Retrieve your Kubernetes configuration with the {{site.data.keyword.codeengineshort}} CLI
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
{: #kubernetes-api-crd}


The following sections list the custom resource definition methods to use with {{site.data.keyword.codeengineshort}}.

### Batch CRD methods
{: #api-crd-batch}

You can use batch CRDs when [Working with jobs and job runs in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-job-plan).

| Group | Version | Kind |
| --------- | -------- | -------- |
| `codeengine.cloud.ibm.com` | v1beta1 | `JobDefinition` |
| `codeengine.cloud.ibm.com` | v1beta1 | `JobRun` |
{: caption="Batch CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

After you retrieve the Kubernetes configuration, you can view Batch CRD details by using the following methods.

1. Use `kubectl explain --api-version='codeengine.cloud.ibm.com/v1beta1' <Kind>`.
2. [Download Swagger or `OpenAPI` specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.

Note that you cannot delete a job run without also deleting any associated pods. Any attempt to delete with the `propagationPolicy=Orphan` option is rejected.

### Function CRD methods
{: #api-crd-function}

You can use function CRDs when [Working with functions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-work).

| Group | Version | Kind |
| --------- | -------- | -------- |
| `codeengine.cloud.ibm.com` | v1beta1 | `Function` |
{: caption="Function CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

### Serving CRD methods
{: #api-crd-serving}

You can use serving CRDs when [Working with applications in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads).


| Group | Version | Kind |
| --------- | -------- | -------- |
| `serving.knative.dev` | v1 | `Configuration` |
| `serving.knative.dev` | v1 | `Revision` |
| `serving.knative.dev` | v1 | `Route` |
| `serving.knative.dev` | v1 | `Service` |
{: caption="Serving CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

For more information about these CRDs, see [Knative Serving API Specification](https://github.com/knative/specs/blob/main/specs/serving/knative-api-specification-1.0.md){: external}.

### Source-to-image CRD methods
{: #api-crd-s2i}

You can use source-to-image CRDs when [Working with builds and build runs in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-build).


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

You can use subscription CRDs when [Working with with subscriptions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-subscribing-events).

| Group | Version | Kind |
| --------- | -------- | -------- |
| `sources.codeengine.cloud.ibm.com` | v1alpha1 | `CosSource` |
| `sources.knative.dev` | v1beta1 | `KafkaSource` |
| `sources.knative.dev` | v1 | `PingSource` |
{: caption="Subscription CRDs for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

After you retrieve the Kubernetes configuration, you can view the Subscription CRD details by using one of the following methods.

- Use `kubectl explain --api-version='sources.knative.dev/<VERSION>' <KIND>`.
- [Download the Swagger or `OpenAPI` specification of CRDs](https://kubernetes.io/docs/concepts/overview/kubernetes-api/){: external}.








