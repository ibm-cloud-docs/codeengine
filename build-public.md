---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-05"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine, registry secret, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Create a build configuration that pulls source from public repository
{: #build-create-config1}

If your source is located in a public repository, create a build configuration with settings that include information about where to pull source from a public repository. For the build output, you can choose to specify registry details along with a registry secret to access your built image in the registry. Or, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}}. For this case, you do not need to specify a registry secret or the location of the image registry.
{: shortdesc}

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.

## Creating a build configuration from the console (public repo)
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a public repo, use an HTTPS URL and select **None** for the code repo access. An example of an HTTPS URL is `https://github.com/IBM/CodeEngine`. If your code is in a private repo, use an SSH URL for the code repo URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the section to specify build output details.
7. In the **Output** section, enter the details of your container image. Select an existing registry access secret, or click **Create registry access secret** to add a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you. Then, select the namespace, repository, and tag of the image you want to build. You can choose to let {{site.data.keyword.codeengineshort}} create and manage the namespace in {{site.data.keyword.registryshort}} for you. If your image exists in {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

After you create the build, you must [run the build](#build-run). 

## Creating a build configuration with the CLI (public repo)
{: #build-create-cli}

To create a build configuration with the CLI, use the **`build create`** command. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

With the **`build create`** command, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source for you and then storing the image in {{site.data.keyword.registrylong_notm}}. For this *automatic access* case, you do not need to specify a registry secret or the location of the image registry. Or, you can specify the location for your build image output and provide a registry secret so that {{site.data.keyword.codeengineshort}} can access and push the build result to your registry. 

### Creating a build configuration with the CLI (with public repo source and automatic access to registry)
{: #build-create-cli-a}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your public Git repository source, and automatically uploads the image to {{site.data.keyword.registrylong_notm}} with automatic access. See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create a build configuration to build an image from a public Git repo and let {{site.data.keyword.codeengineshort}} automatically store and access the image. For example, the following **`build create`** command creates a build configuration that is called `helloworld-build` that builds from source in the public Git repo `https://github.com/IBM/CodeEngine`. In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo. By not specifying the location of the image registry or a registry secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 

    ```txt
    ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine --context-dir /hello 
    ```
    {: pre}

    Example output

    ```txt 
    Creating build helloworld-build...
    OK
    ```
    {: screen}

    The following table summarizes the options that are used with the **`build create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 55 characters or fewer and can contain letters, numbers, and hyphens (-). |  |
    | `--source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`.  |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory. This value is optional. |
    {: caption="Table 1. Command description" caption-side="bottom"}


2. Use the **`build get`** command to check the status of your build. 

    ```txt
    ibmcloud ce build get --name helloworld-build
    ```
    {: pre}

    Example output

    Notice the generated name for the image, and that the name of the automatically created registry secret is of the format, `ce-auto-icr-private-<region>`.

    ```txt
    Getting build 'helloworld-build'
    OK

    Name:          helloworld-build  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-05-24T09:58:43-05:00  
    Build Type:    git  
    Status:        Succeeded  
    Reason:        all validations succeeded 

    Image:              private.us.icr.io/ce--e97a8-odof2whblw5/build-helloworld-build
    Registry Secret:    ce-auto-icr-private-us-south  
    Build Strategy:     dockerfile-medium
    Timeout:            10m0s
    Source:             https://github.com/IBM/CodeEngine
    Commit:             main
    Context Directory:  /hello
    Dockerfile:         Dockerfile

    ```
    {: screen}

3. After you create the build, you must [run the build](#build-run). 

### Creating a build configuration with the CLI (with public repo source and user-provided access to registry) 
{: #build-create-cli-b}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your public Git repository source, and then uploads the image to your container registry with the registry access that you provide. 


Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).

1. Create a build configuration to build an image from a public Git repo and specify the location of the image registry for the build output with a registry secret. With the **`build create`** command, specify the `--image` option to provide the location of the image registry, and specify the `--registry-secret` option to access the registry. For example, the following command creates a build configuration that is called `helloworld-build2` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the `myregistry` registry secret. In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo. 

    If you are using the `--strategy` option with the value of `dockerfile`, then ensure the `--dockerfile` option is correctly set to the name of the `dockerfile`. The default value for the `--strategy` option is `Dockerfile`. 
    {: important}

    ```txt
    ibmcloud ce build create --name helloworld-build2 --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --context-dir /hello 
    ```
    {: pre}

    Example output

    ```txt 
    Creating build helloworld-build2...
    OK
    ```
    {: screen}

    The following table summarizes the options that are used with the **`build create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 55 characters or fewer and can contain letters, numbers, and hyphens (-). |  |
    | `--image` | The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. |
    | `--registry-secret` | The registry secret that is used to access the registry. You can add the registry secret by running the **`secret create --format registry`** command. The registry secret is used to authenticate with a private registry.  |
    | `--source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`.  |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory. This value is optional. |
    {: caption="Table 2. Command description" caption-side="bottom"}

2. Use the **`build get`** command to check the status of your build. 

    ```txt
    ibmcloud ce build get --name helloworld-build2
    ```
    {: pre}

    Example output

    ```txt
    Getting build 'helloworld-build2'
    OK

    Name:          helloworld-build2  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2021-03-14T14:48:19-05:00  
    Status:        Succeeded  
    Reason:        all validations succeeded

    Image:              us.icr.io/mynamespace/codeengine-helloworld
    Registry Secret:    myregistry
    Build Strategy:     dockerfile-medium
    Timeout:            10m0s
    Source:             https://github.com/IBM/CodeEngine
    Commit:             main
    Context Directory:  /hello
    Dockerfile:         Dockerfile

    ```
    {: screen}

3. After you create the build, you must [run the build](#build-run). 

If you receive a command validation failure, check that your secret exists. If you refer to an registry secret (`--registry-secret`) for your image and the secret does not exist, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}



