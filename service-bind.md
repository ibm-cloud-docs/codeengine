---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-20"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Integrating {{site.data.keyword.cloud_notm}} services with service binding
{: #service-binding}

Find out how to integrate an {{site.data.keyword.cloud_notm}} service instance to resources in an {{site.data.keyword.codeenginefull}} project by using service binding.
{: shortdesc} 

Service bindings provide applications and jobs access to {{site.data.keyword.cloud_notm}} services.



## What is {{site.data.keyword.cloud_notm}} service binding?
{: #about-service-binding}

Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job automatically adds credentials for a service instance to the environment variables of the container for your application or the job. To see the contents of a service credential, go to the dashboard for the service instance and locate the **Service credentials** page. Service credentials are shown as a JSON object, which, when bound, are added to the application or job environment.

```
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

**What types of services can I bind?**

You can add any type of {{site.data.keyword.cloud_notm}} service that is enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to your application or job. To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

**I already have service credentials for an {{site.data.keyword.cloud_notm}} service instance. Can I still use {{site.data.keyword.cloud_notm}} service binding?**

Yes, you can bind a service instance by using existing service credentials. To use existing service credentials, specify the `--service-credential` option in the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) or [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command and provide the name of your service credentials.

## What access do I need to create service bindings?
{: #service-binding-access}

Each {{site.data.keyword.codeengineshort}} project must be configured with a set of [IAM Access Policies](/docs/account?topic=account-userroles), which authorizes {{site.data.keyword.codeengineshort}} service binding to view service instances and to view and create service credentials in your account. IAM policies are provided to {{site.data.keyword.codeengineshort}} service binding with a Service ID.

**What policies does a {{site.data.keyword.codeengineshort}} Service ID need in order to create a service binding?**
To create service bindings in a project, the project must be configured with a Service ID that contains the proper access policies. Each policy consists of a role and an IAM-enabled entity.

The required roles are,
* The Operator role, which is required to create new service credentials or to reference existing service credentials for a service instance
* The appropriate service roles (Reader, Writer, Manager, or custom service roles). For example, in order to create a Writer credential for a service instance, the Service ID needs at least a Writer role for that service instance. Note that assigning the Manager role to the Service ID is also sufficient to create a Writer role, but Reader is not.

The IAM-enabled entities to which you can apply these roles include,
* Individual service instances
* Service types
* Resource groups

**What policies does a user need to create a {{site.data.keyword.codeengineshort}} service binding Service ID?**
You must have one or more platform Administrator policies to delegate permissions to a Service ID. The Administrator policies must cover the resource groups, service types or service instances, which are configured in the {{site.data.keyword.codeengineshort}} service binding Service ID.

More information about IAM access policies and service IDs, see [IAM documentation](/docs/account?topic=account-iamoverview)

## How can I access a bound service instance from an app or job?
{: #access-bound-service}

Use environment variables to access your bound service credentials with one of following methods: the [`CE_SERVICES`](#ce-services) method or the [Prefix](#prefix-method) method.

### `CE_SERVICES` method
{: #ce-services}

The `CE_SERVICES` environment variable contains information that you can use to interact with a service instance. This environment variable points to a JSON object that contains key value pairs. These key value pairs represent each type of service that is bound to your application. The `key` is the name of the service type, such as `cloud-object-storage`, and the `value` is an array of credentials for bound service instances of that type.

The following example illustrates a `CE_SERVICES` variable:

```
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

```
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

## Configure a {{site.data.keyword.codeengineshort}} project for service binding
{: #configure-binding}

Before you can bind a service instance, your {{site.data.keyword.codeengineshort}} project must be configured to create service bindings. For more information about service binding access requirements, see [Service Binding access](#service-binding-access).

**Before you begin**

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.

### Option 1: Use the default service binding access policies
{: #service-bind-option1}

When you create a service binding in a project, {{site.data.keyword.codeengineshort}} checks to see if the project is already configured for service binding. If a project is not configured, {{site.data.keyword.codeengineshort}} creates a Service ID for the project with Operator and Manager access for all services in the project resource group.

If you have insufficient permissions to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you.

### Option 2: Manually configure a project for access to a resource group
{: #service-bind-option2}

To configure a {{site.data.keyword.codeengineshort}} project for service binding access for all service instances in a resource group, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

To configure service binding access for all service instances in the **Default** resource group,

```
ibmcloud ce project update --binding-resource-group Default
```
{: pre}

To configure service binding access for all service instances in _all_ resource groups:

```
ibmcloud ce project update --binding-resource-group "*"
```
{: pre}

When you run the **`project update`** command, a service ID is created for the project and is used to configure the current project for service bindings. If you do not have permission to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you.

### Option 3: Manually configure a project with a custom service ID
{: #service-bind-option3}

To configure a {{site.data.keyword.codeengineshort}} project for service binding with a custom Service ID, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.
1. Create a Service ID with the policies required for your service binding needs. For more information about working with Service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
2. Find the ID of your Service ID by clicking Details on your Service ID page or else run `ibmcloud iam service-ids`.
3. Run the **`ibmcloud ce project update`** command.

    For example, if the ID of your Service ID is `ServiceId-12a3456b-c78d-901e-f2a3b4c56de7`:

    ```
    ibmcloud ce project update --binding-service-id ServiceId-12a3456b-c78d-901e-f2a3b4c56de7
    ```
    {: pre}

## Bind a service instance to a {{site.data.keyword.codeengineshort}} application or job
{: #bind}

**Before you begin**

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* Create the service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.

    For example, to create an {{site.data.keyword.cos_full_notm}} service instance (Lite plan):

    ```
    ibmcloud resource service-instance-create my-object-storage cloud-object-storage lite global -g Default
    ```
    {: pre}

* Create a {{site.data.keyword.codeengineshort}} application.

    For example, to create an application that is called `my-application` that uses the `ibmcom/hello` image:

    ```
    ibmcloud ce application create --name my-application --image ibmcom/hello
    ```
    {: pre}


### Binding a service instance with a new credential
{: #bind-credentials}

To bind your new service instance to your {{site.data.keyword.codeengineshort}} application and generate a new service credential, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all of the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```
    Name                Location   State    Type        
    my-object-storage   global     active   service_instance   
    tone_analyzer1      us-south   active   service_instance   
    tone_analyzer2      us-south   active   service_instance 
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with the default service role. The default service role is either Manager or the first role that is provided by the service if Manager is not supported. The following example **`application bind`** command binds the `my-object-storage` service instance with the app called `my-application`. A new service credential with the Manager role is generated for this binding action.

    ```
    ibmcloud ce application bind --name my-application --service-instance my-object-storage
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    <table>
    <caption><code>application bind</code> components</caption>
    <thead>
    <col width="25%">
    <col width="75%">
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--name</code></td>
    <td>The name of the application to bind. This value is required.</td>
    </tr>
    <tr>
    <td><code>--service-instance</code></td>
    <td>Specify the name of an existing service instance to bind to the application. This value is required.</td>
    </tr>
    </tbody>
    </table>

    **Example output**

    ```
    Binding service instance...
    Waiting for service binding to become ready...
    Status: Pending (Processing Resource)
    Status: Creating service binding
    Status: Ready
    Waiting for application revision to become ready...
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```
    [...]
    Service Bindings:
    Name              Service Instance   Service Type          Role / Credential  Environment Variable Prefix  Status  
    ce-binding-abcde  my-object-storage  cloud-object-storage  Manager            CLOUD_OBJECT_STORAGE         Ready 
    [...]
    ```
    {: screen}

### Binding a service instance with a particular role
{: #bind-credentials-role}

To bind a service instance to your {{site.data.keyword.codeengineshort}} application and generate new service credentials with a particular role, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all of the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```
    Name                Location   State    Type        
    my-object-storage   global     active   service_instance   
    tone_analyzer1      us-south   active   service_instance   
    tone_analyzer2      us-south   active   service_instance 
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with a particular service role. For more information about IAM service roles, see [Service access roles](/docs/account?topic=account-userroles#service_access_roles). The following example **`application bind`** command binds the `my-object-storage` service instance to the app called `my-application` by using the Writer service role. A new service credential with the Writer role is generated for this binding action.

    ```
    ibmcloud ce application bind --name my-application --service-instance my-object-storage --role Writer
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    <table>
    <caption><code>application bind</code> components</caption>
    <thead>
    <col width="25%">
    <col width="75%">
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--name</code></td>
    <td>The name of the application to bind. This value is required.</td>
    </tr>
    <tr>
    <td><code>--service-instance</code></td>
    <td>Specify the name of an existing service instance to bind to the application. This value is required.</td>
    </tr>
    <tr>
    <td><code>--role</code></td>
    <td>The name of a service role for the new service credential that is created for this service binding. Valid values include <code>Reader</code>, <code>Writer</code>, <code>Manager</code>, or a service-specific role. If the <code>--role</code> option is not specified, the default is <code>Manager</code> or the first role that is provided by the service if <code>Manager</code> is not supported. This option is ignored if <code>--service-credential</code> is specified.</td>
    </tr>
    </tbody>
    </table>

    **Example output**

    ```
    Binding service instance...
    Waiting for service binding to become ready...
    Status: Pending (Processing Resource)
    Status: Creating service binding
    Status: Ready
    Waiting for application revision to become ready...
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```
    [...]
    Service Bindings:
    Name              Service Instance   Service Type          Role / Credential  Environment Variable Prefix  Status  
    ce-binding-vwyxz  my-object-storage  cloud-object-storage  Writer             CLOUD_OBJECT_STORAGE         Ready 
    [...]
    ```
    {: screen}   

### Binding a service instance with existing credentials
{: #bind-existing-credentials}

If you already created a credential for your service instance and want to use it for your service binding, add the `--service-credentials` option.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all of the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```
    ibmcloud resource service-instances
    ```
    {: pre}

    **Example output**

    ```
    Name                Location   State    Type        
    my-object-storage   global     active   service_instance   
    tone_analyzer1      us-south   active   service_instance   
    tone_analyzer2      us-south   active   service_instance 
    ```
    {: screen}

2. Find the credentials of the service instance.

    ```
    ibmcloud resource service-keys --instance-name INSTANCENAME
    ```
    {: pre}
    
    **Example output**
    
    ```
    Name                State    Created At       
    my-cos-credential   active   Tue Mar  2 01:15:33 UTC 2021 
    ```
    {: screen}
    
    To see details of a service credential, run `ibmcloud resource service-key KEYNAME`. You can find all of the service keys in your resource group by running `ibmcloud resource service-keys`.
    {: tip}

3. Bind the service instance to the application or job with existing credentials. For example, the following **`job bind`** command binds the `my-object-storage` service instance with existing service credentials called `my-cos-credential` to an existing job that is called `my-job`.

    ```
    ibmcloud ce job bind --name my-job --service-instance my-object-storage --service-credential my-cos-credential
    ```
    {: pre}

    The following table summarizes the options that are used with the **`job bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

    <table>
    <caption><code>job bind</code> components</caption>
    <thead>
    <col width="25%">
    <col width="75%">
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--name</code></td>
    <td>The name of the job to bind. This value is required.</td>
    </tr>
    <tr>
    <td><code>--service-instance</code></td>
    <td>Specify the name of an existing service instance to bind to the job. This value is required.</td>
    </tr>
    <tr>
    <td><code>--service-credential</code></td>
    <td>The name of the existing service credential to bind.</td>
    </tr>
    </tbody>
    </table>

4. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```
    ibmcloud ce job get --name my-job
    ```
    {: pre}

    **Example output**

    ```
    [...]
    Service Bindings:
    Name                    Service Instance   Service Type          Role / Credential  Environment Variable Prefix  Status  
    my-cos-credential-abc12 my-object-storage  cloud-object-storage  my-cos-credential  CLOUD_OBJECT_STORAGE         Ready 
    [...]
    ```
    {: screen} 

## Unbinding service instances
{: #unbind}

Unbinding service instances from an application or job removes existing service bindings.

1. Find the service binding that you want to remove with the **`application get`** or **`job get`** command; for example, 

    ```
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    **Example output**

    ```
    [...]
    Service Bindings:
    Name                    Service Instance   Service Type          Role / Credential  Environment Variable Prefix  Status  
    my-cos-credential-abc12 my-object-storage  cloud-object-storage  my-cos-credential  CLOUD_OBJECT_STORAGE         Ready 
    ce-binding-vwxyz        appid              appid                 Manager            APPID                        Ready 
    [...]
    ```
    {: screen}

2. Remove the service binding by using the **`application unbind`** or the **`job unbind`** command.

    * To remove a single binding, specify the `--name` and `--binding` options. 

        ```
        ibmcloud ce application unbind --name APPLICATION_NAME --binding BINDING_NAME
        ```
        {: pre}

    * To unbind all service instances, use the `--all` option:

        ```
        ibmcloud ce job unbind --name JOB_NAME --all
        ```
        {: pre}


