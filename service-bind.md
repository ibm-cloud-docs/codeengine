---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-07"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Integrating {{site.data.keyword.cloud_notm}} services with service binding
{: #service-binding}

Find out how to integrate an {{site.data.keyword.cloud_notm}} service instance to resources in an {{site.data.keyword.codeenginefull}} project by using service binding.
{: shortdesc} 

Service bindings provide applications and jobs access to {{site.data.keyword.cloud_notm}} services.



To take advantage of the latest enhancements and continue to manage service bindings for your apps and jobs easily, update to the [latest IBM Cloud Code Engine CLI version](/docs/codeengine?topic=codeengine-cli_versions) and [replace service bindings that use the previous implementation](/docs/codeengine?topic=codeengine-service-binding#replaceprevimpl-binding).
{: tip}

If you created service bindings with a version of the CLI **before** CLI 1.27.0, see  [considerations](/docs/codeengine?topic=codeengine-service-binding#considerations-previmpl-binding).
{: important}



## What is {{site.data.keyword.codeenginefull_notm}} service binding?
{: #about-service-binding}

Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job automatically adds credentials for a service instance to the environment variables of the container for your application or the job. To see the contents of a service credential, go to the dashboard for the service instance and locate the **Service credentials** page. Service credentials are shown as a JSON object, which, when bound, are added to the application or job environment.

```txt
{
    "apikey": "xxxxxxx",
    "endpoints": "https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints",
    "iam_apikey_description": "Auto-generated for key 1d3eb853-4ef1-4d8c-78cf-d2630d872a82",
    "iam_apikey_name": "my-object-storage-codeengine-credential",
    "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Writer",
    "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/1176a104ad4241e6b0aa82ed0b60c15c::serviceid:ServiceId-c3081ceb-7ae8-4769-a219-49403c474cc7",
    "resource_instance_id": "crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ac4241e6b0cb82ed0b60c15c:11179bc4-3736-4777-9c8e-d330a450c85b::"
}
```
{: screen}

To bind a service instance to your application or job, you must provision an instance of the service first. Then, use the **`application bind`** or **`job bind`** command to configure service credentials and secrets. Secrets are automatically encrypted to protect your data.

What types of services can I bind?
:    You can add any type of {{site.data.keyword.cloud_notm}} service that is enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to your application or job. To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

I already have service credentials for an {{site.data.keyword.cloud_notm}} service instance. Can I use these credentials with {{site.data.keyword.codeengineshort}} service bindings?
:    Yes, you can bind a service instance to {{site.data.keyword.codeengineshort}} apps and jobs by using existing service credentials. To use existing service credentials, specify the `--service-credential` option in the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) or [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command and provide the name of your service credentials.

## What access do I need to create service bindings?
{: #service-binding-access}

Each {{site.data.keyword.codeengineshort}} project must be configured with a set of [IAM Access policies](/docs/account?topic=account-userroles), which authorizes {{site.data.keyword.codeengineshort}} service binding to view service instances and to view and create service credentials in your account. IAM policies are provided to {{site.data.keyword.codeengineshort}} service binding with a Service ID.

What policies does a {{site.data.keyword.codeengineshort}} Service ID need to create a service binding?
:    To create service bindings in a project, the project must be configured with a Service ID that contains the proper access policies. Each policy consists of a role and an IAM-enabled entity.

:    The required roles are,
     * The Operator role, which is required to create new service credentials or to reference existing service credentials for a service instance
     * The appropriate service roles (Reader, Writer, Manager, or custom service roles). For example, to create a Writer credential for a service instance, the Service ID needs at least a Writer role for that service instance. Note that assigning the Manager role to the Service ID is also sufficient to create a Writer role, but Reader is not.

:    The IAM-enabled entities to which you can apply these roles include,
     * Individual service instances
     * Service types
     * Resource groups

What policies does a user need to create a {{site.data.keyword.codeengineshort}} service binding Service ID?
:    You must have one or more platform Administrator policies to delegate permissions to a Service ID. The Administrator policies must cover the resource groups, service types, or service instances, which are configured in the {{site.data.keyword.codeengineshort}} service binding Service ID.
:    More information about IAM access policies and service IDs, see [IAM documentation](/docs/account?topic=account-iamoverview)

## How can I access a bound service instance from an app or job?
{: #access-bound-service}

Use environment variables to access your bound service credentials with one of following methods: the [`CE_SERVICES`](#ce-services) method or the [Prefix](#prefix-method) method.

If your application or job wants to talk to a bound service by using private networking and the service has both `private` and `direct` endpoints (such as {{site.data.keyword.cos_full_notm}}), then the `direct` endpoints must be used.
{: important}

### `CE_SERVICES` method
{: #ce-services}

The `CE_SERVICES` environment variable contains information that you can use to interact with a service instance. This environment variable points to a JSON object that contains key value pairs. These key value pairs represent each type of service that is bound to your application. The `key` is the name of the service type, such as `cloud-object-storage`, and the `value` is an array of credentials for bound service instances of that type.

The following example illustrates a `CE_SERVICES` variable:

```txt
{
    "cloud-object-storage": [
        {
            "credentials": {
                "apikey": "xxxxxxx",
                "endpoints": "https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints",
                "iam_apikey_description": "Auto-generated for key 1d3eb853-4ef1-4d8c-78cf-d2630d872a82",
                "iam_apikey_name": "my-object-storage-codeengine-credential",
                "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Writer",
                "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-c3081ceb-7ae8-4769-a219-49403c474cc7",
                "resource_instance_id": "crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ad4441e6b0aa92ed0b60b15c:11179ac4-3736-4887-9c8e-d330a430c85a::"
            },
            "name": "my-object-storage",
            "plan": "standard"
        }
    ],
    "language-translator": [
        {
            "credentials": {
                "apikey": "xxxxxx",
                "iam_apikey_description": "Auto-generated for key 1d3eb853-4ef1-4d8c-78cf-d2630d872a82",
                "iam_apikey_name": "my-language-translator-codeengine-credential",
                "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",
                "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-81f9b539-e679-45ed-a01b-9bccb354ca21",
                "url": "https://api.us-south.language-translator.watson.cloud.ibm.com/instances/3d487cc7-8562-4a77-b700-803738ba4946"
            },
            "name": "my-language-translator",
            "plan": "standard"
        },
        {
            "credentials": {
                "apikey": "xxxxxx",
                "iam_apikey_description": "Auto-generated for key 1d3eb853-4ef1-4d8c-78cf-d2630d872a82,
                "iam_apikey_name": "another-language-translator-codeengine-credential",
                "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",
                "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-9b77862b-f084-4958-850a-3e1ecc95e03f",
                "url": "https://api.us-south.language-translator.watson.cloud.ibm.com/instances/535b21b3-7c47-4c0e-92e4-e32b5152b5b6"
            },
            "name": "another-language-translator",
            "plan": "standard"
        }
    ]
}
```
{: screen}


### Prefix method
{: #prefix-method}

With the prefix method, for each credential variable in a service credential object, that variable is provided individually to your environment by using the common environment variable syntax of capital letters that are separated by underscores, such as `VARIABLE_NAME`.

By default, the variable name is the name of the service, followed by the name of credential variable. For example, an {{site.data.keyword.cos_full_notm}} service credential variable that is named `apikey` is available in an environment variable called `CLOUD_OBJECT_STORAGE_APIKEY`. The following example shows the environment variables that are created for an {{site.data.keyword.cos_full_notm}} service instance binding.

```txt
CLOUD_OBJECT_STORAGE_APIKEY=xxxxxx
CLOUD_OBJECT_STORAGE_ENDPOINTS=https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints
CLOUD_OBJECT_STORAGE_IAM_APIKEY_DESCRIPTION=Auto-generated for key b1c66882-d87a-424c-bbb0-6afaceed6234
CLOUD_OBJECT_STORAGE_IAM_APIKEY_NAME=my-object-storage-codeengine-credential
CLOUD_OBJECT_STORAGE_IAM_ROLE_CRN=crn:v1:bluemix:public:iam::::serviceRole:Manager
CLOUD_OBJECT_STORAGE_IAM_SERVICEID_CRN=crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-ddf06b7e-c6fd-4a4c-8b41-531fc64e640e
CLOUD_OBJECT_STORAGE_RESOURCE_INSTANCE_ID=crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ad4441e6b0aa92ed0b60b15c:11179ac4-3736-4887-9c8e-d330a430c85a::
CLOUD_OBJECT_STORAGE_SERVICENAME=my-object-storage
```
{: screen}

By default, if more than one instance of the same type is bound to a single application, {{site.data.keyword.codeengineshort}} appends an index to the service name, such as `CLOUD_OBJECT_STORAGE_2_APIKEY`.

Each service binding can be configured to use a custom environment variable prefix by using the `--prefix` option.

## Configure access policies for a service binding
{: #configure-binding}

Before you can bind a service instance, your {{site.data.keyword.codeengineshort}} project must be configured to create service bindings. For more information about service binding access requirements, see [Service Binding access](#service-binding-access).

Before you begin

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.

### Use the default service binding access policies
{: #service-bind-option1}

When you create a service binding in a project, {{site.data.keyword.codeengineshort}} checks to see whether the project is already configured for service binding. If a project is not configured, {{site.data.keyword.codeengineshort}} creates a Service ID for the project with Operator and Manager access for all services in the project resource group.

If you have insufficient permissions to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you. If you want more control over access policies, you can set them manually by configuring your project for access to your resource group or with a custom service ID.  

### (Optional) Manually configure a project for access to a resource group
{: #service-bind-option2}

To configure a {{site.data.keyword.codeengineshort}} project for service binding access for all service instances in a resource group, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

To configure service binding access for all service instances in the **Default** resource group,

```txt
ibmcloud ce project update --binding-resource-group Default
```
{: pre}

Note that the **`project update`** command works within the project that is selected as the current context. Use the [**`ibmcloud ce project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to display all projects, including information for the selected project. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context. 

To configure service binding access for all service instances in _all_ resource groups:

```txt
ibmcloud ce project update --binding-resource-group "*"
```
{: pre}

When you run the **`project update`** command, a service ID is created for the project and is used to configure the current project for service bindings. If you do not have permission to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you.

### (Optional) Manually configure a project with a custom service ID
{: #service-bind-option3}

To configure a {{site.data.keyword.codeengineshort}} project for service binding with a custom Service ID, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.
1. Create a Service ID with the policies required for your service binding needs. For more information about working with Service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
2. Find the ID of your Service ID by clicking Details on your Service ID page or else run `ibmcloud iam service-ids`.
3. Run the **`ibmcloud ce project update`** command.

    For example, if the ID of your Service ID is `ServiceId-12a3456b-c78d-901e-f2a3b4c56de7`:

    ```txt
    ibmcloud ce project update --binding-service-id ServiceId-12a3456b-c78d-901e-f2a3b4c56de7
    ```
    {: pre}

Note that the **`project update`** command works within the project that is selected as the current context. Use the [**`ibmcloud ce project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to display all projects, including information for the selected project. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context. 

## Bind a service instance to a {{site.data.keyword.codeengineshort}} application or job
{: #bind}

Before you begin

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* Create the service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.

    For example, to create an {{site.data.keyword.cos_full_notm}} service instance (Lite plan):

    ```txt
    ibmcloud resource service-instance-create my-object-storage cloud-object-storage lite global -g Default
    ```
    {: pre}

* Create a {{site.data.keyword.codeengineshort}} application.

    For example, to create an application that is called `my-application` that uses the `icr.io/codeengine/hello` image:

    ```txt
    ibmcloud ce application create --name my-application --image icr.io/codeengine/hello
    ```
    {: pre}


### Binding a service instance with a new credential
{: #bind-credentials}

To bind your new service instance to your {{site.data.keyword.codeengineshort}} application and generate a new service credential, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with the default service role. The default service role is either Manager or the first role that is provided by the service if Manager is not supported. The following example **`application bind`** command binds the `my-object-storage` service instance with the app called `my-application`. A new service credential with the Manager role is generated for this binding action.

    ```txt
    ibmcloud ce application bind --name my-application --service-instance my-object-storage
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the application to bind. This value is required. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the application. This value is required. |
    {: caption="Table 1. Command options" caption-side="bottom"}

    **Example output**

    ```txt
    Binding service instance...
    Status: Done
    Waiting for application revision to become ready...
    The Configuration is still working to reflect the latest desired specification.
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready.
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage     cloud-object-storag   Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}

### Binding a service instance with a particular role
{: #bind-credentials-role}

To bind a service instance to your {{site.data.keyword.codeengineshort}} application and generate new service credentials with a particular role, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with a particular service role. For more information about IAM service roles, see [Service access roles](/docs/account?topic=account-userroles#service_access_roles). The following example **`application bind`** command binds the `my-object-storage` service instance to the app called `my-application` by using the Writer service role. A new service credential with the Writer role is generated for this binding action.

    ```txt
    ibmcloud ce application bind --name my-application --service-instance my-object-storage --role Writer
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the application to bind. This value is required. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the application. This value is required. |
    | `--role` | The name of a service role for the new service credential that is created for this service binding. Valid values include `Reader`, `Writer`, `Manager`, or a service-specific role. If the `--role` option is not specified, the default is `Manager` or the first role that is provided by the service if `Manager` is not supported. This option is ignored if `--service-credential` is specified. |
    {: caption="Table 2. Command options" caption-side="bottom"}

    **Example output**

    ```txt
    Binding service instance...
    Status: Done
    Waiting for application revision to become ready...
    The Configuration is still working to reflect the latest desired specification.
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready.
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage  cloud-object-storage     Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}   

### Binding a service instance with existing credentials
{: #bind-existing-credentials}

If you already created a credential for your service instance and want to use it for your service binding, add the `--service-credentials` option.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Find the credentials of the service instance.

    ```txt
    ibmcloud resource service-keys --instance-name INSTANCENAME
    ```
    {: pre}
    
    **Example output**
    
    ```txt
    Name                State    Created At       
    my-cos-credential   active   Tue Mar  2 01:15:33 UTC 2021 
    ```
    {: screen}
    
    To see details of a service credential, run `ibmcloud resource service-key KEYNAME`. You can find all the service keys in your resource group by running `ibmcloud resource service-keys`.
    {: tip}

3. Bind the service instance to the application or job with existing credentials. For example, the following **`job bind`** command binds the `my-object-storage` service instance with existing service credentials called `my-cos-credential` to an existing job that is called `myjob`.

    ```txt
    ibmcloud ce job bind --name myjob --service-instance my-object-storage --service-credential my-cos-credential
    ```
    {: pre}

    The following table summarizes the options that are used with the **`job bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the job to bind. This value is required. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the job. This value is required. |
    | `--service-credential` | The name of the existing service credential to bind. |
    {: caption="Table 3. Command options" caption-side="bottom"}

4. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce job get --name myjob
    ```
    {: pre}

    **Example output**

    ```txt
    [...]
    Service Bindings:
    Name                                 ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    myjob-ce-service-binding-abcde       abcde645-d3f9-407d-b964-6c3ae69abcde  myfmo-object-storage  cloud-object-storage  my-cos-credential  CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen} 

## Unbinding service instances
{: #unbind}

Unbinding service instances from an application or job removes existing service bindings.

1. Find the service binding that you want to remove with the **`application get`** or **`job get`** command; for example, 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage     cloud-object-storage  Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}

2. Remove the service binding by using the **`application unbind`** or the **`job unbind`** command.

    * To remove a single binding, specify the `--name` and `--binding` options. 

        ```txt
        ibmcloud ce application unbind --name APPLICATION_NAME --binding BINDING_NAME
        ```
        {: pre}

    * To unbind all service instances, use the `--all` option.

        ```txt
        ibmcloud ce job unbind --name JOB_NAME --all
        ```
        {: pre}


## What should I consider if I have service bindings that use the previous implementation? 
{: #considerations-previmpl-binding}

CLI 1.27.0 introduced an improved service binding implementation, which is used for all bindings that are created with this version or later. Service bindings that were created with a version of the CLI **before** CLI 1.27.0 are using the previous service binding implementation. Applications and jobs that have service bindings that use the previous implementation continue to function normally regarding access to the bound services. However, if you want to change service bindings that use the previous implementation, consider the following information. 

* You cannot have a mixture of previous implementation and improved implementation service bindings for the same app or job. Before you can add new service bindings to an app or job that has service bindings that use the previous implementation, you must unbind all of these service bindings. You can then re-create them with the improved implementation and add new service bindings.  
* You cannot individually unbind these service bindings. You must remove them all by using the **`app unbind --all`** or **`job unbind--all`** command.

To take advantage of the latest enhancements and continue to manage service bindings for your apps and jobs easily, update to the [latest IBM Cloud Code Engine CLI version](/docs/codeengine?topic=codeengine-cli_versions) and [replace service bindings that use the previous implementation](/docs/codeengine?topic=codeengine-service-binding#replaceprevimpl-binding).
{: tip}


### How can I replace a service binding that uses the previous implementation?
{: #replaceprevimpl-binding}

If your app or job has service bindings that use the previous implementation, and you want to add new service bindings to your app or job, you must first remove the bindings that use the previous implementation before new bindings are created. You can re-create those existing service bindings if needed. 

Your application might not be fully functional during the process of unbinding and rebinding.
{: note}

1. To discover if your app or job uses the previous implementation of service bindings, run the **`app get`** or **`job get`** command. If the previous service binding implementation is used, the output of this command provides the information and the commands that you must use to bind an additional service to the application or job. For example, 

    ```txt
    ibmcloud ce app get --name myapp
    ```
    {: pre}

    **Example output**

    ```txt
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    This application uses a previous service binding implementation.
    Your application will continue to function normally.
    To bind an additional service to this application, delete and re-create those service bindings with the improved implementation.
    Your application might not be fully functional during the process of unbinding and rebinding.
    Re-create the existing service bindings by issuing the following commands:
    (1) Remove all existing service bindings from this application.
    ibmcloud ce application unbind --name myapp -all
    (2) Bind the services again.
    ibmcloud ce application bind --name myapp --service-instance myobjectstorage --prefix CLOUD_OBJECT_STORAGE

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                2m4s
    Created:            2021-09-09T14:01:02-04:00
    URL:                https://myapp.abcdabcdabc.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.abcdabcdabc.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:     Application deployed successfully
    [...]
    Service Bindings:
    Service Instance    Service Type           Environment Variable Prefix  
    myobjectstorage     cloud-object-storage   CLOUD_OBJECT_STORAGE  
    ```
    {: screen}

    Similarly, if you are working with jobs, run the `ibmcloud ce job get --name JOB_NAME` command to discover if deprecated bindings are used with your job.


2. Unbind the existing service bindings that use the previous implementation. The `--all` option specifies to unbind all service instances for this application.

    ```txt
    ibmcloud ce app unbind --name APP_NAME --all
    ```
    {: pre}

   Similarly, if you are working with jobs, run the `ibmcloud ce job unbind --name JOB_NAME --all` command to unbind all service instances for your job. 

3. Create new bindings. To create new bindings, run the [**`ibmcloud ce app bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) or [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command. To replace service binding that used the previous implementation, use the commands that are provided in the output of the `app get` or `job get` commands. For example, to re-create an existing binding from the {{site.data.keyword.codeengineshort}} application, `myapp`, to the {{site.data.keyword.cos_full_notm}} service instance, `myobjectstorage`, 

    ```txt
    ibmcloud ce app bind --name myapp --service-instance myobjectstorage --prefix CLOUD_OBJECT_STORAGE
    ```
    {: pre}

    Similarly, if you are working with jobs, run the `ibmcloud ce job bind --name JOB_NAME ---service-instance SERVICE_INSTANCE --prefix PREFIX` command. 

    Repeat this step for each binding that you want to re-create.  

4. (optional) Run the **`app get`** or **`job get`**  command again. This time, notice that the output of the command does not display the information about service bindings with a previous implementation. For example,    

    ```txt
    ibmcloud ce app get --name myapp
    ```
    {: pre}

    **Example output**

    ```txt
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                2m4s
    Created:            2021-09-09T14:01:02-04:00
    URL:                https://myapp.abcdabcdabc.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.abcdabcdabc.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:     Application deployed successfully
    [...]

    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    myapp-app-ce-service-binding-abcde          abcde5d3-dfc3-4f52-b133-b869b5eabcde   my-object-storage    cloud-object-storage   Writer             CLOUD_OBJECT_STORAGE
    ```
    {: screen}



