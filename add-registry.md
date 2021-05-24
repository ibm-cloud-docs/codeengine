---

copyright:
  years: 2021
lastupdated: "2021-05-24"

keywords: registries, container registry, image registry, apikey, API key, access token

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
{:terraform: .ph data-hd-interface='terraform'}
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


# Accessing container registry
{: #add-registry}

Images that are used by {{site.data.keyword.codeenginefull}} are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).
{: shortdesc}

A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private.

## Types of image registries
{: #types-registries}

Images are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).

Public registries, such as public Docker Hub, can be used to get started with Docker and {{site.data.keyword.codeengineshort}} to create your first application or job. But when it comes to enterprise workloads, use a private registry, such as the one provided in {{site.data.keyword.registrylong_notm}} to protect your images from being used and changed by unauthorized users. Access to private registries must be set up to ensure that the credentials to access the private registry are available.

| Registry | Description | Benefit |
|--------|-----------|-------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started)| With this option, you can set up your own secured image repository in {{site.data.keyword.registrylong_notm}} where you can safely store and share images between users.|<ul><li>Manage access to images in your account.</li><li>Use {{site.data.keyword.IBM_notm}} provided images and sample apps, such as {{site.data.keyword.IBM_notm}} Liberty, as a parent image and add your own app code to it.</li>/ul> |
|Any other private registry | Connect any existing private registry to {{site.data.keyword.codeengineshort}} by adding access. Adding access  securely saves your registry URL and credentials in a Kubernetes secret. | <ul><li>Use existing private registries independent of their source (Docker Hub, organization-owned registries, or other private Cloud registries).</li></ul> |
| [Public Docker Hub](https://hub.docker.com/){: external}{: #dockerhub}| Use this option to pull existing public images from Docker Hub directly in your {{site.data.keyword.codeengineshort}} applications or jobs. <p>**Important**</p> <ul><li>This option might not meet your organization's security requirements such as access management, vulnerability scanning, or app privacy.</li><li>When you pull an image from Docker Hub to use with apps or jobs in {{site.data.keyword.codeengineshort}}, be aware of [Docker rate limits](https://docs.docker.com/docker-hub/download-rate-limit){: external} for free plan (anonymous) users. You might experience pull limits if you receive a `429` error indicating you have reached your pull rate limit. To [increase rate limits ](https://www.docker.com/increase-rate-limits){: external}, you can upgrade your account to a Docker `Pro` or `Team` subscription.</li></ul> | <ul><li>These images can be referred to directly when you create an app or job, no additional setup is required.</li><li>Includes various open source applications.</li></ul> |
{: caption="Public and private image registry options" caption-side="top"}

After you [set up access](/docs/codeengine?topic=codeengine-add-registry) to an image registry, you can deploy the images as applications or jobs in {{site.data.keyword.codeengineshort}}.

## Setting up authorities for image registries
{: #authorities-registry}

if your registry is public, you do not have to set up authorities in order to pull images. Note that pulling images from a public registry while you are getting started with {{site.data.keyword.codeengineshort}} is acceptable, use a private registry when it comes to your enterprise workloads.

**What authorities do I need?**

When you deploy apps or run jobs from the console, {{site.data.keyword.codeengineshort}} can automatically access images that are in your own account. If you want to access images from a shared account, other {{site.data.keyword.cloud_notm}} accounts, or a private Docker acount, you must be assigned the proper access authorities.

| Action | IAM service access | Description |
|--------|-----------|---------------------|
| Pull images | `Read` access | When you deploy an image as an application or job, you must pull the image from a registry. To pull images, you need `read` access. Note that if the repository is public, you already have `read` access to the images. |
| Push images | `Read` and `write` access | When you build source code, you must push the image to a registry. To push images, you need `write` access to {{site.data.keyword.registryfull_notm}}. You cannot push images to a registry other than {{site.data.keyword.registryfull_notm}}. |
| Create a namespace | `Manager` access | To create a namespace in {{site.data.keyword.registrylong_notm}}, you must have `manager` access. |



**Can I access images in a different registry?**

Yes! [Here is how](#images-different-account).

## Accessing images from a public account
{: #images-public-account}

If your image is stored in a public repository, such as a public Docker Hub, then you can simply reference the image directly when you deploy your application or run your job. Note that while storing images in a public registry is fine for getting started with applications and jobs, store your enterprise images in a private registry.

## Accessing images in your own account from console
{: #images-your-account}

If you are accessing {{site.data.keyword.codeengineshort}} from an account that you own or administer, then {{site.data.keyword.codeengineshort}} can automatically push and pull images to and from an {{site.data.keyword.registryfull_notm}} namespace in your account when you create or update apps, jobs, or builds from the console. {{site.data.keyword.codeengineshort}} can even create a namespace for you when you push an image. For more information, see the following topics.

- [Deploying an app that references an image in {{site.data.keyword.registryfull_notm}} with the console](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-crimage-console).
- [Deploying your app from source code](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-source-code).
- [Creating a job from images in {{site.data.keyword.registryfull_notm}} with the console](/docs/codeengine?topic=codeengine-job-deploy#create-job-crimage-console).
- [Creating a job from source code](/docs/codeengine?topic=codeengine-job-deploy#run-job-source-code).

## Accessing images from your account with an API key
{: #images-your-account-api-key}

If you are accessing {{site.data.keyword.codeengineshort}} with the CLI, you must first create an IAM API key and then [save the IAM API key as registry access](#add-registry-access-ce) in {{site.data.keyword.codeengineshort}}.

The following steps create an API key that stores the credentials of a user ID. Instead of using a user ID, you might want to create an API key for a service ID that has an {{site.data.keyword.cloud_notm}} IAM service access policy to {{site.data.keyword.registryfull_notm}}. If you choose to authenticate a user ID, make sure that the user is a functional ID or plan for cases where the user leaves so that {{site.data.keyword.codeengineshort}} can still access the registry.
{: note}

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
   
Now that you created your API key, [save it as registry access](#add-registry-access-ce).
   
### Creating an API key with the CLI
{: #access-registry-account-cli}

To create an {{site.data.keyword.cloud_notm}} IAM API key with the CLI, run the [**`iam api-key-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

```sh
ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
```
{: pre}

If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
{: important}

Now that you created your API key, [save it as registry access](#add-registry-access-ce).

## Accessing images in a shared account
{: #images-shared-account}

In order to access images from {{site.data.keyword.registryfull_notm}} in a shared account, you must be assigned the [proper authority](#authorities-registry).

If you are planning to deploy apps and run jobs from the shared account, {{site.data.keyword.codeengineshort}} can pull or push images for you when you deploy your application or create your job.

If you want to pull images from the shared account to your own account, then you must be [authorized to access {{site.data.keyword.registrylong_notm}}](#authorities-registry).

## Accessing images in a different account
{: #images-different-account}

You can assign {{site.data.keyword.cloud_notm}} IAM access policies to users or a service ID to restrict permissions to specific registry image namespaces or actions (such as push or pull). Then, create an API key and store these registry credentials in {{site.data.keyword.codeengineshort}}.
{: shortdesc}

For example, to access images in other {{site.data.keyword.cloud_notm}} accounts, [create an API key](#images-your-account-api-key) that stores the {{site.data.keyword.registryfull_notm}} credentials of a user or service ID in that account. Then, in {{site.data.keyword.codeengineshort}}, use that key to [create access](#add-registry-access-ce) in your account.

## Accessing images in a private Docker Hub account
{: #access-private-docker-hub}

To access images in a private Docker Hub account, create registry access by providing your password or an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.  

After you decide whether to use your password directly or to create an access token, [create your registry access](#add-registry-access-ce).

## Add registry access to {{site.data.keyword.codeengineshort}}
{: #add-registry-access-ce}

To set up access to an {{site.data.keyword.registryfull_notm}} in a different {{site.data.keyword.cloud_notm}} account, to pull images from a private Docker Hub account, or to pull or push images by using the {{site.data.keyword.codeengineshort}} CLI, you can use the [IBM API key](#images-your-account-api-key) or [Docker Hub password or access token](#access-private-docker-hub) to create registry access through {{site.data.keyword.codeengineshort}} to store your authentication key or token for you.
   
### Adding registry access from the console
{: #add-registry-access-ce-console}

To add {{site.data.keyword.registryfull_notm}} or Docker Hub access with the console,

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Registry access**.
4. Click **Create**.
5. Select **Docker hub** or **Custom**.
6. Enter a name for your registry access.
7. Enter a server name for your registry access. For {{site.data.keyword.registryshort}}, the server name is `<region>.icr.io`. For example, `us.icr.io`. For [Docker Hub](https://hub.docker.com/), the server name is `https://index.docker.io/v1/`.
8. Enter a username. For {{site.data.keyword.registryfull_notm}}, it is `iamapikey`. For Docker Hub, it is your Docker ID.
9. Enter the password. For {{site.data.keyword.registryfull_notm}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#add-registry-access-docker).
10. Click **Add**.

You can add access to a container registry when you create an application or job, or when you build an image. Click **Select image** and then **Add registry**. Follow previous steps 5-9.
{: tip}

### Adding registry access with the CLI
{: #add-registry-access-ce-cli}

To add {{site.data.keyword.registryfull_notm}} or Docker Hub access with the CLI, use the **`registry create`** command. This command requires a name of the image registry access secret, the URL of the registry server, and the username and password information to access the registry server and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command. 
{: shortdesc}

For example, the following **`registry create`** command creates registry access to an {{site.data.keyword.registryfull_notm}} instance called `myregistry` that is on the `us.icr.io` registry server:

```sh
ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password API_KEY
```
{: pre}

**Example output**
```
Creating image registry access secret 'myregistry'...
OK
```
{: screen}

The following table summarizes the options that are used with the **`registry create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command.

<table>
  <caption><code>**`registry create`**</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
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



## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}: Container registry implementation
{: #private-registry-imp}

To pull images from a registry, {{site.data.keyword.codeengineshort}} uses a special type of Kubernetes secret that is called an `imagePullSecret`. This image pull secret stores the credentials to access a container registry. When you add access to a container registry with {{site.data.keyword.codeengineshort}}, you are creating an image pull secret. For more information about image pull secrets, see [Kubernetes documentation](https://kubernetes.io/docs/home/){: external}.
