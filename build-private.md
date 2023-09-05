---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-05"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine, registry secret, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Create a build configuration that pulls source from private repository
{: #build-config-gitrepo}

If your source is located in a private repository, create a build configuration with settings that include information about where to pull source from a private repository. For the build output, you can choose to specify registry details along with a registry secret to access your built image in the registry. Or, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}}. For this case, you do not need to specify a registry secret or the location of the image registry.
{: shortdesc}

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.

## Creating a build configuration from the console (private repo)
{: #build-config-gitrepo-ui}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a private repo, use an SSH URL for the code repository URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the last section.
7. In the **Output** section, enter the details of your container image. Select an existing registry access secret, or click **Create registry access secret** to add a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you. Then, select the namespace, repository, and tag of the image you want to build. You can choose to let {{site.data.keyword.codeengineshort}} create and manage the namespace in {{site.data.keyword.registryshort}} for you. If your image exists in {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build. 

After you create the build, you must [run the build](#build-run). 

## Creating a build configuration with the CLI (private repo)
{: #build-config-gitrepo-cli}

To create a build configuration with the CLI, use the **`build create`** command. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

With the **`build create`** command, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source for you and storing the image in {{site.data.keyword.registrylong_notm}}. For this *automatic access* case, you do not need to specify a registry secret or the location of the image registry. Or, you can specify the location for your build image output and provide a registry secret so that {{site.data.keyword.codeengineshort}} can access and push the build result to your registry. 

### Creating a build configuration with the CLI (with private repo source and automatic access to registry)
{: #build-config-gitrepo-cli-a}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your private repository source, and automatically uploads the image to {{site.data.keyword.registrylong_notm}}. See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a Git repository secret to access your source](/docs/codeengine?topic=codeengine-code-repositories).


1. Create a build configuration to build an image from a private repository and let {{site.data.keyword.codeengineshort}} automatically store and access the image. For example, the following **`build create`** command creates a build configuration that is called `helloworld-build-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, and uses the `buildpacks` strategy and `medium` build size. {{site.data.keyword.codeengineshort}} automatically uploads the image to {{site.data.keyword.registrylong_notm}}. Also, because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo. By not specifying the location of the image registry or a registry secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 

    Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.

    ```txt
    ibmcloud ce build create --name helloworld-build-private --source git@github.com:myprivaterepo/builds.git --context-dir /hello --strategy buildpacks --git-repo-secret myrepo
    ```
    {: pre}

2. After you create the build, you must [run the build](#build-run). 


### Creating a build configuration with the CLI (with private repo source and user-provided access to registry) 
{: #build-config-gitrepo-cli-b}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your private repository source with a Git repository secret that you provide, and then uploads the image to your container registry with the registry access that you provide. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a Git repository secret to access your source](/docs/codeengine?topic=codeengine-code-repositories).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).


1. Create a build configuration to build an image from a private repo and specify the location of the image registry for the build output with a registry secret. With the **`build create`** command, specify the `--image` option to provide the location of the image registry, and specify the `--registry-secret` option to access the registry. For example, the following command creates a build configuration that is called `helloworld-build-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, uses the `buildpacks` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the registry secret that is defined in `myregistry`.

    Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.

    In this example, the command uses the default `medium` build size. Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository.

    ```txt
    ibmcloud ce build create --name helloworld-build-private --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source git@github.com:myprivaterepo/builds.git --context-dir /hello --strategy buildpacks --git-repo-secret myrepo
    ```
    {: pre}

2. After you create the build, you must [run the build](#build-run). 

