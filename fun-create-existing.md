---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-17"

keywords: functions in code engine, functions, serverless, create functions in code engine, function workloads in code engine, registry secret, registry access, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating function workloads from existing code bundles
{: #fun-create-existing}

Create your {{site.data.keyword.codeengineshort}} function with a code bundle in {{site.data.keyword.registrylong}}. You can create a function from the console or with the CLI.
{: shortdesc}

A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image.

You cannot pull code bundles from a location other than {{site.data.keyword.registryshort}}.
{: note}

Before you begin

- You must have a code bundle in {{site.data.keyword.registrylong}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started). Or, you can build an image from [repository source](/docs/codeengine?topic=codeengine-fun-create-repo) or from [local source](/docs/codeengine?topic=codeengine-fun-create-local).

- Verify that you can access the registry. See [Setting up authorities for container registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

Interested in configuring your project such that all users of the project can store and access images in {{site.data.keyword.registryshort}} without having to manually create registry secrets? With sufficient permissions, you can configure this default registry access on a per location (region) basis. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions. See [Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations). 
{: note}


## Creating a function that references a code bundle in {{site.data.keyword.registryshort}} with the console
{: #create-fun-cr-console}

Create a function that uses an existing code bundle by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically pull code bundles from {{site.data.keyword.registryshort}}.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Let's go**.
3. Select **Function**.
4. Enter a name for the function; for example, `myfunction`. Use a name for your function that is unique within the project.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must select a project to create a function.
6. Select a **Runtime image** for your function code. For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).
7. Select to **Use an existing code bundle**.
8. Specify the location of your code bundle in the format `registry/namespace/repository:tag`.
9. If your code bundle is in your account or in a public registry, you do not need to specify a registry secret. If the code bundle is in a private registry, you must add the registry secret. For additional help, click **Help me specify the code bundle**. For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).
10. Specify your resource information, including [CPU and memory combinations](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo) and [Scale down delay](/docs/codeengine?topic=codeengine-fun-work#functions-scale).
11. Optionally, specify a [custom domain](/docs/codeengine?topic=codeengine-fun-domainmapping) or [environment variables](/docs/codeengine?topic=codeengine-envvar).
12. Click **Create**.
13. After the function status changes to **Ready**, you can test the function. Click **Test function** and then click **Send request**. To open the function in a web page, click **Function URL**.




## Deploying a function with an existing code bundle with the CLI
{: #fun-cr-cli}

Create a function that uses a code bundle that is stored in {{site.data.keyword.registrylong}} with the CLI with the **`ibmcloud ce fn create`** command. For a complete listing of options, see the [**`ibmcloud ce fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
* Before you can work with a {{site.data.keyword.codeengineshort}} function that references a code bundle in {{site.data.keyword.registryshort}}, you must first add access to the registry so {{site.data.keyword.codeengineshort}} can pull the code bundle when the function is created. For information about the required permissions for accessing registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

### Deploying a function from a public registry with the CLI
{: #fun-cr-cli-public}


If your existing code bundle is in your account or a public registry, you can use the **`ibmcloud ce fn create`** command.

For example, run the following command to pull an existing code bundle from the public registry and create a function.

```txt
ibmcloud ce fn create --name myhellofun --code-bundle icr.io/codeengine/samples/function-nodejs-codebundle --runtime nodejs
```
{: pre}

Run the provided **`fn get`** command to find the URL. You can then use the `curl` command to call that URL.

Example output from the existing code bundle.

```txt
<html><body><h3>Hello, Functions on CodeEngine!</h3></body></html>
```
{: screen}

### Deploying a function from a private registry with the CLI
{: #fun-cr-cli-private}

To access an existing code bundle from a private registry, you must set up access to the registry, create a registry secret, and then provide that secret when you run the **`ibmcloud ce fn create`** command.

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key). To create an {{site.data.keyword.cloud_notm}} IAM API key with the CLI, run the [**`iam api-key-create`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=ui#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of `My CLI API key` and save it to a file called `key_file`, run the following command:

    ```txt
    ibmcloud iam api-key-create cliapikey -d "My CLI API key" --file key_file
    ```
    {: pre}

    If you choose to not save your key to a file, you must record the API key that is displayed when you create it. You cannot retrieve it later.
    {: important}

2. After you create your API key, create a registry secret to {{site.data.keyword.codeengineshort}}. To create a registry secret, use the [**`ibmcloud ce secret create --format registry`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. For example, the following command creates registry access to a {{site.data.keyword.registryshort}} instance called `myregistry`. Note, even though the `--server` and `--username` options are specified in the example command, the default value for the `--server` option is `us.icr.io` and the `--username` option defaults to `iamapikey` when the server is `us.icr.io`.

    ```txt
    ibmcloud ce secret create --format registry --name myregistry --server us.icr.io --username iamapikey --password APIKEY
    ```
    {: pre}

    Example output

    ```txt
    Creating registry secret 'myregistry'...
    OK
    ```
    {: screen}

3. Create your function and reference a code bundle in a private registry in {{site.data.keyword.registryshort}}. For example, use the [**`ibmcloud ce fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command to create the `myhellofun` function to reference the `icr.io/codeengine/samples/function-nodejs-codebundle` by using the `myregistry` access information.

    ```txt
    ibmcloud ce fn create --name myhellofun --code-bundle icr.io/NAMESPACE/REGISTRY:TAG --registry-secret myregistry
    ```
    {: pre}

    The format of the name of the code bundle for this function is `REGISTRY/NAMESPACE/REGISTRY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `icr.io`. If `TAG` is not specified, the default is `latest`.
    {: important}

4. After your function creates, you can invoke it. To find the URL of your function, run the provided `ibmcloud ce fn get` command. You can then use the `curl` command to call that URL.


## Next steps
{: #nextsteps-funrunexisting}


- After your function is created, you can access your function by clicking **Test function** in the console or finding the URL for your function with the [**`function get`**](/docs/codeengine?topic=codeengine-cli#cli-function-get) command.

- You can create a [custom domain mapping](/docs/codeengine?topic=codeengine-domain-mappings) and assign it to your function.  

- After your function is created and deployed, you can update the function to meet your needs from the console or by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

After your function is created, you can update your function and its referenced code by using *any* of the following ways, independent of how you created or previously updated your function:

- If you have an existing code bundle, then you need to provide only a reference to the image, which points to the location of your container registry when you deploy your app. For more information, see [Creating function workloads from existing code bundles](/docs/codeengine?topic=codeengine-fun-create-existing).

    If you created your function by using the **`function create`** command and you specified the `--build-source` option to build the code bundle from local or repository source, and you want to change your function to point to a different code bundle, you must first remove the association of the build from your function. For example, run `ibmcloud ce function update -n FUN_NAME --build-clear`. After you remove the association of the build from your function, you can update the function to reference a different image. 
    {: note}

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} to build the code bundle from your source and create your function with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code bundle to {{site.data.keyword.registrylong}}. To learn more, see [Creating your function from repository source code](/docs/codeengine?topic=codeengine-fun-create-repo).

- If you are starting with source code that resides on a local workstation, you can choose for {{site.data.keyword.codeengineshort}} to build the code bundle from your source and create your function with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your source code and code bundle to {{site.data.keyword.registrylong}}. 

    For example, you might choose for {{site.data.keyword.codeengineshort}} to build your local source while you evolve the development of your source for the function. Then, after the code bundle is matured, you can update your function to reference the specific code bundle that you want. You can repeat this process as needed.



Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
