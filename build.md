---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-11"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine, registry secret, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# Building a container image
{: #build-image}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.
{: shortdesc}

For source code that is located in a Git repository or in a local file, {{site.data.keyword.codeengineshort}} provides options to build your code as a container image or code bundle, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}. 

When you build an image, {{site.data.keyword.codeengineshort}} pulls the source code from either a local file or a Git repository and then stores the code and image in an image registry.

When you build multiple versions of the same container image, the latest version of the container image is downloaded and used when you run your job or deploy your application, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the app or job. 

Review [planning information](/docs/codeengine?topic=codeengine-plan-build). 

In the following build options, {{site.data.keyword.codeengineshort}} pulls source code from a Git repository or a local directory, builds the container image, and then pushes (uploads) the container image to a registry. You can choose from public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). If your registry is private, specify registry details with a registry secret for your build output with *user-provided access*. Or, you can choose for {{site.data.keyword.codeengineshort}} to create access to store the image in {{site.data.keyword.registrylong_notm}} for you with *automatic access*. 

Interested in configuring your project such that all users of the project can store and access images in {{site.data.keyword.registryshort}} without having to manually create registry secrets? With sufficient permissions, you can configure this default registry access on a per location (region) basis. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions. See [Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations). 
{: note}

## Create build configurations
{: #build-create-config}

In this scenario, {{site.data.keyword.codeengineshort}} create a configuration for your build. 

Creating a build configuration does not create an image, but instead, creates the configuration to build an image. You can create an image from the configuration by running the build. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.

## Create container image with stand-alone build commands
{: #build-create-image-standalone}

To learn about how to build your container image with a single {{site.data.keyword.codeengineshort}} CLI command and create the container image without creating a reusable build configuration, see [Building a container image with stand-alone build commands (CLI)](/docs/codeengine?topic=codeengine-build-standalone).

## Build your code and create your workload
{: #build-code-create-workload}



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

You can now create an application or job from your container image. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


