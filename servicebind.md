---

copyright:
  years: 2020, 2023
lastupdated: "2023-04-25"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}} 
{: #service-binding}

Find out how to integrate an {{site.data.keyword.cloud_notm}} service instance to resources in an {{site.data.keyword.codeenginefull}} project by using service binding.
{: shortdesc}

Service bindings provide applications and jobs access to {{site.data.keyword.cloud_notm}} services.


If you are using the CLI to work with service bindings, and you have service bindings that were created with a version of the CLI **before** CLI 1.27.0, see [considerations](/docs/codeengine?topic=codeengine-service-binding#considerations-previmpl-binding) for information about replacing service bindings that use the previous implementation. To take advantage of the latest enhancements of the CLI, update to the [latest IBM Cloud Code Engine CLI version](/docs/codeengine?topic=codeengine-cli_versions).
{: important}



## What is {{site.data.keyword.codeenginefull_notm}} service binding?
{: #about-service-binding}

Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job automatically adds credentials for a service instance to the environment variables of the container for your application or the job. To see the contents of a service credential, go to the dashboard for the service instance and locate the **Service credentials** page. Service credentials are shown as a JSON object, which, when bound, are added to the application or job environment.

```txt
{
    "apikey": "xxxxxxx",
    "endpoints": "https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints",
    "iam_apikey_description": "Auto-generated for key abcdabcd-abcd-4d8c-78cf-abcdabcdabcd",
    "iam_apikey_name": "my-object-storage-codeengine-credential",
    "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Writer",
    "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/1176a104ad4241e6b0aa82ed0b60c15c::serviceid:ServiceId-abcdabcd-7ae8-abcd-a219-abcdabcdabcd",
    "resource_instance_id": "crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ac4241e6b0cb82ed0b60c15c:abcdabcd-abcd-4777-abcd-d330a450c85b::"
}
```
{: screen}

To bind a service instance to your application or job, you must provision an instance of the service first. Then, use the {{site.data.keyword.codeengineshort}} console or the CLI to bind your app or job to your {{site.data.keyword.cloud_notm}} service instance. 


When you bind a service instance to an app or job, {{site.data.keyword.codeengineshort}} uses a *service access secret* to store the credential of the specified {{site.data.keyword.cloud_notm}} service instance. This type of secret is the key mechanism in a service binding that connects the {{site.data.keyword.cloud_notm}} service instance to a particular {{site.data.keyword.codeengineshort}} app or job. {{site.data.keyword.codeengineshort}} creates and manages this secret for you.


What types of services can I bind?
:    You can add any type of {{site.data.keyword.cloud_notm}} service that is enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) and that uses service credentials to your application or job. To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

I already have service credentials for an {{site.data.keyword.cloud_notm}} service instance. Can I use these credentials with {{site.data.keyword.codeengineshort}} service bindings?
:    Yes, you can bind a service instance to {{site.data.keyword.codeengineshort}} apps and jobs by using existing service credentials. From the console, you can use existing credentials that are already used in a service binding. To use existing service credentials from the CLI, specify the `--service-credential` option in the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) or [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command and provide the name of your service credentials. 

What access is required to create service bindings?
:    Each {{site.data.keyword.codeengineshort}} project must be configured with a set of [IAM Access policies](/docs/account?topic=account-userroles), which authorizes {{site.data.keyword.codeengineshort}} service bindings to view service instances and to view and create service credentials in your account. IAM policies are provided to {{site.data.keyword.codeengineshort}} service binding with a service ID. For more information, see [Configuring access for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess).


Is there a way to configure service binding operations for all users in a project? 
:    Yes! With sufficient permissions, you can use the Integration page in the console to configure service binding operations from a single page. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions. See [Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations). 


## Accessing a bound service instance from an app or job
{: #access-bound-service}

{{site.data.keyword.codeengineshort}} provides environment variables for accessing service instances that are bound to your apps or jobs with both the [`CE_SERVICES`](#ce-services) and [`PREFIX`](#prefix-method) methods.

* The `CE_SERVICES` environment variable is a single environment variable that contains all service binding information as a JSON object. 

* {{site.data.keyword.codeengineshort}} also creates multiple environment variables for your service binding, which are based on the variables in the service credential for your service instance. To distinguish these multiple environment variables for your service binding, you can use a `PREFIX` such that these environment variables use the same prefix. If you do not specify a custom prefix, {{site.data.keyword.codeengineshort}} automatically generates a prefix. 

If your application or job wants to talk to a bound service by using private networking and the service has both `private` and `direct` endpoints (such as {{site.data.keyword.cos_full_notm}}), then the `direct` endpoints must be used.
{: important}

### `CE_SERVICES` environment variable
{: #ce-services}

The `CE_SERVICES` environment variable contains information that you can use to interact with a service instance. This environment variable points to a JSON object that contains key value pairs. These key value pairs represent each type of service that is bound to your application. The `key` is the name of the service type, such as `cloud-object-storage`, and the `value` is an array of credentials for bound service instances of that type.

The following example illustrates a `CE_SERVICES` variable:

```txt
{
  "appid": [
    {
      "credentials": {
        "apikey": "xxxxxx",
        "appidServiceEndpoint": "https://us-south.appid.test.cloud.ibm.com",
        "clientId": "abcdabcd-xxxxxxxx",
        "discoveryEndpoint": "https://us-south.appid.test.cloud.ibm.com/oauth/v4/xxxxxxxx/.well-known/openid-configuration",
        "iam_apikey_description": "Auto-generated for key crn:v1:staging:public:appid:us-south:a/abcdabcd719f45b98a931f6e20db1bd8:xxxxxxxx:resource-key:abcdabcd-xxxxxxxx",
        "iam_apikey_name": "ce-service-access-abcd",
        "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Writer",
        "iam_serviceid_crn": "crn:v1:staging:public:iam-identity::a/abcdabcd719f45b98a931f6e20db1bd8::serviceid:ServiceId-6d7087e5-0611-4240-9e46-af8a4c15cba4",
        "managementUrl": "https://us-south.appid.test.cloud.ibm.com/management/v4/xxxxxxxx",
        "oauthServerUrl": "https://us-south.appid.test.cloud.ibm.com/oauth/v4/xxxxxxxx",
        "profilesUrl": "https://us-south.appid.test.cloud.ibm.com",
        "secret": "abcdabcdYTAtZmU0MC00YTQ1LTliY2YtMDk0ODg0NDMyNDgw",
        "tenantId": "xxxxxxxx",
        "version": 4
      },
      "name": "App ID-yn",
      "plan": "c0258a22-160a-403b-845d-1588ad61204c",
      "resourcekey_name": "ce-service-access-abcd",
      "resourcekey_id": "abcdabcd-xxxxxxxx"
    }
  ],
  "cloud-object-storage": [
    {
      "credentials": {
        "apikey": "xxxxxx",
        "endpoints": "https://control.cloud-object-storage.test.cloud.ibm.com/v2/endpoints",
        "iam_apikey_description": "Auto-generated for key crn:v1:staging:public:cloud-object-storage:global:a/abcdabcd719f45b98a931f6e20db1bd8:abcdabcd-34b3-4edf-95b7-abcdabcdabcd:resource-key:abcdabcd-96e0-46ef-b805-31288524f194",
        "iam_apikey_name": "ce-service-access-c5yn1",
        "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Writer",
        "iam_serviceid_crn": "crn:v1:staging:public:iam-identity::a/abcdabcd719f45b98a931f6e20db1bd8::serviceid:ServiceId-ee6394cb-f203-4c3c-9152-ac886a3f66bb",
        "resource_instance_id": "crn:v1:staging:public:cloud-object-storage:global:a/abcdabcd719f45b98a931f6e20db1bd8:abcdabcd-34b3-4edf-95b7-abcdabcdabcd::"
      },
      "name": "Cloud Object Storage-56",
      "plan": "2fdf0c08-2d32-4f46-84b5-32e0c92fffd8",
      "resourcekey_name": "ce-service-access-c5yn1",
      "resourcekey_id": "abcdabcd-96e0-46ef-b805-31288524f194"
    }
  ]
}
```
{: screen}

### Prefix method
{: #prefix-method}

With the prefix method, for each credential variable in a service credential object, that variable is provided individually to your environment by using the common environment variable syntax of capital letters that are separated by underscores, such as `VARIABLE_NAME`.

By default, the variable name is the name of the service, followed by the name of credential variable. For example, an {{site.data.keyword.cos_full_notm}} service credential variable that is named `apikey` is available in an environment variable that is called `CLOUD_OBJECT_STORAGE_APIKEY`. The following example shows the environment variables that are created for an {{site.data.keyword.cos_full_notm}} service instance binding.

```txt
CLOUD_OBJECT_STORAGE_APIKEY=xxxxxx
CLOUD_OBJECT_STORAGE_ENDPOINTS=https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints
CLOUD_OBJECT_STORAGE_IAM_APIKEY_DESCRIPTION=Auto-generated for key abcdabcd-abcd-abcd-abcd-abcdabcdabcd
CLOUD_OBJECT_STORAGE_IAM_APIKEY_NAME=my-object-storage-codeengine-credential
CLOUD_OBJECT_STORAGE_IAM_ROLE_CRN=crn:v1:bluemix:public:iam::::serviceRole:Manager
CLOUD_OBJECT_STORAGE_IAM_SERVICEID_CRN=crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-abcdabcd-abcd-abcd-8b41-531fc64e640e
CLOUD_OBJECT_STORAGE_RESOURCE_INSTANCE_ID=crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ad4441e6b0aa92ed0b60b15c:11179ac4-abcd-4887-abcd-d330a430abcd::
CLOUD_OBJECT_STORAGE_SERVICENAME=my-object-storage
```
{: screen}

By default, if more than one instance of the same type is bound to a single application, {{site.data.keyword.codeengineshort}} appends an index to the service name, such as `CLOUD_OBJECT_STORAGE_2_APIKEY`.

Each service binding can be configured to use a custom environment variable prefix. If you are using the console, you can optionally provide a prefix when you create the service binding. If you are using the CLI, use the `--prefix` option with the **`app bind`** or **`job bind`** command.


## What should I consider if I have service bindings that use the previous implementation? 
{: #considerations-previmpl-binding}

CLI 1.27.0 introduced an improved service binding implementation, which is used for all bindings that are created with this version or later. Service bindings that were created with a version of the CLI **before** CLI 1.27.0 are using the previous service binding implementation. Applications and jobs that have service bindings that use the previous implementation continue to function normally regarding access to the bound services. However, if you want to change service bindings that use the previous implementation, consider the following information. 

* You cannot have a mixture of previous implementation and improved implementation service bindings for the same app or job. Before you can add new service bindings to an app or job that has service bindings that use the previous implementation, you must unbind all these service bindings. You can then re-create them with the improved implementation and add new service bindings.  
* You cannot individually unbind these service bindings. You must remove them all by using the **`app unbind --all`** or **`job unbind --all`** command.

To take advantage of the latest enhancements and continue to manage service bindings for your apps and jobs easily, update to the [latest IBM Cloud Code Engine CLI version](/docs/codeengine?topic=codeengine-cli_versions) and [replace service bindings that use the previous implementation](/docs/codeengine?topic=codeengine-service-binding#replaceprevimpl-binding).
{: tip}

### How can I replace a service binding that uses the previous implementation?
{: #replaceprevimpl-binding}

If your app or job has service bindings that use the previous implementation, and you want to add new service bindings to your app or job, you must first remove the bindings that use the previous implementation before new bindings are created. You can re-create those existing service bindings if needed. 

Your application might not be fully functional during the process of unbinding and rebinding.
{: note}

1. To discover if your app or job uses the previous implementation of service bindings, run the **`app get`** or **`job get`** command. If the previous service binding implementation is used, the output of this command provides the information, and the commands that you must use to bind another service to the application or job. For example, 

    ```txt
    ibmcloud ce app get --name myapp
    ```
    {: pre}

    Example output

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

    Example output

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

## Next steps
{: #service-binding-nextsteps}

Before you can bind a service instance to a {{site.data.keyword.codeengineshort}} application or job, you must configure access for bindings. See [Configuring access for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess).
