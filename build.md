---

copyright:
  years: 2022
lastupdated: "2022-04-13"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Building a container image
{: #build-image}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.
{: shortdesc}

{{site.data.keyword.codeenginefull}} pulls source code from a repository or a local directory, builds it, and then pushes (uploads) the container image to a registry. You can choose public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). With {{site.data.keyword.codeengineshort}}, you first set up the option for your build configuration and then you run it. After your build is complete, you can deploy the container images as applications or run them as jobs. Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build).

Note that if you build multiple versions of the same container image, the most current version of the container image is downloaded and used when you run your job or deploy your application.

## Create a build configuration that pulls source from public repository
{: #build-create-config}

You can create a build configuration that pulls source from a public repository. You must specify the details of your source, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.



Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

### Creating a build configuration from the console (public repo)
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a public repo, use an HTTPS URL and select **None** for the code repo access. An example of an HTTPS URL is `https://github.com/IBM/CodeEngine`. If your code is in a private repo, use an SSH URL for the code repo URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the section to specify build output details.
7. In the **Output** section, enter the details of your container image. Select an existing registry access secret, or click **Create registry access secret** to add a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you. Then, select the namespace, repository, and tag of the image you want to build. You can choose to let {{site.data.keyword.codeengineshort}} create and manage the namespace in {{site.data.keyword.registryshort}} for you. If your image exists in {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

After you create the build, you must [run the build](#running-a-build ). 

### Creating a build configuration with the CLI (public repo)
{: #build-create-cli}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the `myregistry` image registry secret. In this example, the command uses the default `dockerfile` strategy, the default `medium` build size. Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo. 

If you are using the `--strategy` option with the value of `dockerfile`, then ensure the `--dockerfile` option is correctly set to the name of the `dockerfile`. The default value for the `--strategy` option is `Dockerfile`. 
{: important}

```txt
ibmcloud ce build create --name helloworld-build --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --context-dir /hello 
```
{: pre}

The following example shows the output of the **`build create`** command.

```txt 
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
| `--source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`.  |
| `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory. This value is optional. |
{: caption="Table 1. Command components" caption-side="bottom"}

During this process, your build is validated. You can check the status of your build by running the [**`ibmcloud ce build get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. For example, use the following **`build get`** command to check the status of the build configuration from the previous example:

```txt
ibmcloud ce build get --name helloworld-build
```
{: pre}

The following example shows the output of the **`build get`** command.

```txt
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

After you create the build, you must [run the build](#running-a-build ). 

If you receive a command validation failure, check that your secret exists. If you refer to an image registry access secret (`--registry-secret`) for your image and the secret does not exist, see [Accessing a private container registry](/docs/codeengine?topic=codeengine-add-registry). If you refer to a Git repository access secret (`--git-repo-secret`) to work with source in a private repository and the secret does not exist, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}


## Creating a build configuration that references a Git repository access secret
{: #build-config-gitrepo}

You can create a build configuration that pulls source from a private repository. You must specify the details of your source repository, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.  

**UPDATE Better??**

If your source is located in a private repository, you must specify credentials to access the source. Create a build configuration with settings that include information about where to pull source from the private repository and include the Git repository access secret. While you must specify the details of your source and credentials to access this source, you can optionally specify details about where to output the build image, and optionally use the default values for other build settings, such as build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), or [build size](/docs/codeengine?topic=codeengine-plan-build#build-size). If you don't specify where to output the build image, {{site.data.keyword.codeengineshort}} automatically builds and uploads the image to a {{site.data.keyword.registryshort}} namespace in your account. If you do not have an existing {{site.data.keyword.registryshort}} namespace, {{site.data.keyword.codeengineshort}} automatically creates one for you. 

Does title for this section make sense?  "references a Git repository access secret"??

**End**

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
7. In the **Output** section, enter the details of your container image. Select an existing registry access secret, or click **Create registry access secret** to add a new one. Then, select the namespace, repository, and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build. 

### Creating a build configuration with the CLI (private)
{: #build-config-gitrepo-cli}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

**QUESTION -- I might be confusing myself...   build create requires name, image, source code repository, and **registry** secret... or should this be a repository access secret??

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

This example pulls code from a private repository and so references a Git repository secret. 

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, uses the `buildpacks` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`. 

Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.

In this example, the command uses the default `medium` build size. Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository.   

For example, see the following **`build create`** command.

```txt
ibmcloud ce build create --name helloworld-build-private --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source git@github.com:myprivaterepo/builds.git --context-dir /hello --strategy buildpacks --git-repo-secret myrepo
```
{: pre}

## Create a build configuration that pulls source from a local directory
{: #build-config-local}

You can create a build configuration that pulls source from a local directory by using only the {{site.data.keyword.codeengineshort}} CLI. You must specify the details of your source repository, the [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size), and the container image details to store the container image.


**UPDATE - Thinking this should replace the previous blurb/simplify.**

You can create a build configuration that pulls source from a local directory by using only the {{site.data.keyword.codeengineshort}} CLI. 

**END OF UPDATE**

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. Note that you can only target {{site.data.keyword.registrylong_notm}} for your local builds. You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. The source image is created in the same namespace as your build image.

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then [run a build](#running-a-build) that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

### Creating a build configuration with the CLI (local)
{: #build-config-local-cli}

To create a build configuration that pulls code from a local directory with the CLI, use the **`build create`** command and specify the `build-type` as `local`. This command requires a name, an image, and a registry secret. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 

**UPDATE - THINKING this should replace the previous blurb**
 To create a build configuration that pulls code from a local directory with the CLI, use the **`build create`** command and specify the `build-type` as `local`, a name for the build configuration, and information about the location of your source on your local workstation. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create)

**END OF UPDATE**


{: shortdesc}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).

The following example command creates a build configuration that pulls source from a local directory, puts the image in the `mynamespace` namespace that is defined in `us.icr.io`, and uses the `myregistry` registry access secret that is known to {{site.data.keyword.codeengineshort}}. When you specify `local` as the value for `-build-type`, you can only target {{site.data.keyword.registrylong_notm}} for the output of your local build. 

```txt
ibmcloud ce build create --name build-local-dockerfile --build-type local --image us.icr.io/mynamespace/codeengine-build --registry-secret myregistry --dockerfile Dockerfile --strategy dockerfile 
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

### Creating a build run with the CLI for source from a repository (non-local)
{: #build-run-cli}

To submit a build run from a build configuration with the CLI, use the **`buildrun submit`** command. This command requires the name of a build configuration. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.
{: shortdesc} 

The following example runs a build that is called `helloworld-build-run` and uses the `helloworld-build` build.

```txt
ibmcloud ce buildrun submit --build helloworld-build --name helloworld-build-run 
```
{: pre}

The following example shows the output of the **`buildrun submit`** command.

```txt
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

```txt
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

The following example shows the output of the **`build get`** command.

```txt
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


### Creating a build run with the CLI for source from a local directory (local)
{: #build-run-cli-local}

To submit a build run from a build configuration with the CLI that pulls source from a local directory, use the **`buildrun submit`** command. This command requires the name of a build configuration, and the path to your local source. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.
{: shortdesc} 

The following scenario clones the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external} into a `CodeEngineLocalSample` directory on your local machine.

1. Clone the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external} to a subdirectory that is created on your local machine, such as the `CodeEngineLocalSamples` subdirectory. From this directory, run the `git clone` command; for example,

    ```txt
    git clone https://github.com/IBM/CodeEngine
    ```
    {: pre}

2. Go to the directory where your source code is located on your machine. For example, go to the `CodeEngine` subdirectory as this is the directory where the {{site.data.keyword.codeengineshort}} Samples reside.

3. From the directory where your source code resides, submit the build run. The following example runs a build that is called `buildrun-local-dockerfile`and uses the `build-local-dockerfile` build configuration. The `--source` option specifies the path to the source on the local machine to the `helloworld` sample.

    ```txt
    ibmcloud ce buildrun submit --name buildrun-local-dockerfile --build build-local-dockerfile --source ./helloworld  
    ```
    {: pre}

    The following example shows the output of the **`buildrun submit`** command.

    ```txt
    Getting build 'build-local-dockerfile'
    Packaging files to upload from source path './helloworld' ...
    Submitting build run 'buildrun-local-dockerfile'...
    Run 'ibmcloud ce buildrun get -n buildrun-local-dockerfile' to check the build run status.
    OK 
    ```
    {: screen}

4. Monitor the progress of your build run by using the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. For example, to check the status of the build run from the previous example,

    ```txt
    ibmcloud ce buildrun get --name helloworld-build-run
    ```
    {: pre}

    The following example shows the output of the **`build get`** command.

    ```txt
    Getting build run 'buildrun-local-dockerfile'...
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun events -n buildrun-local-dockerfile' to get the system events of the build run.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun logs -f -n buildrun-local-dockerfile' to follow the logs of the build run.
    OK

    Name:          buildrun-local-dockerfile
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           40s
    Created:       2022-01-19T12:22:33-05:00

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
      Source Image Digest:  sha256:07159930b5abcf94e1a7451ea18490d4ad1162a77c2b987da5b7493fa1f1e49d
    Image Digest:  sha256:04c7be7db438a41040ea24d646314f1c847c191d88fffdbea6f483fc443c2bbe

    Build Name:    build-local-dockerfile
    Source Image:  us.icr.io/mynamespace/codeengine-build-source
    Image:         us.icr.io/mynamespace/codeengine-build
    Timeout:       10m0s
    ```
    {: screen}

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. After the build run is completed, you can see your built image, such as `codeengine-build`, in the {{site.data.keyword.registrylong_notm}} instance. You also see a source image with `-source` appended to the name of your build, such as `codeengine-build-source`. You can delete this source image without impact. 
{: note}

For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Next steps for builds
{: #nextsteps-buildimage}

You can now create an application or job from your container image. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


