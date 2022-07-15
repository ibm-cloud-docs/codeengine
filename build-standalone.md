---

copyright:
  years: 2022
lastupdated: "2022-07-15"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Building a container image with stand-alone build commands (CLI)
{: #build-standalone}

When your code exists as source in a local file or in a Git repository, {{site.data.keyword.codeengineshort}} provides options for you to build your code as a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}. With the {{site.data.keyword.codeengineshort}} CLI, you can build a container image with a single command. 
{: shortdesc}

{{site.data.keyword.codeengineshort}} offers the flexibility to handle the build process for you whenever you are [deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code), [deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code), or you are [creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code) or [creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code).

However, if you want more control over the build of your container image, {{site.data.keyword.codeengineshort}} gives you the flexibility to build your container image by using one of the following options:

* Use a single CLI command, **`buildrun submit`**, to run one build run. The benefit of this option is that you can obtain your build with a single CLI command; however, the configuration for the build is not preserved.
* Define a build configuration from which you can run multiple build runs. See [Building a container image by using a build configuration](/docs/codeengine?topic=codeengine-build-image). 

After your build is complete and your image exists, you can deploy the container image as an application or create a job that references your image. 

Let's learn about how to build your container image with a single command and not reference a build configuration. In this scenario, {{site.data.keyword.codeenginefull}} pulls source code from a Git repository or a local directory, builds it, and then pushes (uploads) the container image to a registry. You can choose public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). You can choose to specify registry details with a registry access secret for your build output with *user-provided access*. Or, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}} with *automatic access*. 

Consider the following points before you build your container image:

* Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build). You'll also need to verify that you can access the registry. See [Setting up authorities for container registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

* If you build multiple versions of the same container image, the latest version of the container image is downloaded and used when you run your job or deploy your application, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the app or job. 

* Build runs that are submitted with the CLI that do not reference a defined build configuration are not viewable from the console.

* {{site.data.keyword.codeengineshort}} has quotas for build runs within a project. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). 

Build runs that complete are ultimately automatically deleted. When you run a build run with a single CLI command such that it is not based on a build configuration, this build run is deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console. 
{: note}


## Running a single build that pulls source from public repository with the CLI
{: #buildsa-public}

If your source is located in a public repository and you want to use a single command to build and output a container image, then use the **`buildrun submit`** command to create the container image without creating a reusable build configuration. 
{: shortdesc}

For the build output, you can choose *automatic access* and let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}}. For this case, you do not need to specify a registry access secret or the location of the image registry. Or, you can choose *user-provided access* and specify registry details along with a registry access secret to access your built image in the registry.

For a complete listing of options for running a single build, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command. 

### Running a single build with the CLI (with public repo source and automatic access to registry)
{: #buildsa-public-cli-a}

In this *automatic access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your public Git repository source, and uploads the image to {{site.data.keyword.registrylong_notm}} with automatic access by using build options with the **`buildrun submit`** command. In this case, you do not need to specify a registry access secret or the location of the image registry. 

See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. Run a build to build an image from a public Git repo and let {{site.data.keyword.codeengineshort}} automatically store and access the image. For example, the following **`buildrun submit`** command runs a build run that is  called `helloworld-buildrun` that builds from source in the public Git repo `https://github.com/IBM/CodeEngine`. 

    ```txt
    ibmcloud ce buildrun submit --name helloworld-buildrun --source https://github.com/IBM/CodeEngine --context-dir /hello 
    ```
    {: pre}

    * In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. 
    * Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo. 
    * By not specifying the location of the image registry or a registry access secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 
    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option. 

    Example output

    ```txt 
    Submitting build run 'helloworld-buildrun'...
    Creating image 'private.us.icr.io/ce--27fe9-glxo4k7nj7d/buildrun-helloworld-buildrun'...
    Run 'ibmcloud ce buildrun get -n helloworld-buildrun' to check the build run status.
    OK
    ```
    {: screen}

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project.  \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--source` | The URL of the Git repository or the path to the local source that contains your source code; for example, `https://github.com/IBM/CodeEngine`.  |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory.  |
    {: caption="Table 1. Command components" caption-side="bottom"}


2. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name helloworld-buildrun
    ```
    {: pre}

    Example output

    Notice the generated name for the image and that the name of the automatically created registry access secret is of the format, `ce-auto-icr-private-<region>`.

    ```txt
    Getting build 'helloworld-buildrun'
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'ibmcloud ce buildrun events -n helloworld-buildrun' to get the system events of the build run.
    Run 'ibmcloud ce buildrun logs -f -n helloworld-buildrun' to follow the logs of the build run.
    OK

    Name:          helloworld-buildrun  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-06-07T15:30:46-04:00  
    Build Type:    git

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
        Commit Branch:  main
        Commit SHA:     946dd18f6e5a5474336786bc28d7dda93aec49c1
        Commit Author:  COMMIT_AUTHOR
    Image Digest:  sha256:ba3c445a27238040e102c083f76ad8922effcc3a7c4dc97b8472e626d87c11a2

    Image:              private.us.icr.io/ce--6ef04-8aaon2dfwa0/buildrun-helloworld-buildrun
    Registry Secret:    ce-auto-icr-private-us-south
    Build Strategy:     dockerfile-medium
    Timeout:            10m0s
    Source:             https://github.com/IBM/CodeEngine
    Commit:             main
    Context Directory:  /hello
    Dockerfile:         Dockerfile
    ```
    {: screen}

### Running a single build with the CLI (with public repo source and user-provided access to registry)
{: #buildsa-public-cli-b}

In this *user-provided access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your public Git repository source, and then uploads the image to your container registry with the registry access that you provide with a single build command. 


Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).

1. Run a build to build an image from a public Git repo and specify the location of the image registry for the build output with a registry access secret. For example, the following **`buildrun submit`** command runs a build run that is called `helloworld-buildrun2` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, and stores the image to the `us.icr.io/mynamespace/codeengine-helloworld` registry by using the `myregistry` image registry secret to access this registry. 


    ```txt
    ibmcloud ce buildrun submit --name helloworld-buildrun2 --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --context-dir /hello 
    ```
    {: pre}

    * In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. 
    * Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository, which is `main` for this Git repo.
    * If you are using the `--strategy` option with the value of `dockerfile`, then ensure the `--dockerfile` option is correctly set to the name of the `dockerfile`. The default value for the `--strategy` option is `Dockerfile`. 
    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option. 

    Example output

    ```txt 
    Submitting build run 'helloworld-buildrun2'...
    Creating image 'us.icr.io/mynamespace/codeengine-helloworld'...
    Run 'ibmcloud ce buildrun get -n helloworld-buildrun2' to check the build run status.
    OK
    ```
    {: screen}

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--image` | The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. |
    | `--registry-secret` | The image registry access secret that is used to access the registry when you create the container image. Run the **`registry create`** command to create a registry secret. The image registry access secret is used to authenticate with a private registry.  |
    | `--source` | The URL of the Git repository or the path to the local source that contains your source code; for example, `https://github.com/IBM/CodeEngine`.  |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory.  |
    {: caption="Table 2. Command components" caption-side="bottom"}

2. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name helloworld-buildrun2
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'helloworld-buildrun2'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun events -n helloworld-buildrun2' to get the system events of the build run.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun logs -f -n helloworld-buildrun2' to follow the logs of the build run.
    OK

    Name:          helloworld-buildrun2  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-06-07T15:57:43-04:00
    Build Type:    git

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
        Commit Branch:  main
        Commit SHA:     946dd18f6e5a5474336786bc28d7dda93aec49c1
        Commit Author:  COMMIT_AUTHOR
    Image Digest:  sha256:6312ee613efa5bec7baa20c47f607e7f15473947d5675fd7384491bee8023afc

    Image:              us.icr.io/mynamespace/codeengine-helloworld2
    Registry Secret:    myregistry
    Build Strategy:     dockerfile-medium
    Timeout:            10m0s
    Source:             https://github.com/IBM/CodeEngine
    Context Directory:  /hello
    Dockerfile:         Dockerfile
    ```
    {: screen}

If you receive a command validation failure, check that your secret exists. If you refer to an image registry access secret (`--registry-secret`) for your image and the secret does not exist, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}

## Running a single build that pulls source from private repository with the CLI
{: #buildsa-private}

If your source is located in a private repository and you want to use a single command to build and output a container image, then use the **`buildrun submit`** command to create the container image without creating a reusable build configuration. 
{: shortdesc} 

For the build output, you can choose *automatic access* and let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}}. For this case, you do not need to specify a registry access secret or the location of the image registry. Or, you can choose *user-provided access* and specify registry details along with a registry access secret to access your built image in the registry.

For a complete listing of options for running a single build, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command. 


### Running a single build with the CLI (with private repo source and automatic access to registry)
{: #buildsa-private-cli-a}

In this *automatic access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your private repository source, and uploads the image to {{site.data.keyword.registrylong_notm}} with automatic access by using build options with the **`buildrun submit`** command. In this case, you do not need to specify a registry access secret or the location of the image registry. 

See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a Git repository secret to access your source](/docs/codeengine?topic=codeengine-code-repositories).


1. Run a build to build an image from a private repository and let {{site.data.keyword.codeengineshort}} automatically store and access the image. For example, the following **`buildrun submit`** command runs a build run that is called `helloworld-buildrun-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`. 


    ```txt
    ibmcloud ce buildrun submit --name helloworld-buildrun-private --source git@github.com:myprivaterepo/builds.git --context-dir /hello --strategy buildpacks --git-repo-secret myrepo
    ```
    {: pre}

    * This example command uses the `buildpacks` strategy and `medium` build size. 
    * By not specifying the location of the image registry or a registry access secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 
    * Because the source in the specified Git repo is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.
    * Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. 
    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option. 

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--source` | The URL of the Git repository or the path to the local source that contains your source code; for example, `git@github.com:myprivaterepo/builds.git`. |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory.  |
    | `--strategy` | The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`.  |
    | `--git-repo-secret` | The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. Run the **`repo create`** command to create this access secret.  |
    {: caption="Table 3. Command components" caption-side="bottom"}

2. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name helloworld-buildrun-private
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'helloworld-buildrun-private'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'ibmcloud ce buildrun events -n helloworld-buildrun-private' to get the system events of the build run.
    Run 'ibmcloud ce buildrun logs -f -n helloworld-buildrun-private' to follow the logs of the build run.
    OK

    Name:          helloworld-buildrun-private  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-06-08T06:02:36-05:00  
    Build Type:    git  

    Summary:       Succeeded  
    Status:        Succeeded  
    Reason:        All Steps have completed executing   
    Source:          
        Commit Branch:  main  
        Commit SHA:     946dd18f6e5a5474336786bc28d7dda93aec49c1  
        Commit Author:  COMMIT_AUTHOR  
    Image Digest:  sha256:39c4a87bc43102c2ee88562072c57c135b8dcc5cc4a1104e1d782fe3acc5d5b6  
    Image:              private.us.icr.io/ce--e97a8-odof2whblw5/build-helloworld-buildrun-private
    Registry Secret:    ce-auto-icr-private-us-south  
    Build Strategy:     buildpacks-v3-medium
    Timeout:            10m0s
    Source:             git@github.com:myprivaterepo/builds.git  
    Context Directory:  /hello  
    Repo Secret:        myrepo
    ```
    {: screen}


### Running a single build with the CLI (with private repo source and and user-provided access to registry)
{: #buildsa-private-cli-b}

In this *user-provided access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your private repository source with a Git repository secret that you provide, and then uploads the image to your container registry with the registry access that you provide with a single build command.  

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a Git repository secret to access your source](/docs/codeengine?topic=codeengine-code-repositories).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).


1. Run a build to build an image from a private repo and specify the location of the image registry for the build output with a registry access secret. The following example **`buildrun submit`** command runs a build run that is called `helloworld-buildrun-private2` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the `myregistry` image registry secret to access this registry. . 

    ```txt
    ibmcloud ce buildrun submit --name helloworld-buildrun-private2 --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source git@github.com:myprivaterepo/builds.git --context-dir /hello --strategy buildpacks --git-repo-secret myrepo
    ```
    {: pre}

    * This example command uses the `buildpacks` strategy and the default `medium` build size.
    * Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format.
    * Because the branch name of the repository is not specified with the `--commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository.  
    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option. 

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--image` | The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. |
    | `--registry-secret` | The image registry access secret that is used to access the registry when you create the container image. Run the **`registry create`** command to create a registry secret. The image registry access secret is used to authenticate with a private registry.  |
    | `--source` | The URL of the Git repository or the path to the local source that contains your source code; for example, `git@github.com:myprivaterepo/builds.git`.  |
    | `--context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory.  |
    | `--strategy` | The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`.  |
    | `--git-repo-secret` | The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. Run the **`repo create`** command to create this access secret.  |
    {: caption="Table 4. Command components" caption-side="bottom"}

2. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name helloworld-buildrun-private2
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'helloworld-buildrun-private2'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'ibmcloud ce buildrun events -n helloworld-buildrun-private2' to get the system events of the build run.
    Run 'ibmcloud ce buildrun logs -f -n helloworld-buildrun-private2' to follow the logs of the build run.
    OK

    Name:          helloworld-buildrun-private2  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d10h
    Created:       2022-06-08T06:11:05-05:00  
    Build Type:    git  

    Summary:       Succeeded  
    Status:        Succeeded  
    Reason:        All Steps have completed executing  
    Source:          
        Commit Branch:  main  
        Commit SHA:     946dd18f6e5a5474336786bc28d7dda93aec49c1  
        Commit Author:  COMMIT_AUTHOR  
    Image Digest:  sha256:39c4a87bc43102c2ee88562072c57c135b8dcc5cc4a1104e1d782fe3acc5d5b6  

    Image:              us.icr.io/mynamespace/codeengine-helloworld  
    Registry Secret:    myregistry  
    Build Strategy:     buildpacks-v3-medium  
    Timeout:            10m0s  
    Source:             git@github.com:myprivaterepo/builds.git  
    Context Directory:  /hello  
    Repo Secret:        myrepo
    ```
    {: screen}

## Running a single build that pulls source from a local directory
{: #buildsa-local}

If your source is on your local workstation, and you want to use a single command to build and output a container image, then use the **`buildrun submit`** command to create the container image without creating a reusable build configuration. 
{: shortdesc}

For the build output, you can choose *automatic access* and let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}}. For this case, you do not need to specify a registry access secret or the location of the image registry. Or, you can choose *user-provided access* and specify registry details along with a registry access secret to access your built image in the registry.

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. Note that you can only target {{site.data.keyword.registrylong_notm}} for your local builds. The source image is created in the same namespace as your build image.  

You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.

For a complete listing of options for running a single build, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command. 


### Running a single build with the CLI (with local source and automatic access to registry)
{: #buildsa-local-cli-a}

In this *automatic access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your local source, and automatically uploads the image to {{site.data.keyword.registrylong_notm}} with automatic access by using build options with the **`buildrun submit`** command. 

See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}. In this case, you do not need to specify a registry access secret or the location of the image registry. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Before you work with local source, make sure that your source is in an accessible location on your local workstation.  

This example uses the `https://github.com/IBM/CodeEngine` samples; in particular, the `helloworld` sample.

1. Download the `https://github.com/IBM/CodeEngine` sample source to your local workstation with the following command.

    ```txt
    git clone https://github.com/IBM/CodeEngine
    ```
    {: pre}

2. Change to the `CodeEngine\helloworld` directory. 

3. From the `CodeEngine\helloworld` directory, run a build to build an image from the `helloworld` source on your local workstation and let {{site.data.keyword.codeengineshort}} automatically store and access the image. This command automatically builds and pushes the image to a {{site.data.keyword.registryshort}} namespace in your account. If you do not have an existing {{site.data.keyword.registryshort}} namespace, {{site.data.keyword.codeengineshort}} automatically creates one for you. For example, the following **`buildrun submit`** command runs a build run that is called `buildrun-local-dockerfile` that builds from the local source.

    ```txt
    ibmcloud ce buildrun submit --name buildrun-local-dockerfile --source .
    ```
    {: pre}

    The `.` indicates the build source is located in your current working directory. 
    {: note}

    * This example command uses the default `dockerfile` strategy, and the default `medium` build size. 
    * By not specifying the location of the image registry or a registry access secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 
    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option. 

    Example output

    ```txt 
    Packaging files to upload from source path '.'...
    Submitting build run 'buildrun-local-dockerfile'...
    Creating image 'private.us.icr.io/ce--27fe9-glxo4k7nj7d/buildrun-buildrun-local-dockerfile'...
    Run 'ibmcloud ce buildrun get -n buildrun-local-dockerfile' to check the build run status.
    OK
    ```
    {: screen}

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--source` | The path to the local source that contains your source code or the URL of the Git repository; for example, `.`.  |
    {: caption="Table 5. Command components" caption-side="bottom"}

4. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name buildrun-local-dockerfile
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'buildrun-local-dockerfile'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun events -n buildrun-local-dockerfile' to get the system events of the build run.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun logs -f -n buildrun-local-dockerfile' to follow the logs of the build run.
    OK

    Name:          buildrun-local-dockerfile  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-06-07T16:09:34-04:00
    Build Type:    local

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
        Source Image Digest:  sha256:ced7abc34f018941145efb56e9a0c1fca99236653c2a05dd5b8b985928ff5f4f
    Image Digest:  sha256:6459430ff49436494aa5e3103eaac98ad90ea50df88a2e14af6314fe88f3c952

    Image:                   private.us.icr.io/ce--27fe9-glxo4k7nj7d/buildrun-buildrun-local-dockerfile
    Registry Secret:         ce-auto-icr-private-us-south
    Build Strategy:          dockerfile-medium
    Timeout:                 10m0s
    Source Image:            private.us.icr.io/ce--27fe9-glxo4k7nj7d/buildrun-buildrun-local-dockerfile-source
    Source Registry Secret:  ce-auto-icr-private-us-south
    Dockerfile:              Dockerfile
    ```
    {: screen}

    Notice the generated name for the image and that the name of the automatically created registry access secret is of the format, `ce-auto-icr-private-<region>`.

### Running a single build with the CLI (with local source and user-provided access to registry)
{: #buildsa-local-cli-b}

In this *user-provided access* scenario, {{site.data.keyword.codeengineshort}} builds an image from your local source, and then uploads the image to your container registry with the registry access that you provide with the **`buildrun submit`** command. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).

Before you work with local source, make sure that your source is in an accessible location on your local workstation.  

This example uses the `https://github.com/IBM/CodeEngine` samples; in particular, the `helloworld` sample.

1. Download the `https://github.com/IBM/CodeEngine` sample source to your local workstation with the following command.

    ```txt
    git clone https://github.com/IBM/CodeEngine
    ```
    {: pre}

2. Change to the `CodeEngine\helloworld` directory. 

3. From the `CodeEngine\helloworld` directory, run a build run to build an image from the `helloworld` source on your local workstation and specify the location of the image registry for the build output with a registry access secret. This **`buildrun submit`** command automatically builds and pushes the image to the registry that you specify with the `--image` option. Specify the `--registry-secret` option to access your registry. 

    ```txt
    ibmcloud ce buildrun submit --name buildrun-local-dockerfile2 --source . --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry 
    ```
    {: pre}

    The `.` indicates the build source is located in your current working directory. 
    {: note}

    * {{site.data.keyword.codeengineshort}} automatically determines whether your source resides in a repo or on a local workstation, based on the value of the `--source` option.  
    * In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. 

    The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the build run. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase letter. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |  |
    | `--source` | The path to the local source that contains your source code or the URL of the Git repository; for example, `.`.  |
    | `--image` | The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. |
    | `--registry-secret` | The image registry access secret that is used to access the registry when you create the container image. Run the **`registry create`** command to create a registry secret. The image registry access secret is used to authenticate with a private registry.  |
    {: caption="Table 6. Command components" caption-side="bottom"}


4. Use the **`buildrun get`** command to check the status of your build run. 

    ```txt
    ibmcloud ce buildrun get --name buildrun-local-dockerfile2
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'buildrun-local-dockerfile2'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun events -n buildrun-local-dockerfile2' to get the system events of the build run.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun logs -f -n buildrun-local-dockerfile2' to follow the logs of the build run.
    OK

    Name:          buildrun-local-dockerfile2  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-06-07T16:34:42-04:00
    Build Type:    local

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
        Source Image Digest:  sha256:00fb80a8cdc17394ccae564efceb81f48c2cbcbd76afd0fb0b74019352933a63
    Image Digest:  sha256:25bc4bedccc1b34c98ccd92368246df3e61a7cf0cf4915a32f111669b60e2fea

    Image:                   us.icr.io/mynamespace/codeengine-helloworld
    Registry Secret:         myregistry
    Build Strategy:          dockerfile-medium
    Timeout:                 10m0s
    Source Image:            us.icr.io/mynamespace/codeengine-helloworld-source
    Source Registry Secret:  myregistry
    Dockerfile:              Dockerfile
    ```
    {: screen}


## Next steps for builds
{: #nextsteps-buildimage-stand}

Now that you have built a container image from your source, you can now create an application or job that uses your container image. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}





