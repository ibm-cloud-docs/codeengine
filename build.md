---

copyright:
  years: 2022
lastupdated: "2022-01-12"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Building a container image
{: #build-image}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.
{: shortdesc}

{{site.data.keyword.codeenginefull}} pulls source code from a repository, builds it, and then pushes the container image to a registry. You can choose public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). With {{site.data.keyword.codeengineshort}}, you first set up the option for your build configuration and then you run it. After your build is complete, you can deploy the container images as applications or run them as jobs. Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build).

Note that if you build multiple versions of the same container image, the most current version of the container image is downloaded and used when you run your job or deploy your application.

## Create a build configuration that pulls source from public repository
{: #build-create-config}

You can create a build configuration that pulls source from a public repository. You must specify the details of your source repository, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

### Creating a build configuration from the console (public repo)
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a public repo, use an HTTPS URL and select **Public** for the code repo access. An example of an HTTPS URL is `https://github.com/IBM/CodeEngine`. If your code is in a private repo, use an SSH URL for the code repo URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the last section.
7. In the **Output** section, you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository, and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

### Creating a build configuration with the CLI (public repo)
{: #build-create-cli}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, uses the `dockerfile` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`. The branch for this Git repo is `main`. If you do not provide a branch name with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. 

If you are using the `--strategy` option with the value of `dockerfile`, then ensure the `--dockerfile` option is correctly set to the name of the `dockerfile`. The default value for the `--strategy` option is `Dockerfile`. 
{: important}

```sh
ibmcloud ce build create --name helloworld-build --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --commit main --context-dir /hello --strategy dockerfile --size medium
```
{: pre}

The following example shows the output of the **`build create`** command.

```sh 
Creating build helloworld-build...
OK
```
{: screen}

The following table summarizes the options that are used with the **`build create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command.

| Option | Description |
| --- | --- |
| `--name` | The name of the build. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 55 characters or fewer and can contain letters, numbers, and hyphens (-). |  |
| `--image` | The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is required. |
| `--registry-secret` | The image registry access secret that is used to access the registry. You can add the image registry access secret by running the **`registry create`** command. The image registry access secret is used to authenticate with a private registry. This value is required. |
| `--source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`. |
| `--commit` | The commit, tag, or branch in the source repository to pull. |
| `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory. |
| `--size` | The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, and `xlarge`. |
| `--strategy` | The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. |
{: caption="Table 1. Command components" caption-side="bottom"}

During this process, your build is validated. You can check the status of your build by running the [**`ibmcloud ce build get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. For example, use the following **`build get`** command to check the status of the build configuration from the previous example:

```sh
ibmcloud ce build get --name helloworld-build
```
{: pre}

The following example shows the output of the **`build get`** command.

```sh
Getting build 'helloworld-build'
OK

Name:          helloworld-build  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           2d15h
Created:       2021-03-14T14:48:19-05:00  
Status:        Succeeded  
Reason:        all validations succeeded

Last Build Run:
  Name:     helloworld-build-run-211001-2116380
  Age:      89s
  Created:  2021-10-08T16:16:38-05:00

Image:              us.icr.io/mynamespace/codeengine-helloworld
Registry Secret:    myregistry
Build Strategy:     dockerfile-medium
Timeout:            10m0s
Source:             https://github.com/IBM/CodeEngine
Commit:             main
Context Directory:  /hello
Dockerfile:         Dockerfile

Build Runs:
  Name                                 Status                              Image                                        Age
  helloworld-build-run-211001-2116380  All Steps have completed executing  us.icr.io/mynamespace/codeengine-helloworld  91s
  helloworld-build-run                 All Steps have completed executing  us.icr.io/mynamespace/codeengine-helloworld  39d

```
{: screen}

If you receive a command validation failure, check that your secret exists. If you refer to an image registry access secret (`--registry-secret`) for your image and the secret does not exist, see [Accessing a private container registry](/docs/codeengine?topic=codeengine-add-registry). If you refer to a Git repository access secret (`--git-repo-secret`) to work with source in a private repository and the secret does not exist, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}


## Creating a build configuration that references a Git repository access secret
{: #build-config-gitrepo}

You can create a build configuration that pulls source from a private repository. You must specify the details of your source repository, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}


### Creating a build configuration from the console (private)
{: #build-config-gitrepo-ui}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a private repo, use an SSH URL for the code repository URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the last section.
7. In the **Output** section, you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository, and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

### Creating a build configuration with the CLI (private)
{: #build-config-gitrepo-cli}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

This example pulls code from a private repository and so references a Git repository secret. 

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, uses the `buildpacks` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`. 

Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.

For example, see the following **`build create`** command.

```sh
ibmcloud ce build create --name helloworld-build-private --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source git@github.com:myprivaterepo/builds.git --commit main --context-dir /hello --strategy buildpacks --size medium --git-repo-secret myrepo
```
{: pre}

## Running a build
{: #build-run}

After you create a build configuration, you can submit a run based on that build configuration. Run your build from the console or with the CLI.
{: shortdesc}

{{site.data.keyword.codeengineshort}} has quotas for builds and build runs within a project. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
{: important}

### Running a build from the console
{: #build-run-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you created your build.
3. From the project page, click **Image builds**.
4. Select your build configuration.
5. In the **Configuration** section, you can review the build configuration and changes values, if needed.
6. To submit your build, click **Submit build**.
7. Verify any additional information, such as the **Image tag** to create a specific tag for this build run or overwrite the **Timeout** value.
8. Submit the build run by clicking **Submit build**.

Monitor your build progress in the **Build runs** section.

### Creating a build run with the CLI
{: #build-run-cli}

To submit a build run from a build configuration with the CLI, use the **`buildrun submit`** command. This command requires the name of a build configuration and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.
{: shortdesc} 

The following example runs a build that is called `helloworld-build-run` and uses the `helloworld-build` build.

```sh
ibmcloud ce buildrun submit --build helloworld-build --name helloworld-build-run 
```
{: pre}

The following example shows the output of the **`buildrun submit`** command.

```sh
Submitting build run 'helloworld-build-run'...
Run 'ibmcloud ce buildrun get -n helloworld-build-run' to check the build run status.
OK 
```
{: screen}

The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.


| Option | Description |
| --- | --- |
| `--build` | The name of the build configuration to use. This value is required. |
| `--name` | The name of the build run. Use a name that is unique within the project.  \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |
{: caption="Table 2. Command components" caption-side="bottom"}

Your build runs begins. Monitor the progress by using the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. 

For example, to check the status of the build run from the previous example:

```sh
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

The following example shows the output of the **`build get`** command.

```sh
Getting build run 'helloworld-build-run'...
[...]
OK

Name:          helloworld-build-run  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           21m  
Created:       2021-03-14T14:50:13-05:00  

Summary:  Succeeded  
Status:   Succeeded  
Reason:   Succeeded
```
{: screen}

For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Next steps for builds
{: #nextsteps-buildimage}

You can now create an application or job from your container image. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


