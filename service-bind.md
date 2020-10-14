---

copyright:
  years: 2020
lastupdated: "2020-10-14"

keywords: about, code engine, bind, service bind

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Integrating {{site.data.keyword.cloud_notm}} services with service binding
{: #service-binding}

Find out how to integrate an {{site.data.keyword.cloud_notm}} service to resources in a {{site.data.keyword.codeengineshort}} project by using service binding.
{:shortdesc} 

Service bindings provide applications and jobs access to {{site.data.keyword.cloud_notm}} services.


## Beta limitations
{{site.data.keyword.codeengineshort}} service bindings are under development. Only existing services can be used. ({{site.data.keyword.codeengineshort}} does not currently create new service instances for you).


<br/>
**What is {{site.data.keyword.cloud_notm}} service binding?**

Binding a service to a {{site.data.keyword.codeengineshort}} application or job automatically adds credentials for a service to the environment variables of the container for your application or the job. To see the contents of a service credential, go to the dashboard for the service and locate the **Service credentials** page. Service credentials are shown as a JSON object, which, when bound, are added to the application or job environment.

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

To bind a service to your application or job, you must provision an instance of the service first. Then, use the `application bind` or `job bind` command to configure service credentials and secrets. Secrets are automatically encrypted to protect your data.

**What types of services can I bind?**

You can add any {{site.data.keyword.cloud_notm}} service that is enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) to your application or job. To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

**I already have an {{site.data.keyword.cloud_notm}} service with service credentials. Can I still use {{site.data.keyword.cloud_notm}} service binding?**

Yes, you can reuse the service credentials. To use your existing service credentials, specify the `--service-credential` flag in the `ibmcloud ce application bind` command and provide the name of your service credentials. {{site.data.keyword.cloud_notm}} service binding automatically creates a Kubernetes secret with your existing service credentials.

## How can I access a bound service from an app or job?
{: #access-bound-service}

Use environment variables to connect to your service instance with one of following methods: the [`VCAP_SERVICES`](#vcap-service) method or the [Prefix](#prefix-method) method.

### `VCAP_SERVICES` method
{: #vcap-service}

The `VCAP_SERVICES` environment variable contains information that you can use to interact with a service instance. This environment variable points to a JSON object that contains key value pairs. These key value pairs represent each type of service that is bound to your application. The `key` is the name of the service type, such as `cloud-object-storage`, and the `value` is an array of credentials for bound services of that type.

The following example illustrates a `VCAP_SERVICES` variable:

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

By default, the variable name is the name of the service, followed by `SECRET`, and then the name of credential variable. For example, an {{site.data.keyword.cos_full_notm}} service credential variable that is named `apikey` is available in an environment variable called `CLOUD_OBJECT_STORAGE_SECRET_APIKEY`. The following example shows the environment variables that are created for an {{site.data.keyword.cos_full_notm}} service instance binding.

```
CLOUD_OBJECT_STORAGE_SECRET_APIKEY=xxxxxx
CLOUD_OBJECT_STORAGE_SECRET_ENDPOINTS=https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints
CLOUD_OBJECT_STORAGE_SECRET_IAM_APIKEY_DESCRIPTION=Auto-generated for key b1c66882-d87a-424c-bbb0-6afaceed6234
CLOUD_OBJECT_STORAGE_SECRET_IAM_APIKEY_NAME=my-object-storage-codeengine-credential
CLOUD_OBJECT_STORAGE_SECRET_IAM_ROLE_CRN=crn:v1:bluemix:public:iam::::serviceRole:Manager
CLOUD_OBJECT_STORAGE_SECRET_IAM_SERVICEID_CRN=crn:v1:bluemix:public:iam-identity::a/1176a104ad4441e6b0aa92ed0b60b15c::serviceid:ServiceId-ddf06b7e-c6fd-4a4c-8b41-531fc64e640e
CLOUD_OBJECT_STORAGE_SECRET_RESOURCE_INSTANCE_ID=crn:v1:bluemix:public:cloud-object-storage:global:a/1176a104ad4441e6b0aa92ed0b60b15c:11179ac4-3736-4887-9c8e-d330a430c85a::
CLOUD_OBJECT_STORAGE_SERVICENAME=my-object-storage
```
{: screen}

By default, if more than one instance of the same type is bound to a single application, {{site.data.keyword.codeengineshort}} appends an index to the service name, such as `CLOUD_OBJECT_STORAGE_2_SECRET_APIKEY`.

Each service binding can be configured to use a custom environment variable prefix by using the `--prefix` flag.

## Bind an existing service to a {{site.data.keyword.codeengineshort}} application or job
{: #bind-existing}

**Before you begin**

* [Create and target a project](/docs/codeengine?topic=codeengine-manage-project). 
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


### Binding a service with new credentials
{: #bind-credentials}

To bind your new service to your {{site.data.keyword.codeengineshort}} application and generate new service credentials, use the `application bind` command. To bind your service to a {{site.data.keyword.codeengineshort}} job, you must bind the service to a job with the `job bind` command.

1. Identify the name of the service that you want to bind to your app or job. You can find all of the service instances that are in your account for your current resource group by running `ibmcloud resource service-instances`.

   **Example output**
   
   ```
   Name                Location   State    Type        
   my-object-storage   global     active   service_instance   
   tone_analyzer1      us-south   active   service_instance   
   tone_analyzer2      us-south   active   service_instance 
   ```
   {: pre}

2. Bind your service to your {{site.data.keyword.codeengineshort}} application or job and generate new service credentials. The following example binds the `my-object-storage` service instance with the app called `my-application`. New service credentials are generated for this binding action.

   ```
   ibmcloud ce application bind --name my-application --service-instance my-object-storage
   ```
   {: pre}
   
   <table>
  <caption><code>application bind</code> components</caption>
   <thead>
   <col width="25%">
   <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>application bind</code></td>
   <td>The command to bind the instance to your application.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the application.</td>
   </tr>
   <tr>
   <td><code>--service-instance</code></td>
   <td>Specify the name of an existing service instance.</td>
   </tr>
   </tbody>
   </table>

3. Verify that the credentials were generated by using the `application get` or the `job get` command.  In the following example, verify that the credentials that were created in the previous example were created. 

   ```
   ibmcloud ce application get --name my-application
   ```
   {: pre}
   
   **Example output**
   
   ```
   [...]
   Service Bindings:
   Service Instance   Service Type          Credential                               Environment Variable Prefix  Status
   my-object-storage  cloud-object-storage  my-object-storage-codeengine-credential  CLOUD_OBJECT_STORAGE         Ready
   ```
   {: screen}   

### Binding a service instance that has existing credentials
{: #bind-existing-credentials}

If you already created a credential for your service instance and want to use it for your service binding, add the `--service-credentials` option.

1. Identify the name of the service that you want to bind to your app or job. You can find all of the service instances that are in your account for your current resource group by running `ibmcloud resource service-instances`.

   **Example output**
   
   ```
   Name                Location   State    Type        
   my-object-storage   global     active   service_instance   
   tone_analyzer1      us-south   active   service_instance   
   tone_analyzer2      us-south   active   service_instance 
   ```
   {: screen}
   
2. Find the credentials of the service.
   
   ```
   ibmcloud resource service-keys --instance-name INSTANCENAME
   ```
   {: pre}
   
   **Example output**	
   	
   ```	
   Name                State    Created At   	
   object-credential   active   Wed May 27 15:55:53 UTC 2020 	
   ```	
   {: screen}
   
   To see details of a service credential, run `ibmcloud resource service-key KEYNAME`. You can find all of the service keys in your resource group by running `ibmcloud resource service-keys`.
   {: tip}
   
3. Bind the service to the application or job with existing credentials. The following example binds the `my-object-storage` service instance with existing service credentials called `object-credential` to an existing job that is called `my-job`.

   ```
   ibmcloud ce job bind --name my-job --service-instance my-object-storage --service-credential object-credential
   ```
   {: pre}
   
   <table>
  <caption><code>job bind</code> components</caption>
   <thead>
   <col width="25%">
   <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>job bind</code></td>
   <td>The command to bind the instance to your job.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job.</td>
   </tr>
   <tr>
   <td><code>--service-instance</code></td>
   <td>Specify the name of an existing service instance.</td>
   </tr>
   <tr>
   <td><code>--service-credential</code></td>
   <td>The name of the service KEY credentials to bind.</td>
   </tr>
   </tbody>
   </table>
   
4. Verify that the credentials were generated by using the `application get` or the`job get` command.  In the following example, verify that the credentials that were created in the previous example were created. 

   ```
   ibmcloud ce job get --name my-job
   ```
   {: pre}
   
   **Example output**
   
   ```
   [...]
   Service Bindings:
   Service Instance         Service Type           Credential               Environment Variable Prefix   Status
   my-object-storage        cloud-object-storage   object-credential        CLOUD_OBJECT_STORAGE          Ready
   ```
   {: screen} 
   
## Unbinding services 
{: #unbind}

Unbinding a service from an application or job removes existing service bindings.

1. Find the service binding that you want to remove with the `application get` or `job get` command.

   ```
   ibmcloud ce application get --name my-application
   ```
   {: pre}
   
2. Unbind a service by using the `application unbind` or the `job unbind` command.

   * To unbind a single service, specify the `--name` and `--service-instance` flags:
   
     ```
     ibmcloud ce application unbind --name APPLICATION_NAME --service-instance SERVICE_NAME
     ```
     {: pre}
     
   * To unbind all services, use the `--all` flag:
   
     ```
     ibmcloud ce job unbind --name JOB_NAME --all
     ```
     {: pre}
