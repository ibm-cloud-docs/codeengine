---

copyright:
  years: 2022
lastupdated: "2022-08-03"

keywords: build for code engine, planning for code engine, source code building for code engine, source code repositories and code engine, image builds for code engine, container image builds for code engine, build strategy for code engine, build size for code engine, build, build run, source repository, image registry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Planning your build
{: #plan-build}

Before you start building images with {{site.data.keyword.codeenginefull}}, learn about the different options you have for your build.
{: shortdesc}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.

{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Source-to-image CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-s2i).

## Prepare your source location
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository or in an accessible location on your local workstation.
{: shortdesc}

Git repository
:    Store your code in a Git repository, for example in [GitHub](https://github.com/){: external} or [GitLab](https://gitlab.com){: external}. Your code can be at the top level of your repository or in a subdirectory. If your source repository is not public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories).

Local workstation
:    Store your code on your local workstation. When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. The source image is created in the same namespace as your build image. Note that you can target only {{site.data.keyword.registrylong_notm}} for your local builds. 
You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.

## Choose a build strategy
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image by using one of following strategies.

### Dockerfile
{: #build-dockerfile-strat}

[Dockerfile](https://docs.docker.com/engine/reference/builder/){: external} build that uses the [BuildKit](https://github.com/moby/buildkit){: external} tool. To use this strategy, add a Dockerfile to your source repository. This Dockerfile describes the steps that are needed to build a container image from your source repository. The Dockerfile might contain steps that copy static files from your sources into the container to be hosted by a web service, for example. It might compile source code that is written in the language of your choice and add the resulting binary to your container image. For more information about Dockerfile builds, see [Writing a Dockerfile for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-dockerfile).

When you pull an image from Docker Hub to use with apps or jobs in Code Engine, be aware of [Docker rate limits](https://docs.docker.com/docker-hub/download-rate-limit){: external} for free plan (anonymous) users. You might experience pull limits if you receive a `429` error that indicates you reached your pull rate limit. To [increase rate limits](https://www.docker.com/increase-rate-limits){: external}, you can upgrade your account to a Docker `Pro` or `Team` subscription.
{: tip}

### Cloud Native Buildpacks
{: #build-buildpack-strat}

[Cloud Native Buildpack](https://buildpacks.io/){: external} that uses [Paketo](https://paketo.io/){: external} to inspect your source repository and detect which runtime environment that your code is based on and how a container image is built from your sources. Buildpacks make assumptions about the directory structure of your source repositories. For more information about how to structure your source repository correctly, see the samples that are provided for your runtime.

| Runtime   | Version | Samples |
| --------- | ------- | ------- |
| Go        | 1.17.12  | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go){: external}. |
| Java      | 11.0.16  | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java){: external}. |
| Node.js   | 16.16.0 | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs){: external}. |
| PHP       | 8.0.20  | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php){: external}. |
| Python    | 3.9.13  | [Python samples](https://github.com/paketo-buildpacks/samples/tree/main/python){: external}. |
| Ruby      | 2.7.6   | [Ruby samples](https://github.com/paketo-buildpacks/samples/tree/main/ruby){: external}. |
| .NET Core | 6.0.302 (.NET Core SDK), \n 6.0.7 (.NET Core Runtime) | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core){: external}. |
{: caption="Runtime sample files" caption-side="top"}




## Determine the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large`, and `xlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build. A smaller build is less expensive, but typically also slower because it uses fewer CPU cores. Also, the memory and disk requirements of your build might cause the build to fail with a smaller size.

| Size | Dockerfile | Buildpacks |
| --------- | -------- | -------- |
| `small` | - **CPU** 0.5 \n - **Memory** 2 GB \n - **Disk** 2 GB | - **CPU** 0.5 \n - **Memory** 2 GB \n - **Disk** 2 GB |
| `medium` | - **CPU** 1 \n - **Memory** 4 GB \n - **Disk** 4 GB | - **CPU** 1 \n - **Memory** 4 GB \n - **Disk** 4 GB |
| `large` | - **CPU** 2 \n - **Memory** 8 GB \n - **Disk** 8 GB | - **CPU** 2 \n - **Memory** 8 GB \n - **Disk** 8 GB |
| `xlarge` | - **CPU** 4 \n - **Memory** 16 GB \n - **Disk** 16 GB | - **CPU** 4 \n - **Memory** 16 GB \n - **Disk** 16 GB |
{: caption="Build size values." caption-side="top"}

If you are uncertain about which size to choose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}


## Building with a single CLI build command or a reusable build configuration
{: #build-config-or-single}

When your code exists as source in a local file or in a Git repository, {{site.data.keyword.codeengineshort}} provides options for you to build your code as a container images. {{site.data.keyword.codeengineshort}} gives you the flexibility to build your container image by using one of the following options:

* Use a single CLI command, **`buildrun submit`**, to run one build run. The benefit of this option is that you can obtain your build with a single CLI command; however, the configuration for the build is not preserved. See [Building a container image with stand-alone build commands (CLI)](/docs/codeengine?topic=codeengine-build-standalone). 
* Define a build configuration from which you can run multiple build runs. See [Building a container image by using a build configuration](/docs/codeengine?topic=codeengine-build-image). 

Both of these options apply for cases where you have [repositories for your source](/docs/codeengine?topic=codeengine-code-repositories) and [registries for your container image](/docs/codeengine?topic=codeengine-add-registry) that are public or private. Also, these options apply for cases where you choose to specify registry details with a registry access secret for your build output, or you choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}} with automatic access. 


## Choose your container image registry
{: #build-registry}

{{site.data.keyword.codeengineshort}} pulls source code from a Git repository or a local directory, builds it, and then pushes (uploads) the image to a container image registry. 

You can use [repositories for your source](/docs/codeengine?topic=codeengine-code-repositories) and [registries for your container image](/docs/codeengine?topic=codeengine-add-registry) that are public or private. You can also choose to specify registry details with a registry access secret for your build output, or you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}} with automatic access.

## Next steps for builds
{: #nextsteps-planbuild}

When your planning is complete, [build your container image](/docs/codeengine?topic=codeengine-build-image).


