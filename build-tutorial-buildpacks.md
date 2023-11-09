---

copyright:
  years: 2023
lastupdated: "2023-11-08"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Building applications by using buildpacks
{: #build-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.
{: shortdesc}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Set up registry access
{: #setup-registry-access}
{: step}

Because the output of the build is an image that is stored in a container registry, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to an image registry for {{site.data.keyword.codeengineshort}}. To store an image in Docker Hub, create the registry access by using the [**`ibmcloud ce secret create --format registry`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. In the following example, use `dockerhub` as the name of the registry access and specify your Docker Hub ID as the username. For the Docker Hub password, you can specify your Docker Hub password or an [access token](/docs/codeengine?topic=codeengine-add-registry#access-private-docker-hub).

```txt
ibmcloud ce secret create --format registry --name dockerhub --server https://index.docker.io/v1/ --username username --password password
```
{: pre}

Example output

```txt
Creating registry secret 'dockerhub'...
OK
```
{: screen}

For more information, see [add registry access documentation](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).

## Create a build
{: #create-a-build}
{: step}

Create a build that contains information about the source code for your app or job. Information can include location and access information for the job or app.

The [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command does not create an image, but creates the configuration to build an image. The [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command references the build configuration to create an image. The options that you specify on the **`build create`** command or **`build update`** command are not validated or used to create an image until the **`buildrun submit`** command executes. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

In the following example, to create the build configuration, use the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. Use `tutorial-build` as the name of the build and specify `https://github.com/IBM/CodeEngine` as the location of the source code and `/s2i-buildpacks` as the context directory folder that contains your source. Use the `dockerhub` registry secret that was created previously for registry access. Specify `buildpacks` as the build strategy to compile the source code and specify `small` as the build size.

```txt
ibmcloud ce build create --name tutorial-build --source https://github.com/IBM/CodeEngine --commit main --context-dir /s2i-buildpacks --registry-secret dockerhub --image docker.io/<your_docker_ID>/tutorial --size small --strategy buildpacks
```
{: pre}

Example output

```txt
Creating build 'tutorial-build'...
OK
```
{: screen}

The `size` option specifies the size for the build, which determines the amount of resources that are used. Valid values are `small`, `medium`, `large`, `xlarge`, and `xxlarge`. The `size` reflects the build requirements for your source code for your app or job. If the build fails due to lack of memory or disk space, or is not fast enough, try switching to a larger size. A larger build size also means that more memory and CPU cores are assigned to the build process. Increasing this size can probably speed up the build process, but this action also increases the cost. For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}

## Submit a build run
{: #submit-buildrun}
{: step}

Now that your build configuration is created, you can run a build based on that build configuration by using the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command. In the following example, reference the `tutorial-build` build configuration and submit the build run. The system generates a unique build run name. You can optionally provide a name for your build run by using the `--name` option, which can be helpful as the name of the build run is required for obtaining build run details. In this example, the system automatically generates the build run name.

```txt
ibmcloud ce buildrun submit --build tutorial-build
```
{: pre}

Example output

```txt
Submitting build run 'tutorial-build-run-851026-090000000'...
Run 'ibmcloud ce buildrun get -n tutorial-build-run-851026-090000000' to check the build run status.
OK
```
{: screen}

To check the status of the build run, use the `buildrun get` [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command to display details of the build run.

```txt
ibmcloud ce buildrun get --name tutorial-build-run-851026-090000000
```
{: pre}

Example output

```txt
Getting build run 'tutorial-build-run-851026-090000000'...
[...]
OK

Name:          tutorial-build-run-851026-090000000
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m42s  
Created:       2021-03-14T14:31:21-05:00  

Summary:  Succeeded  
Status:   Succeeded  
Reason:   Succeeded  
```
{: screen}

The build is complete when the status is `Succeeded`.

If there is a problem with the build run, use the [**`ibmcloud ce buildrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command to display logs about the build run.

```txt
ibmcloud ce buildrun logs --buildrun tutorial-build-run-851026-090000000
```
{: pre}

Example output

```txt
Getting build run 'tutorial-build-run-851026-090000000'...
Getting instances of build run 'tutorial-build-run-851026-090000000'...
Getting logs for build run 'tutorial-build-run-851026-090000000'...
OK

tutorial-build-run-851026-090000000-7vlrw-pod-c9t6g/step-git-source-source-7tbwh:
{"level":"info","ts":1610378702.42616,"caller":"git/git.go:165","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 6b66f2bc3e1277c2e6475608a9c50335712116e0 (grafted,  HEAD, origin/main) in path /workspace/source"}
{"level":"info","ts":1610378703.5453625,"caller":"git/git.go:203","msg":"Successfully initialized and updated submodules in path /workspace/source"}
[...]
```
{: screen}

Your container image is successfully built from source code by using the buildpacks build strategy!

## Work with the container image
{: #use-container-image}
{: step}

Now that your container image is built and the image is pushed to the configured container registry location, you can deploy the image in {{site.data.keyword.codeengineshort}}. For example, you can create a {{site.data.keyword.codeengineshort}} app that uses the created image.

```txt
ibmcloud ce application create --name tutorial-app --image <your_docker_ID>/tutorial
```
{: pre}

Example output

```txt
Creating application 'tutorial-app'...
[...]
```
{: screen}

## Next steps for buildpacks
{: #nextsteps-buildapptut}

For more information, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Does your source code project use Dockerfile? Follow the same steps, but specify the `Dockerfile` build strategy to build an image for your application or job. For more information about Dockerfile, see [Writing a Dockerfile for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-dockerfile).
{: tip}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


