---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-22"

keywords: registries, container registry, image registry, apikey, API key, access token, images, registry access, registry secret, service id,registry secret, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Accessing container registries 
{: #add-registry}

Images that are used by {{site.data.keyword.codeenginefull}} are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).
{: shortdesc}

A container registry, or registry, is a service that stores container images. For example, {{site.data.keyword.registryfull_notm}} and Docker Hub are container registries. A container registry can be public or private. A container registry that is public does not require credentials to access. In contrast, accessing a private registry does require credentials.

{{site.data.keyword.codeengineshort}} requires access to container registries to complete the following actions:
- To retrieve (or "pull") a container image to run an app or job
- To store a newly created container image as an output of an image build
- To store and retrieve local files when a build is run from local source

{{site.data.keyword.codeengineshort}} handles many of the underlying details of the interactions between the system and your registry.  

To pull images from a registry, {{site.data.keyword.codeengineshort}} uses a special type of Kubernetes secret that is called an `imagePullSecret`. This image pull secret stores the credentials to access a container registry. When you add access to a container registry with {{site.data.keyword.codeengineshort}} to pull images, you are creating an image pull secret. For more information about image pull secrets, see [Kubernetes documentation](https://kubernetes.io/docs/home/){: external}.
{: note}

## Types of image registries
{: #types-registries}

Images are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).

Public registries, such as public Docker Hub, can be used to get started with Docker and {{site.data.keyword.codeengineshort}} to create your first application or job. But when it comes to enterprise workloads, use a private registry, such as the one provided in {{site.data.keyword.registrylong_notm}} to protect your images from being used by unauthorized users. For private registries, use registry secrets to ensure that the credentials are available to gain access to the private registry. 

| Registry | Description |
|--------|---------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started) | With this type of registry, you can set up your own secured image repository in {{site.data.keyword.registrylong_notm}} where you can safely store and share images between users. \n With {{site.data.keyword.registrylong_notm}}, you can \n - Manage access to images in your account. \n - Use {{site.data.keyword.IBM_notm}} provided images and sample apps, such as {{site.data.keyword.IBM_notm}} Liberty, as a base image and add your own app code to it. |
|Any other private registry | Connect any existing private registry to {{site.data.keyword.codeengineshort}} by adding access. Adding access securely saves your registry URL and credentials in a Kubernetes secret. \n With private registries, you can: \n - Use existing private registries independent of their source (Docker Hub, organization-owned registries, or other private Cloud registries). |
| [Public Docker Hub](https://hub.docker.com/){: external}{: #dockerhub} | Use this type of registry to pull existing public images from Docker Hub directly in your {{site.data.keyword.codeengineshort}} applications or jobs. \n  \n **Important** \n - This registry type might not meet your organization's security requirements such as access management, vulnerability scanning, or app privacy. \n - When you pull an image from Docker Hub to use with apps or jobs in {{site.data.keyword.codeengineshort}}, be aware of [Docker rate limits](https://docs.docker.com/docker-hub/download-rate-limit){: external} for free plan (anonymous) users. You might experience pull limits if you receive a `429` error which indicates that you have reached your pull rate limit. To [increase rate limits](https://www.docker.com/increase-rate-limits){: external}, you can upgrade your account to a Docker `Pro` or `Team` subscription. \n  \n With public Docker Hub, you can: \n - These images can be referred to directly when you create an app or job, no additional setup is required. \n - Includes various open source applications. |
{: caption="Table 1. Public and private image registry types" caption-side="bottom"}

## Types of registry secrets
{: #types-registryaccesssecrets}

 To access images in a registry, {{site.data.keyword.codeengineshort}} uses one of the following types of registry secrets.

* {{site.data.keyword.codeengineshort}} managed secret - If your registry uses an {{site.data.keyword.registrylong_notm}} namespace that is in your account, then you can let {{site.data.keyword.codeengineshort}} create and manage the registry secret for you. In the console, this automatically created registry secret is called a `{{site.data.keyword.codeengineshort}} managed secret`. In the CLI, the name of an automatically created registry secret is of the format, `ce-auto-icr-private-<region>`. 
* User managed secret - This is a secret that you create and manage. You can [access images from your account with an API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key) or use an access token for the container registry of your choice; for example, Docker Hub. For this case, the registry secret that is listed in the console is the name of your registry secret. 

If your registry is public and does not require credentials; for example, {{site.data.keyword.codeengineshort}} sample images in `icr.io/codeengine` or Docker Hub public, then you do not need a registry secret. For this case, the registry secret that is listed in the console is `None`. 


## Setting up authorities for image registries
{: #authorities-registry}

If your registry is public, you do not have to set up authorities to pull images. Note that pulling images from a public registry while you are getting started with {{site.data.keyword.codeengineshort}} is acceptable. Use a private registry when it comes to your enterprise workloads.

### What authorities do I need?
{: #authorities-registry-what-auth}

To determine the authorities that you need, consider the following cases:

* When you deploy apps or run jobs, {{site.data.keyword.codeengineshort}} can automatically access images that are in your own account.

* If you want to access images from a shared account, other {{site.data.keyword.cloud_notm}} accounts, or a private Docker account, you must be assigned the proper access authorities.

* When you deploy apps or run jobs and your registry uses an {{site.data.keyword.registrylong_notm}} namespace that is in your account, then you can let {{site.data.keyword.codeengineshort}} automatically create and manage the registry secret for you, as long as your account has the required permissions as described in the following table.
    - In the console, this registry secret is called a `{{site.data.keyword.codeengineshort}} managed secret`. This option is available when you use the **Configure image** or **Specify build details** workflows for building an image with {{site.data.keyword.codeengineshort}}.
    - In the CLI, this registry secret is of the format, `ce-auto-icr-private-<region>`. This registry secret is automatically created when you specify the `--build-source` option but you do not provide the `--registry-secret` option with the **`app create`**, **`app update`**, **`job create`**, or **`job update`** commands. 


| Action | IAM service access | Description |
|--------|-----------|---------------------|
| Pull images  | `Reader` service access | When you deploy an image as an application or job, you must pull the image from a registry. To pull images, you need read access. If the registry is public, you already have read access to the images. If the registry is private, then a registry secret is required.  |
| Push images  | `Reader` and `Writer` service access | When you build source code, you must push the image to a registry. To push images to your registry, you must have read and write access, and you must have a registry secret. |
| Create a namespace | `Reader`, `Writer`, and `Manager` service access | This action is only supported for {{site.data.keyword.registrylong_notm}}. |
| {{site.data.keyword.codeengineshort}} automatically created registry secret  | `Administrator` platform access \n `Reader`, `Writer`, and `Manager` service access| This action is only supported for {{site.data.keyword.registrylong_notm}}. |
{: caption="Table 2. Access authorities for image registry" caption-side="bottom"}

### Can I use a service ID?
{: #authorities-registry-service-id}

Yes, you can create a service ID and assign authorities to it. Note that service IDs are also automatically created by the {{site.data.keyword.codeengineshort}} UI when you automatically create access to your {{site.data.keyword.registryfull_notm}}. DO NOT delete this service ID as you will lose access to the images in the registry.

### Can I access images in a different registry?
{: #authorities-registry-access-images}

Yes! [Here is how](#images-different-account).

### Can I restrict pull access to a certain regional registry or even a single namespace?
{: #authorities-registry-pull-access}

Yes, you can edit the existing [IAM policy of the service ID](#authorize-cr-service-id) that restricts the **Reader** service access role to that regional registry or a registry resource such as a namespace. Before you can customize registry IAM policies, you must [enable {{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-user).


## Accessing images from a public account
{: #images-public-account}

If your image is stored in a public repository, such as a public Docker Hub, then you can simply reference the image directly when you deploy your application or run your job. Note that while storing images in a public registry is fine for getting started with applications and jobs, store your enterprise images in a private registry.

## Accessing images in your own account from console
{: #images-your-account}

If you are accessing {{site.data.keyword.codeengineshort}} from an account that you own or administer, then {{site.data.keyword.codeengineshort}} can automatically push and pull images to and from an {{site.data.keyword.registryfull_notm}} namespace in your account when you create or update apps, jobs, or builds from the console. {{site.data.keyword.codeengineshort}} can even create a namespace for you when you push an image. For more information, see the following topics.

- [Deploying an app that references an image in {{site.data.keyword.registryfull_notm}} with the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console).
- [Deploying your app from source code](/docs/codeengine?topic=codeengine-app-source-code).
- [Creating a job from images in {{site.data.keyword.registryfull_notm}} with the console](/docs/codeengine?topic=codeengine-create-job-crimage#create-job-crimage-console).
- [Creating a job from source code](/docs/codeengine?topic=codeengine-run-job-source-code).

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

To create an {{site.data.keyword.cloud_notm}} IAM API key with the CLI, run the [**`iam api-key-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI API key" and save it to a file called `key_file`, run the following command:

```txt
ibmcloud iam api-key-create cliapikey -d "My CLI API key" --file key_file
```
{: pre}

If you choose to not save your key to a file, you must record the API key that is displayed when you create it. You cannot retrieve it later.
{: important}

Now that you created your API key, [save it as registry access](#add-registry-access-ce).

## Accessing images in a shared account
{: #images-shared-account}

To access images from {{site.data.keyword.registryfull_notm}} in a shared account, you must be assigned the [proper authority](#authorities-registry).

If you are planning to deploy apps and run jobs from the shared account, {{site.data.keyword.codeengineshort}} can pull or push images for you when you deploy your application or create your job.

If you want to pull images from the shared account to your own account, then you must be [authorized to access {{site.data.keyword.registrylong_notm}}](#authorities-registry).

## Accessing images in a different account
{: #images-different-account}

You can assign {{site.data.keyword.cloud_notm}} IAM access policies to users or a service ID to restrict permissions to specific registry image namespaces or actions (such as push or pull). Then, create an API key and store these registry credentials in {{site.data.keyword.codeengineshort}}.
{: shortdesc}

For example, to access images in other {{site.data.keyword.cloud_notm}} accounts, [create an API key](#images-your-account-api-key) that stores the {{site.data.keyword.registryfull_notm}} credentials of a user or service ID in that account. Then, in {{site.data.keyword.codeengineshort}}, use that key to [create access](#add-registry-access-ce) in your account.

## Accessing images in a private Docker Hub account
{: #access-private-docker-hub}

To access images in a private Docker Hub account, create registry access by providing your password or an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/security/for-developers/access-tokens/){: external}.  

After you decide whether to use your password directly or to create an access token, [create your registry access](#add-registry-access-ce).

## Add registry access to {{site.data.keyword.codeengineshort}}
{: #add-registry-access-ce}

To set up access to an {{site.data.keyword.registryfull_notm}} in a different {{site.data.keyword.cloud_notm}} account, to pull images from a private Docker Hub account, or to pull or push images by using the {{site.data.keyword.codeengineshort}} CLI, you can use the [IBM API key](#images-your-account-api-key) or [Docker Hub password or access token](#access-private-docker-hub) to create registry access through {{site.data.keyword.codeengineshort}} to store your authentication key or token for you.

### Adding registry access from the console
{: #add-registry-access-ce-console}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Components page, click **Secrets and configmaps**.
3. From the Secrets and configmaps page, click **Create** to create your secret.
4. From the Create secret or configmap page, complete the following steps:
    1. Select **Registry secret**, and click **Next**.
    2. Provide a name; for example, `mysecret-registry`.
    3. Specify the target registry for this secret, such as {{site.data.keyword.registrylong_notm}} or Docker Hub.
    4. Specify the location of the registry. 
    5. Specify a username. If this secret is for {{site.data.keyword.registrylong_notm}}, the username is `iamapikey`. If this secret is for Docker Hub, it is your Docker ID.
    6. Enter the credentials for the username. For {{site.data.keyword.registryfull_notm}}, use your IAM API key. For Docker Hub, you can use your Docker Hub password or an [access token](#access-private-docker-hub). For other target registries, specify the password or API key for the username.
    7. Click **Create** to create the secret. 

Now that your secret is created from the console, go to the Secrets and configmaps page to view a list of defined secrets and configmaps. You can apply filters to customize the list to meet your needs. 

You can add access to a container registry when you create an application or job, or when you build an image. Click **Configure image** and specify the container image to run, including the registry where the image is stored and the [registry access](/docs/codeengine?topic=codeengine-add-registry#types-registryaccesssecrets) to use to retrieve the image. 
{: tip}



### Adding registry access with the CLI
{: #add-registry-access-ce-cli}


Beginning with CLI version 1.42.0, defining and working with secrets in the CLI is unified under the **`secret`** command group. See [**`ibmcloud ce secret`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) commands. Use the `--format` option to specify the category of secret, such as `basic_auth`, `generic`, `ssh`, `tls`, or `registry`. 
While you can continue to use the **`registry`** command group, take advantage of the unified **`secret`** command group.
To create a secret to access a container registry, use the [**`ibmcloud ce secret create --format registry`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. To learn more about working with secrets in {{site.data.keyword.codeengineshort}}, see [Working with secrets](/docs/codeengine?topic=codeengine-secret).
{: important}


To add {{site.data.keyword.registryfull_notm}} or Docker Hub access with the CLI, use the **`secret create --format registry`** command. This command requires a name of the registry secret, the URL of the registry server, and the username and password information to access the registry server, and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce secret create`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command.
{: shortdesc}

For example, the following command creates registry access to an {{site.data.keyword.registryfull_notm}} instance called `myregistry` that is on the `us.icr.io` registry server:

```txt
ibmcloud ce secret create --format registry --name myregistry --server us.icr.io --username iamapikey --password API_KEY
```
{: pre}

Example output

```txt
Creating registry secret 'myregistry'...
OK
```
{: screen}

The following table summarizes the options that are used with the **`secret create --format registry`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce secret create`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the registry secret. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-). |
| `--server` | Enter the URL of the registry server. For {{site.data.keyword.registryshort}}, the server name is `<region>.icr.io`. For example, `us.icr.io`. For [Docker Hub](https://hub.docker.com/), the value is `https://index.docker.io/v1/`.|
| `--username` | Enter the username to access the registry server. For {{site.data.keyword.registryshort}}, it is `iamapikey`. For Docker Hub, it is your Docker ID. |
| `--password` | Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#access-private-docker-hub). |
{: caption="Table 3. Command description" caption-side="bottom"}

## Authorizing access to {{site.data.keyword.registryshort}} with service ID
{: #authorize-cr-service-id}

Before you can add access to a service ID in a different account, you must first authorize access to the service ID.

When you create a service ID, you can restrict access to a regional {{site.data.keyword.registryfull_notm}} or even a specific namespace within that {{site.data.keyword.registryfull_notm}} account.

### Authorizing access to {{site.data.keyword.registryshort}} with service ID from the console
{: #authorize-console-service-id}

To pull or push images from or to {{site.data.keyword.registryfull_notm}}, you must create a service ID, create an access policy for the service ID, and then create an API key to store the credentials.

#### Step 1 Create or identify a service ID and authorize it to the {{site.data.keyword.registryfull_notm}} service
{: #create-service-id}

1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
2. Select **Service IDs**.
3. If you have a Service ID that you want to use, select it. If not, select **Create**, enter a name and description, and click **Create**.
4. From the Service ID page, from the **Access policies** section, select **Assign access**.
5. From the **Assign service ID additional access** section,
    1. Select **Container Registry** for type of access. Click **Next**.
    2. Select the type of access: **All resources** or **Specific resources**. If you specify **Specific resources**, you can add attributes based on resource group, geography, region, resource type, resource ID, or resource name to further restrict access. If you select a certain resource group, make sure to select **Viewer** access for **Resource group** access. Click **Next**.
    3. In the **Roles and Actions** section, select the type of access you want to grant. If you plan to use only images for your applications and jobs, select **Reader**. If you want to push the source code and images to Container Registry, then also select **Writer**. Click **Review**.
    4. Click **Add** and then **Assign**.

#### Step 2 Enabling Container Registry discovery
{: #registry-discovery}

To allow the Code Engine console to automatically discover Container registry, you must authenticate the service ID to the IAM Identity Service. 


1. From the Service ID page, from the **Access policies** section, select **Assign access**.
2. From the **Assign service ID additional access** section,
    1. Select **IAM Identity Service** for type of access. Click **Next**.
    2. Select **Specific resources** for resource scope. Select **Resource type** as attribute type, keep **string equals** as operator and enter `serviceid` as value. Click **Add a condition**.
    3. Select **Resource ID** as attribute type, keep **string equals** as operator and put the identifier of your service ID. You can find your service ID on the **Details** page for the service ID or in the browser URL when configuring it. Click **Next**.
    4. In the **Roles and Actions** section, select Platform **Operator** access. Click **Review**
    5. Click **Add** and then **Assign**.

#### Step 3 Creating an API key for a service ID
{: #create-api-key}

Create an API key for a service ID.

1. From the Service ID page, select **API keys** and then **Create**.
2. Enter a name and optional description for your API key and click **Create**.
3. Copy the API key or click download to save it. 

    You won’t be able to see this API key again, so be sure to record it in a safe place.
    {: important}

Now that you have your access policies in place for your service ID and your API key created, you can [add access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce) to pull images from your container registry.

### Authorizing access to {{site.data.keyword.registryshort}} with the CLI
{: #authorize-cr-cli}

To pull images from {{site.data.keyword.registryfull_notm}} in a different account, you must create a service ID, create access policies for the service ID, and then create an API key to store your credentials.
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} IAM service ID for your project that is used for the IAM policies and API key credentials in the image pull secret with the **`iam service-id-create`** command. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the project name. For a complete listing of the **`iam service-id-create`** command and its options, see the [**`ibmcloud iam service-id-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_service_id_create) command.

    For example, the following command creates a service ID called `codeengine-myproject-id` with the description `Service ID for IBM Cloud Container Registry in {{site.data.keyword.codeengineshort}} project myproject`:

    ```txt
    ibmcloud iam service-id-create codeengine-myproject-id --description "Service ID for IBM Cloud Container Registry in Code Engine project my proj"
    ```
    {: pre}

2. Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your service ID that grants access to {{site.data.keyword.registrylong_notm}} with the **`iam service-policy-create`** command. For a complete listing of the **`iam service-policy-create`** command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    For example, the following command creates a policy for `codeengine-myproject-id` service ID with the role of `Reader`:

    ```txt
    ibmcloud iam service-policy-create codeengine-myproject-id --roles Reader --service-name container-registry
    ```
    {: pre}

    The following table summarizes the options that are used with the **`iam service-policy-create`** command in this example. For more information about the command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `<service_ID>` | Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created. |
    | `--roles <service_access_role>` | Required. Enter the [service access role for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#service_access_roles) that you want to scope the service ID access to. Possible values are `Reader`, `Writer`, and `Manager`. If you are pulling images, then `Reader` access is sufficient. For more information, see [Setting up authorities for image registries](#authorities-registry).|
    | `--service-name <container-registry>` | Required. Enter `container-registry` to create an IAM policy for {{site.data.keyword.registrylong_notm}}. 
    {: caption="Table 4. iam service-policy-create command components" caption-side="bottom"}


3. Create a custom service policy to allow access to `iam-identity` service so that {{site.data.keyword.codeengineshort}} can retrieve the API key for your service ID with the **`iam service-policy-create`** command. 

    For example, create a policy for `codeengine-myproject-id` service ID with the role of `Operator`:

    ```txt
    ibmcloud iam service-policy-create codeengine-myproject-id --roles Operator --service-name iam-identity
    ```
    {: pre}

    The following table summarizes the options that are used with the **`iam service-policy-create`** command in this example. For more information about the command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `<service_ID>` | Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created. |
    | `--roles <platform_access_role>` | Required. Enter the platform access role that you want to scope the service ID access to. Possible values are `Administrator`, `Editor`, `Operator`, and `Viewer`. Your service ID requires `Operator` or higher. |
    | `--service-name <iam-identity>` | Required. Enter `iam-identity` to create an IAM policy for IAM identify services. |
    {: caption="Table 5. iam service-policy-create command components" caption-side="bottom"}


4. Create an API key for the service ID with the **`iam service-api-key-create`** command. For a complete listing of the **`iam service-api-key-create`** command and its options, see the [**`ibmcloud iam service-api-key-create`**](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create) command. Name the API key similar to your service ID, and include the service ID that you previously created, `codeengine-<project_name>-id`. Be sure to give the API key a description that helps you retrieve the key later.

    For example, the following command creates a key that is called `codeengine-myproject-key` for the `codeengine-myproject-id` service ID with a description of `API key for service ID codeengine-myproject-id for {{site.data.keyword.codeengineshort}} myproject`:

    ```txt
    ibmcloud iam service-api-key-create codeengine-myproject-key codeengine-myproject-id --description "API key for service ID codeengine-myproject-id for Code Engine myproject"
    ```
    {: pre}

    Example output

    ```txt
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

    Now that you have your access policies in place for your service ID and your API key that is created, you can [add access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce) to pull images from your container registry.



## Controlling access to {{site.data.keyword.registryshort}} for {{site.data.keyword.codeengineshort}} workloads
{: #control-cr-access}

Suppose that you want to control access to {{site.data.keyword.registrylong_notm}} when {{site.data.keyword.codeengineshort}} pulls images. For example, you want to control access to {{site.data.keyword.registryshort}} to specific IP addresses. Consider the following approaches. 

* Use a [context-based restriction](/docs/Registry?topic=Registry-registry-cbr). By using a context-based restriction, if the IP addresses for your {{site.data.keyword.codeengineshort}} project ever change, you do not need to change your access. You can restrict access to {{site.data.keyword.registryshort}} to a network zone, where your network zone includes {{site.data.keyword.codeengineshort}} and anything that requires access to the registry. 

* Disable the public access to {{site.data.keyword.registrylong_notm}} and make sure {{site.data.keyword.codeengineshort}} uses the private endpoints instead of the public endpoints. See [Securing your connection to {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-registry-cbr). 

* To control access by a specific IP range, use an API endpoint to fetch the IP addresses for your particular {{site.data.keyword.codeengineshort}} project. It is important to note that these IP addresses are subject to change, and you must take appropriate steps when this happens. See [{{site.data.keyword.codeengineshort}} public and private IP addresses](/docs/codeengine?topic=codeengine-network-addresses) and [How can I add my {{site.data.keyword.codeengineshort}} app to an allowlist](/docs/codeengine?topic=codeengine-ts-allowlist-app)?



## Considerations for images in your registry
{: #considerations-registry}

The name of your image that is used for your app or job must be in one of the following formats.

- `REGISTRY/NAMESPACEorDOCKERUSERorDOCKERORG/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, do not include the colon (:). The default for `TAG` is `latest`.  
- `REGISTRY/NAMESPACEorDOCKERUSERorDOCKERORG/REPOSITORY@IMAGEID` where `REGISTRY` is optional. If `REGISTRY` is not specified, the default is `docker.io` and `ibm` as the Docker organization.

| Component | Characters allowed | Length | Additional rules |
| -------------- | -------------- | -------------- | -------------- |
| `REGISTRY` | `a-zA-Z0-9 -_.  --__` | 1-253 | `(0-127Periods)(label:1-63,noDashOnEnd)` |
| `NAMESPACE` | `a-z   0-9 -_   --__` | 4-30 | `(start/end with letterOrNumber)` |
| `DOCKERUSERorDOCKERORG` | `a-z   0-9` | 4-30 | |
| `REPOSITORY` | `a-z   0-9 -_. /` | 2-255 | `(start/end with letterOrNumber)` |
| `TAG` | `a-zA-Z0-9 -_.  --__..` | 0-128 | `(NOT start with periodOrDash)` |
| `IMAGEID` | `a-z   0-9    :` |  | `(startwith sha256: noOtherColon)` |
{: caption="Table 6. Rules for image name" caption-side="bottom"}

The parts of the image name must meet the following criteria.

- `REGISTRY` must be 253 characters or fewer and can contain lowercase or uppercase letters, numbers, periods (.), hyphens (-), and underscores (`_`). Do not use a dash (.) as the last character. Do not use more than 127 periods (.) and the labels between them can be between 1 and 63 characters long.
- `NAMESPACE` must be between 4 and 30 characters and must begin and end with a lowercase letter or number. `NAMESPACE` can contain lowercase alphanumeric characters, hyphens (-), and underscores (`_`).
- `DOCKERUSERorDOCKERORG` can be used for Docker registries instead of `NAMESPACE`. Specify your Docker username or Docker organization. Your Docker username and organization must be between 4 and 30 characters and contains only lowercase alphanumeric characters or numbers.
- `REPOSITORY` must be between 2 and 255 characters and must begin and end with a lowercase letter or number. `REPOSITORY` can contain lowercase alphanumeric characters, forward slashes (/), periods (.), hyphens (-), and underscores (`_`).
- `TAG` must be between 0 and 128 characters and can contain lowercase or uppercase letters, numbers, periods (.), hyphens (-), and underscores (`_`). The `TAG` must not begin with a period or dash. If you do not include a `TAG`, do not include the colon either.
- `IMAGEID` is prefixed with `sha256:` and can contain lowercase letters and numbers.

