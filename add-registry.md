---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-30"

keywords: registries, container registry, image registry, apikey, API key, access token, images, registry access, service id

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Accessing container registries
{: #add-registry}

Images that are used by {{site.data.keyword.codeenginefull}} are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).
{: shortdesc}

A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private.

## Types of image registries
{: #types-registries}

Images are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).

Public registries, such as public Docker Hub, can be used to get started with Docker and {{site.data.keyword.codeengineshort}} to create your first application or job. But when it comes to enterprise workloads, use a private registry, such as the one provided in {{site.data.keyword.registrylong_notm}} to protect your images from being used and changed by unauthorized users. Access to private registries must be set up to ensure that the credentials to access the private registry are available.

| Registry | Description |
|--------|---------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started)| With this option, you can set up your own secured image repository in {{site.data.keyword.registrylong_notm}} where you can safely store and share images between users.<p>With {{site.data.keyword.registrylong_notm}}, you can:</p><ul><li>Manage access to images in your account.</li><li>Use {{site.data.keyword.IBM_notm}} provided images and sample apps, such as {{site.data.keyword.IBM_notm}} Liberty, as a parent image and add your own app code to it.</li></ul> |
|Any other private registry | Connect any existing private registry to {{site.data.keyword.codeengineshort}} by adding access. Adding access  securely saves your registry URL and credentials in a Kubernetes secret.<p>With private registries, you can:</p><ul><li>Use existing private registries independent of their source (Docker Hub, organization-owned registries, or other private Cloud registries).</li></ul> |
| [Public Docker Hub](https://hub.docker.com/){: external}{: #dockerhub}| Use this option to pull existing public images from Docker Hub directly in your {{site.data.keyword.codeengineshort}} applications or jobs. <p>**Important**</p> <ul><li>This option might not meet your organization's security requirements such as access management, vulnerability scanning, or app privacy.</li><li>When you pull an image from Docker Hub to use with apps or jobs in {{site.data.keyword.codeengineshort}}, be aware of <a href="https://docs.docker.com/docker-hub/download-rate-limit">Docker rate limits</a> <img src="../icons/launch-glyph.svg" alt="External link icon"> for free plan (anonymous) users. You might experience pull limits if you receive a <code>429</code> error indicating you have reached your pull rate limit. To <a href="https://www.docker.com/increase-rate-limits">increase rate limits</a> <img src="../icons/launch-glyph.svg" alt="External link icon">, you can upgrade your account to a Docker <code>Pro</code> or <code>Team</code> subscription.</li></ul><p>With public Docker Hub, you can:</p><ul><li>These images can be referred to directly when you create an app or job, no additional setup is required.</li><li>Includes various open source applications.</li></ul> |
{: caption="Public and private image registry options" caption-side="top"}



## Setting up authorities for image registries
{: #authorities-registry}

if your registry is public, you do not have to set up authorities in order to pull images. Note that pulling images from a public registry while you are getting started with {{site.data.keyword.codeengineshort}} is acceptable, use a private registry when it comes to your enterprise workloads.

**What authorities do I need?**

When you deploy apps or run jobs from the console, {{site.data.keyword.codeengineshort}} can automatically access images that are in your own account. If you want to access images from a shared account, other {{site.data.keyword.cloud_notm}} accounts, or a private Docker account, you must be assigned the proper access authorities.

| Action | IAM service access | Description |
|--------|-----------|---------------------|
| Pull images | `Read` access | When you deploy an image as an application or job, you must pull the image from a registry. To pull images, you need `read` access. Note that if the repository is public, you already have `read` access to the images. |
| Push images | `Read` and `write` access | When you build source code, you must push the image to a registry. To push images, you need `write` access to {{site.data.keyword.registryfull_notm}}. You cannot push images to a registry other than {{site.data.keyword.registryfull_notm}}. |
| Create a namespace | `Read`, `write`, and `Manager` access | To create a namespace in {{site.data.keyword.registrylong_notm}}, you must have `manager` access. In order to pull and push images, you must have `read` and `write` access. |

<br />

**Can I use a service ID?**

Yes, you can create a service ID and assign authorities to it. Note that service IDs are also automatically created by the {{site.data.keyword.codeengineshort}} UI when you automatically create access to your {{site.data.keyword.registryfull_notm}}. DO NOT delete this service ID as you will lose access to the images in the registry.

**Can I access images in a different registry?**

Yes! [Here is how](#images-different-account).

**Can I restrict pull access to a certain regional registry or even a single namespace?**

Yes, you can edit the existing [IAM policy of the service ID](#authorize-cr-service-id) that restricts the **Reader** service access role to that regional registry or a registry resource such as a namespace. Before you can customize registry IAM policies, you must [enable {{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-user#existing_users).

## Accessing images from a public account
{: #images-public-account}

If your image is stored in a public repository, such as a public Docker Hub, then you can simply reference the image directly when you deploy your application or run your job. Note that while storing images in a public registry is fine for getting started with applications and jobs, store your enterprise images in a private registry.

## Accessing images in your own account from console
{: #images-your-account}

If you are accessing {{site.data.keyword.codeengineshort}} from an account that you own or administer, then {{site.data.keyword.codeengineshort}} can automatically push and pull images to and from an {{site.data.keyword.registryfull_notm}} namespace in your account when you create or update apps, jobs, or builds from the console. {{site.data.keyword.codeengineshort}} can even create a namespace for you when you push an image. For more information, see the following topics.

- [Deploying an app that references an image in {{site.data.keyword.registryfull_notm}} with the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console).
- [Deploying your app from source code](/docs/codeengine?topic=codeengine-deploy-app-source-code).
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
9. Enter the password. For {{site.data.keyword.registryfull_notm}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#access-private-docker-hub).
10. Click **Create**.

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

```sh
Creating image registry access secret 'myregistry'...
OK
```
{: screen}

The following table summarizes the options that are used with the **`registry create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the image registry access secret. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-). |
| `--server` | Enter the URL of the registry server. For {{site.data.keyword.registryshort}}, the server name is `<region>.icr.io`. For example, `us.icr.io`. For [Docker Hub](https://hub.docker.com/), the value is `https://index.docker.io/v1/`.|
| `--username` | Enter the username to access the registry server. For {{site.data.keyword.registryshort}}, it is `iamapikey`. For Docker Hub, it is your Docker ID. |
| `--password` | Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. For Docker Hub, you can use your Docker Hub password or an [access token](#access-private-docker-hub). |
{: caption="Table 1. registry create command components" caption-side="top"}

## Authorizing access to {{site.data.keyword.registryshort}} with service ID
{: #authorize-cr-service-id}

Before you can add access to a service ID in a different account, you must first authorize access to the service ID.

When you create a service ID, you can restrict access to a regional {{site.data.keyword.registryfull_notm}} or even a specific namespace within that {{site.data.keyword.registryfull_notm}} account.

### Authorizing access to {{site.data.keyword.registryshort}} with service ID from the console
{: #authorize-console-service-id}

In order to pull or push images from or to {{site.data.keyword.registryfull_notm}}, you must create a service ID, create an access policy for the service ID, and then create an API key to store the credentials.

#### Step 1 Create the service ID and authorize it to the {{site.data.keyword.registryfull_notm}} service
{: #create-service-id}

1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview).
2. Select **Service IDs**.
3. If you have a Service ID that you want to use, select it. If not, select **Create**, enter a name and description,  and click **Create**.
4. From the Service ID page, select **Access policies** and then **Assign access**.
5. From the **Assign service ID additional access** section,
    1. Select **IAM services**.
    2. Select **Container Registry** for type of access.
    3. Select the type of access: **All resources** or **Resources based on attributes**. If you specify **Resources based on attributes**, you can add attributes based on resource group, region, resource type, or resource name to further restrict access. 
    4. For Service access, select the type of access you want to grant. If you plan to use only images for your applications and jobs, select **Reader**. If you want to push the outcome of builds, then also select **Writer**.
    5. Click **Add** and then **Assign**.

#### Step 2 Creating an API key for a service ID
{: #create-api-key}

Create an API key for a service ID.

1. From the Service ID page, select **API keys** and then **Create**.
2. Enter a name and optional description for your API key and click **Create**.
3. Copy the API key or click download to save it. 

    You won’t be able to see this API key again, so be sure to record it in a safe place.
    {: important}

#### Step 3 Authorize service ID to get details of an API key with the console
{: #authorize-service-id}

Now that our service ID is created and is granting access to {{site.data.keyword.registryshort}}, you must authorize the service ID to also get details of an API key by giving the service ID IAM Identity service access for Account management.

1. From the Service ID page, select **Access policies** and then **Assign access**.
2. From the **Assign service ID additional access** section,
    1. Select **Account management**.
    2. Select **IAM Identity service** for type of access to assign.
    3. Select the services that you want to assign access: **All resources** or **Resources based on attributes**. If you specify **Resources based on attributes**, you can add attributes based on location, service instance, resource group, or resource ID to further restrict access. 
    4. For Platform access, select **Operator** access or higher.
    5. Click **Add** and then **Assign**.


Now that you have your access policies in place for your service ID and your API key created, you can [add access to {{site.data.keyword.codeengineshort}}](#add-registry-access-ce) in order to pull images from your container registry.

### Authorizing access to {{site.data.keyword.registryshort}} with the CLI
{: #authorize-cr-cli}

In order to pull images from {{site.data.keyword.registryfull_notm}} in a different account, you must create a service ID, create access policies for the service ID, and then create an API key to store your credentials.
{: shortdesc}

1. Create an {{site.data.keyword.cloud_notm}} IAM service ID for your project that is used for the IAM policies and API key credentials in the image pull secret with the **`iam service-id-create`** command. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the project name. For a complete listing of the **`iam service-id-create`** command and its options, see the [**`ibmcloud iam service-id-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_id_create) command.

    For example, the following command creates a service ID called `codeengine-myproject-id` with the description `Service ID for IBM Cloud Container Registry in {{site.data.keyword.codeengineshort}} project myproject`:

    ```sh
    ibmcloud iam service-id-create codeengine-myproject-id --description "Service ID for IBM Cloud Container Registry in {{site.data.keyword.codeengineshort}} project my proj"
    ```
    {: pre}

2. Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your service ID that grants access to {{site.data.keyword.registrylong_notm}} with the **`iam service-policy-create`** command. For a complete listing of the **`iam service-policy-create`** command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    For example, the following command creates a policy for `codeengine-myproject-id` service ID with the role of `Reader`:

    ```sh
    ibmcloud iam service-policy-create codeengine-myproject-id --roles Reader --service-name container-registry
    ```
    {: pre}

    The following table summarizes the options that are used with the **`iam service-policy-create`** command in this example. For more information about the command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `<service_ID>` | Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created. |
    | `--roles <service_access_role>` | Required. Enter the [service access role for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-iam#service_access_roles) that you want to scope the service ID access to. Possible values are `Reader`, `Writer`, and `Manager`. If you are pulling images, then `Reader` access is sufficient. For more information, see [Setting up authorities for image registries](#authorities-registry).|
    | `--service-name <container-registry>` | Required. Enter `container-registry` to create an IAM policy for {{site.data.keyword.registrylong_notm}}. 
    {: caption="Table 1. iam service-policy-create command components" caption-side="top"}


3. Create a custom service policy to allow access to `iam-identity` service so that {{site.data.keyword.codeengineshort}} can retrieve the API key for your service ID  with the **`iam service-policy-create`** command. 

    For example, create a policy for `codeengine-myproject-id` service ID with the role of `Operator`:

    ```sh
    ibmcloud iam service-policy-create codeengine-myproject-id --roles Operator --service-name iam-identity
    ```
    {: pre}

    The following table summarizes the options that are used with the **`iam service-policy-create`** command in this example. For more information about the command and its options, see the [**`ibmcloud iam service-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_policy_create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `<service_ID>` | Required. Replace with the `codeengine-<project_name>-id` service ID that you previously created. |
    | `--roles <platform_access_role>` | Required. Enter the platform access role that you want to scope the service ID access to. Possible values are `Administrator`, `Editor`, `Operator`, and `Viewer`. Your service ID requires `Operator` or higher. |
    | `--service-name <iam-identity>` | Required. Enter `iam-identity` to create an IAM policy for IAM identify services. |
    {: caption="Table 1. iam service-policy-create command components" caption-side="top"}


4. Create an API key for the service ID with the **`iam service-api-key-create`** command. For a complete listing of the **`iam service-api-key-create`** command and its options, see the [**`ibmcloud iam service-api-key-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create) command. Name the API key similar to your service ID, and include the service ID that you previously created, `codeengine-<project_name>-id`. Be sure to give the API key a description that helps you retrieve the key later.

    For example, the following command creates a key called `codeengine-myproject-key` for the `codeengine-myproject-id` service ID with a description of `API key for service ID codeengine-myproject-id for {{site.data.keyword.codeengineshort}} myproject`:

    ```sh
    ibmcloud iam service-api-key-create codeengine-myproject-key codeengine-myproject-id --description "API key for service ID codeengine-myproject-id for {{site.data.keyword.codeengineshort}} myproject"
    ```
    {: pre}

    **Example output**

    ```sh
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

## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}: Container registry implementation
{: #private-registry-imp}

To pull images from a registry, {{site.data.keyword.codeengineshort}} uses a special type of Kubernetes secret that is called an `imagePullSecret`. This image pull secret stores the credentials to access a container registry. When you add access to a container registry with {{site.data.keyword.codeengineshort}}, you are creating an image pull secret. For more information about image pull secrets, see [Kubernetes documentation](https://kubernetes.io/docs/home/){: external}.


