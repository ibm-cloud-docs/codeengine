---

copyright:
  years: 2021
lastupdated: "2021-03-18"

keywords: registries and code engine, container registry and code engine, image registry and codeengine, apikeys and code engine, API key and code engine, access token and code engine

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Adding access to a private container registry 
{: #add-registry}

Before you can push or pull images in a private container registry, you must add access to a container registry.
{: shortdesc}

A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private. With {{site.data.keyword.codeengineshort}}, you can add access to your private container image registries.

To plan your options for images, see [planning image registries](/docs/codeengine?topic=codeengine-plan-image).

To add access to a Docker Hub account, you need your account name and password (or [access token](#add-registry-access-docker)). To add access to a {{site.data.keyword.registryshort}} instance, you need an IAM API key.

If you are accessing {{site.data.keyword.codeengineshort}} from the console, then {{site.data.keyword.codeengineshort}} can automatically push and pull images to and from a {{site.data.keyword.registryshort}} namespace in your account when you create or update apps, jobs, or builds from the console. {{site.data.keyword.codeengineshort}} can even create a namespace for you when you push an image. For more information, see the following topics,

- [Deploying an app that references an image in {{site.data.keyword.registryshort}} with the console](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-crimage-console).
- [Deploying your app from source code](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-source-code).
- [Creating a job from images in {{site.data.keyword.registryshort}} with the console](/docs/codeengine?topic=codeengine-job-deploy#create-job-crimage-console).
- [Creating a job from source code](/docs/codeengine?topic=codeengine-job-deploy#run-job-source-code).

## Create an IAM API key for a {{site.data.keyword.registryshort}} instance that is in your account
{: #access-registry-account}

If you are accessing a {{site.data.keyword.registryshort}} instance that is in the same account as your {{site.data.keyword.codeengineshort}} instance, you must first create an IAM API key and then provide the key to {{site.data.keyword.codeengineshort}}.

### Creating an API key from the console
{: #access-registry-account-console}

To create an {{site.data.keyword.cloud_notm}} IAM API key from the console,

1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview).
2. Select **API keys**.
3. Click **Create an {{site.data.keyword.cloud_notm}} API key**.
4. Enter a name and optional description for your API key and click **Create**.
5. Copy the API key or click download to save it. 

   You won’t be able to see this API key again, so be sure to record it in a safe place.
   {: important}
   
Now that you created your API key, continue to [Adding {{site.data.keyword.registryshort}} access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce).
   
### Creating an API key with the CLI
{: #access-registry-account-cli}

To create an {{site.data.keyword.cloud_notm}} IAM API key with the CLI, run the [`iam api-key-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

```
ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
```
{: pre}

If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
{: important}

Now that you created your API key, continue to [Adding {{site.data.keyword.registryshort}} access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce).

## Create an access token for Docker Hub
{: #add-registry-access-docker}

In order to create access to a Docker Hub account, you must provide your password or an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.
   
## Add registry access to {{site.data.keyword.codeengineshort}}
{: #add-registry-access-ce}

After you create your IAM API key, you can authorize {{site.data.keyword.codeengineshort}} to pull images from your container registry.
   
### Adding registry access from the console
{: #add-registry-access-ce-console}

To add {{site.data.keyword.registryshort}} or Docker Hub access with the console,

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Registry access**.
4. Click **Create**.
5. Enter a name for your registry access.
6. Enter a server name for your registry access. For {{site.data.keyword.registryshort}}, the server name is `<region>.icr.io`. For example, `us.icr.io`. For [Docker Hub](https://hub.docker.com/), the server name is `https://index.docker.io/v1/`.
7. Enter a name. For {{site.data.keyword.registryshort}}, it is `iamapikey`. For Docker Hub, it is your Docker ID.
8. Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#add-registry-access-docker).
9. Click **Add**.

You can add access to a container registry when you create an application or job, or when you build an image. Click **Select image** and then **Add registry**. Follow previous steps 5-9.
{: tip}

## Adding registry access with the CLI
{: #add-registry-access-ce-cli}

To add {{site.data.keyword.registryshort}} or Docker Hub access with the CLI, use the `registry create` command. This command requires a name of the image registry access secret, the URL of the registry server, and the username and password information to access the registry server and also allows other optional arguments. For a complete listing of options, see the [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command. 
{: shortdesc}

For example, the following `registry create` command creates registry access to a {{site.data.keyword.registryshort}} instance called `myregistry` that is on the `us.icr.io` registry server:

```
ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password API_KEY
```
{: pre}

**Example output**
```
Creating image registry access secret 'myregistry'...
OK
```
{: screen}

The following table summarizes the options that are used with the `registry create` command in this example. For more information about the command and its options, see the [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command.

<table>
  <caption><code>registry create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>registry create</code></td>
   <td>The command to create your registry access.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the image registry access secret. Use a name that is unique within the project. This value is required.
     <ul>
     <li>The name must begin and end with a lowercase alphanumeric character.</li>
	   <li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   <tr>
   <td><code>--server</code></td>
   <td>Enter the URL of the registry server. For {{site.data.keyword.registryshort}}, the server name is `<region>.icr.io`. For example, `us.icr.io`. For [Docker Hub](https://hub.docker.com/), the value is `https://index.docker.io/v1/`.</td>
   </tr>
   <tr>
   <td><code>--username</code></td>
   <td>Enter the username to access the registry server. For {{site.data.keyword.registryshort}}, it is `iamapikey`. For Docker Hub, it is your Docker ID.</td>
   </tr>
   <tr>
   <td><code>--password</code></td>
   <td>Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#add-registry-access-docker).</td>
   </tr>
   </tbody></table>

## Setting up access for a {{site.data.keyword.registryshort}} instance from a different account
{: #access-registry-diff-account}

You can assign {{site.data.keyword.cloud_notm}} IAM access policies to users or a service ID to restrict permissions to specific registry image namespaces or actions (such as push or pull). Then, create an API key and store these registry credentials in {{site.data.keyword.codeengineshort}}.
{: shortdesc}

For example, to access images in other {{site.data.keyword.cloud_notm}} accounts, create an API key that stores the {{site.data.keyword.registryfull_notm}} credentials of a user or service ID in that account. Then, in {{site.data.keyword.codeengineshort}}, save the API key credentials so that you can pull the images to create applications and jobs.

The following steps create an API key that stores the credentials of an {{site.data.keyword.cloud_notm}} IAM service ID. Instead of using a service ID, you might want to create an API key for a user ID that has an {{site.data.keyword.cloud_notm}} IAM service access policy to {{site.data.keyword.registryfull_notm}}. However, make sure that the user is a functional ID or plan for cases where the user leaves so that {{site.data.keyword.codeengineshort}} can still access the registry.
{: note}

**Before you begin**

- [Set up a namespace in {{site.data.keyword.registryfull_notm}} and push images to this namespace](/docs/Registry?topic=Registry-getting-started#gs_registry_namespace_add).
- Log in to your account.

### Authorizing access to {{site.data.keyword.registryshort}} from the console
{: #authorize-cr-console}

In order to pull or push images from or to {{site.data.keyword.registryfull_notm}}, you must create a service ID, create an access policy for the service ID, and then create an API key to store the credentials.

#### Step 1 Create the service ID and authorize it to the Container Registry service
{: #create-service-id}

1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview).
2. Select **Service IDs**.
3. If you have a Service ID that you want to use, select it. If not, select **Create**, enter a name and description,  and click **Create**.
4. From the Service ID page, select **Access policies** and then **Assign access**.
5. From the **Assign service ID additional access** section,
    1. Select **IAM services**.
    2. Select **Container Registry** for type of access.
    3. Select the type of access: **All services** or **Services based on attributes** groups**. If you specify **Services based on attributes**, you can add attributes based on resource group, region, resource type or resource name to further restrict access. 
    4. For Service access, select the type of access you want to grant. If you plan to use only images for your applications and jobs, select **Reader**. If you want to push the outcome of builds, then also select **Writer**.
    5. Click **Add** and then **Assign**.

#### Step 2 Authorize service ID to get details of an API key with the console
{: #authorize-service-id}

Now that our service ID is created and is granting access to {{site.data.keyword.registryshort}}, you must authorize the service ID to also get details of an API key by giving the service ID IAM Identity service access for Account management.

1. From the Service ID page, select **Access policies** and then **Assign access**.
2. From the **Assign service ID additional access** section,
    1. Select **Account management**.
    2. Select **IAM Identity service** for type of access to assign.
    3. Select the services that you want to assign access: **All services** or **Services based on attributes**. If you specify **Services based on attributes**, you can add attributes based on location, service instance, resource group, or resource ID to further restrict access. 
    4. For Platform access, select **Operator** access or higher.
    5. Click **Add** and then **Assign**.
    
#### Step 3 Creating an API key for a service ID
{: #create-api-key}

Create an API key for a service ID.

1. From the Service ID page, select **API keys** and then **Create**.
2. Enter a name and optional description for your API key and click **Create**.
3. Copy the API key or click download to save it. 

   You won’t be able to see this API key again, so be sure to record it in a safe place.
   {: important}

Now that you have your access policies in place for your service ID and your API key created, you can [add access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce) in order to pull images from your container registry.

### Authorizing access to {{site.data.keyword.registryshort}} with the CLI
{: #authorize-cr-cli}

In order to pull images from {{site.data.keyword.registryfull_notm}}, you must create a service ID, create access policies for the service ID, and then create an API key to store your credentials.
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} IAM service ID for your project that is used for the IAM policies and API key credentials in the image pull secret with the `iam service-id-create` command. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the project name. For a complete listing of the `iam service-id-create` command and its options, see the [`ibmcloud iam service-id-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_id_create) command.

  For example, the following command creates a service ID called `codeengine-myproject-id` with the description `Service ID for IBM Cloud Container Registry in Code Engine project myproject`:

  ```
  ibmcloud iam service-id-create codeengine-myproject-id --description "Service ID for IBM Cloud Container Registry in Code Engine project my proj"
  ```
  {: pre}
    
2. Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your service ID that grants access to {{site.data.keyword.registrylong_notm}} with the `iam service-policy-create` command. For a complete listing of the `iam service-policy-create` command and its options, see the [`ibmcloud iam service-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

  For example, the following command creates a policy for `codeengine-myproject-id` service ID with the role of `Reader`:
      
  ```
  ibmcloud iam service-policy-create codeengine-myproject-id --roles Reader --service-name container-registry
  ```
  {: pre}

  The following table summarizes the options that are used with the `iam service-policy-create` command in this example. For more information about the command and its options, see the [`ibmcloud iam service-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

  <table>
    <caption><code>`iam service-policy-create`</code> command components</caption>
    <thead>
      <col width="25%">
      <col width="75%">
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components </th>
    </thead>
      <tbody>
      <tr>
      <td><code>iam service-policy-create</code></td>
      <td>The command to create an access policy and assign it to a service ID.</td>
      </tr>
      <tr>
      <td><code><em>&lt;service_ID&gt;</em></code></td>
      <td>Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created in step 1.</td>
      </tr>
      <tr>
      <td><code>--service-name <em>container-registry</em></code></td>
      <td>Required. Enter `container-registry` to create an IAM policy for {{site.data.keyword.registrylong_notm}}.</td>
      </tr>
      <tr>
      <td><code>--roles <em>&lt;service_access_role&gt;</em></code></td>
      <td>Required. Enter the [service access role for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#service_access_roles) that you want to scope the service ID access to. Possible values are `Reader`, `Writer`, and `Manager`. If you are pulling images, then `Reader` is sufficient.</td>
      </tr>
      </tbody></table>
    
3. Create a custom service policy to allow access to `iam-identity` service so that {{site.data.keyword.codeengineshort}} can retrieve the API key for your service ID  with the `iam service-policy-create` command. 

  For example, create a policy for `codeengine-myproject-id` service ID with the role of `Operator`:
      
  ```
  ibmcloud iam service-policy-create codeengine-myproject-id --roles Operator --service-name iam-identity
  ```
  {: pre}

  The following table summarizes the options that are used with the `iam service-policy-create` command in this example. For more information about the command and its options, see the [`ibmcloud iam service-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

  <table>
    <caption><code>`iam service-policy-create`</code> command components</caption>
    <thead>
      <col width="25%">
      <col width="75%">
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components </th>
    </thead>
      <tbody>
      <tr>
      <td><code>iam service-policy-create</code></td>
      <td>The command to create an access policy and assign it to a service ID.</td>
      </tr>
      <tr>
      <td><code><em>&lt;service_ID&gt;</em></code></td>
      <td>Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created in step 1.</td>
      </tr>
      <tr>
      <td><code>--roles <em>&lt;platform_access_role&gt;</em></code></td>
      <td>Required. Enter the platform access role that you want to scope the service ID access to. Possible values are `Administrator`, `Editor`, `Operator`, and `Viewer`. Your service ID requires `Operator` or higher. </td>
      </tr>
      <tr>
      <td><code>--service-name <em>iam-identity</em></code></td>
      <td>Required. Enter `iam-identity` to create an IAM policy for IAM identify services.</td>
      </tr>
      </tbody></table>

4. Create an API key for the service ID with the `iam service-api-key-create` command. For a complete listing of the `iam service-api-key-create` command and its options, see the [`ibmcloud iam service-api-key-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create) command. Name the API key similar to your service ID, and include the service ID that you previously created, `codeengine-<project_name>-id`. Be sure to give the API key a description that helps you retrieve the key later.

  For example, the following command creates a key called `codeengine-myproject-key` for the `codeengine-myproject-id` service ID with a description of `API key for service ID codeengine-myproject-id for Code Engine myproject`:
      
  ```
  ibmcloud iam service-api-key-create codeengine-myproject-key codeengine-myproject-id --description "API key for service ID codeengine-myproject-id for Code Engine myproject"
  ```
  {: pre}

  **Example output**
      
  ```
  Please preserve the API key! It cannot be retrieved after it's created.

  Name          codeengine-myproject-key   
  Description   API key for service ID codeengine-myproject-id for Code Engine myproject   
  Bound To      crn:v1:bluemix:public:iam-identity::a/1bb222bb2b33333ddd3d3333ee4ee444::serviceid:ServiceId-ff55555f-5fff-6666-g6g6-777777h7h7hh   
  Created At    2019-02-01T19:06+0000   
  API Key       i-8i88ii8jjjj9jjj99kkkkkkkkk_k9-llllll11mmm1   
  Locked        false   
  UUID          ApiKey-222nn2n2-o3o3-3o3o-4p44-oo444o44o4o4   
  ```
  {: screen}
      
  You won’t be able to see this API key again, so be sure to record it in a safe place.
  {: important}
   
  Now that you have your access policies in place for your service ID and your API key created, you can [add access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce) in order to pull images from your container registry.
