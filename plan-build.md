---

copyright:
  years: 2025
lastupdated: "2025-07-28"

keywords: build for code engine, planning for code engine, source code building for code engine, source code repositories and code engine, image builds for code engine, container image builds for code engine, build strategy for code engine, build size for code engine, build, build run, source repository, image registry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Planning your build
{: #plan-build}

Before you start building images with {{site.data.keyword.codeenginefull}}, learn about the different options you have for your build.
{: shortdesc}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.


If you have an image build that exists in a container registry and the image was built with a non-Intel based processor, {{site.data.keyword.codeengineshort}} cannot run your container image. {{site.data.keyword.codeengineshort}} uses Intel-based processing. You can build your own image if you use Intel processing (x86 processor).  You can also choose to let {{site.data.keyword.codeengineshort}} handle the build process for you. 
{: important}


{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [Source-to-image CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-s2i).

## Prepare your source location
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository or in an accessible location on your local workstation.
{: shortdesc}

Git repository
:    Store your code in a Git repository, for example in [GitHub](https://github.com/){: external} or [GitLab](https://about.gitlab.com/){: external}. Your code can be at the top level of your repository or in a subdirectory. If your source repository is not public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories).

Local workstation
:    Store your code on your local workstation. When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. The source image is created in the same namespace as your build image. Note that you can target only {{site.data.keyword.registrylong_notm}} for your local builds. 
You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.




## Choose a build strategy
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image by using one of following strategies.

### Dockerfile
{: #build-dockerfile-strat}

[Dockerfile](https://docs.docker.com/reference/dockerfile/){: external} build that uses the [BuildKit](https://github.com/moby/buildkit){: external} tool. To use this strategy, add a Dockerfile to your source repository. This Dockerfile describes the steps that are needed to build a container image from your source repository. The Dockerfile might contain steps that copy static files from your sources into the container to be hosted by a web service, for example. It might compile source code that is written in the language of your choice and add the resulting binary to your container image. For more information about Dockerfile builds, see [Writing a Dockerfile for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-dockerfile).

When you pull an image from Docker Hub to use with apps or jobs in Code Engine, be aware of [Docker rate limits](https://docs.docker.com/docker-hub/usage/){: external} for free plan (unauthenticated) users. You might experience pull limits if you receive a `429` error that indicates you reached your pull rate limit. To [increase rate limits](https://docs.docker.com/docker-hub/usage/){: external}, you can upgrade your account to a Docker `Pro` or `Team` subscription.
{: tip}

### Cloud Native Buildpacks
{: #build-buildpack-strat}

[Cloud Native Buildpack](https://buildpacks.io/){: external} that uses [Paketo](https://paketo.io/){: external} to inspect your source repository and detect which runtime environment that your code is based on and how a container image is built from your sources. Buildpacks make assumptions about the directory structure of your source repositories. For more information about how to structure your source repository correctly, see the samples that are provided for your runtime.

| Runtime   | Version | Samples |
| --------- | ------- | ------- |
| Go        | 1.23.8  | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go){: external}. |
| Java      | 21.0.8  | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java){: external}. |
| Node.js   | 22.17.0 | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs){: external}. |
| PHP       | 8.1.28  | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php){: external}. |
| Python    | 3.10.17  | [Python samples](https://github.com/paketo-buildpacks/samples/tree/main/python){: external}. |
| Ruby      | 3.1.6   | [Ruby samples](https://github.com/paketo-buildpacks/samples/tree/main/ruby){: external}. |
| .NET Core | 9.0.203 (.NET Core SDK), \n 9.0.4 (.NET Core Runtime) | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core){: external}. |
{: caption="Runtime sample files" caption-side="bottom"}


Images that are built using Cloud Native Buildpacks no longer use the neutral timestamp of `Jan, 1st 1980` as their image creation timestamp. The timestamp of the input source is used as the image creation timestamp; for example, the Git commit timestamp of the commit that was used for your build.
{: important}

The version of a specific runtime for a Paketo buildpack might differ between regions for a brief time whenever an updated version of a buildpack is rolled out to the various {{site.data.keyword.cloud_notm}} regions.
{: note}



## Determine the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large`, `xlarge`, and `xxlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build. A smaller build is less expensive, but typically also slower because it uses fewer CPU cores. Also, the memory and disk requirements of your build might cause the build to fail with a smaller size.

| Size | Dockerfile | Buildpacks |
| --------- | -------- | -------- |
| `small` | - **CPU** 0.5 \n - **Memory** 2 GB \n - **Disk** 2 GB | - **CPU** 0.5 \n - **Memory** 2 GB \n - **Disk** 2 GB |
| `medium` | - **CPU** 1 \n - **Memory** 4 GB \n - **Disk** 4 GB | - **CPU** 1 \n - **Memory** 4 GB \n - **Disk** 4 GB |
| `large` | - **CPU** 2 \n - **Memory** 8 GB \n - **Disk** 8 GB | - **CPU** 2 \n - **Memory** 8 GB \n - **Disk** 8 GB |
| `xlarge` | - **CPU** 4 \n - **Memory** 16 GB \n - **Disk** 16 GB | - **CPU** 4 \n - **Memory** 16 GB \n - **Disk** 16 GB |
| `xxlarge` | - **CPU** 12 \n - **Memory** 48 GB \n - **Disk** 48 GB | - **CPU** 12 \n - **Memory** 48 GB \n - **Disk** 48 GB |
{: caption="Build size values." caption-side="bottom"}

If you are uncertain about which size to choose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}




## Choose your container image registry
{: #build-registry}

{{site.data.keyword.codeengineshort}} pulls source code from a Git repository or a local directory, builds it, and then pushes (uploads) the image to a container image registry. 

You can use [repositories for your source](/docs/codeengine?topic=codeengine-code-repositories) and [registries for your container image](/docs/codeengine?topic=codeengine-add-registry) that are public or private. You can also choose to specify registry details with a registry secret for your build output, or you can choose for {{site.data.keyword.codeengineshort}} to take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}} with [automatic access](/docs/codeengine?topic=codeengine-add-registry#types-registryaccesssecrets).

## Choose your build method
{: #build-method}

In the following build options, {{site.data.keyword.codeengineshort}} pulls source code from a Git repository or a local directory, builds the container image, and then pushes (uploads) the container image to a registry. You can choose from public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). If your registry is private, specify registry details with a registry secret for your build output with *user-provided access*. Or, you can choose for {{site.data.keyword.codeengineshort}} to create access to store the image in {{site.data.keyword.registrylong_notm}} for you with *automatic access*. 

### Create build configurations
{: #build-create-config}

In this scenario, {{site.data.keyword.codeengineshort}} create a configuration for your build. 

Creating a build configuration does not create an image, but instead, creates the configuration to build an image. You can create an image from the configuration by running the build. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.

For more information, see the following topics.

- [Create a build configuration that pulls source from public repository](/docs/codeengine?topic=codeengine-build-create-config1).
- [Create a build configuration that pulls source from private repository](/docs/codeengine?topic=codeengine-build-config-gitrepo).
- [Create a build configuration that pulls source from a local directory](/docs/codeengine?topic=codeengine-build-config-local).

After you create your build configuration, you can [run it](/docs/codeengine?topic=codeengine-build-run).

### Create container image with stand-alone build commands
{: #build-create-image-standalone}

To learn about how to build your container image with a single {{site.data.keyword.codeengineshort}} CLI command and create the container image without creating a reusable build configuration, see [Building a container image with stand-alone build commands (CLI)](/docs/codeengine?topic=codeengine-build-standalone).

### Build your code and create your workload
{: #build-code-create-workload}

When you create a workload from local source code, the source code is packed into an archive file and uploaded to a managed namespace within the {{site.data.keyword.registrylong_notm}} instance in your account. The image is also stored in this same namespace. 

To build your code and create your workload with a single operation, see the following topics.

Git repository
:    - [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code)
     - [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code)
     - [Creating function workloads from repository source code](/docs/codeengine?topic=codeengine-fun-create-repo)

Local file
:    - [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code)
     - [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code)
     - [Creating function workloads from local source code](/docs/codeengine?topic=codeengine-fun-create-local)

## Next steps for builds
{: #nextsteps-buildimage}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
