---
copyright:
  years: 2020
lastupdated: "2020-09-11"

keywords: code engine, tutorial, application

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Building a container image
{: #build-image}

You can use {{site.data.keyword.codeengineshort}} to build container images that you can deploy as applications or jobs.
{: shortdesc}

Before you begin:

- Prepare your source repository
- Decide which build strategy to use
- Decide on the size of your build
- Set up your container registry

## Prepare your source repository
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository, for example in [GitHub](https://github.com/) or [GitLab](https://gitlab.com). If your source repository is public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories.

## Decide which build strategy to use
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image using two strategies:

- [Dockerfile](https://docs.docker.com/engine/reference/builder/) build using the [Kaniko](https://github.com/GoogleContainerTools/kaniko) tool. To use this strategy, you must add a Dockerfile your source repository that describes the steps to build a container image from your source repository. The Dockerfile may contain steps that copy static files from your sources into the container, for example to host them by a web service, or compile source code written in the language of your choice and add the resulting binary to your container image. 
- [Paketo Buildpacks](https://paketo.io/) inspect your source repository to detect which runtime environment your code is based on and how a container images is built from your sources. Buildpacks make assumptions on the directory structure of your source repositories. You should check the samples provided for you runtime to learn how to structure your source repository correctly. Optionally, you can add a `buildpack.yml` file to your source repository to configure the runtime environment version. The supported runtimes are:

  | Runtime   | Samples | `buildpack.yml` settings  |
  | --------- | ------------------------- | ------- |
  | Go        | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go) | [Go version](https://github.com/paketo-buildpacks/go-dist#buildpackyml-configurations) |
  | Java      | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java) | |
  | Node.js   | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs) | [Node.js version](https://github.com/paketo-buildpacks/node-engine#buildpackyml-configurations) |
  | PHP       | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php) | [PHP version](https://github.com/paketo-buildpacks/php-dist#buildpackyml-configurations) and [web server kind](https://github.com/paketo-buildpacks/php-web/tree/main#build) |
  | .NET Core | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core) | [.NET Core SDK version](https://github.com/paketo-buildpacks/dotnet-core-sdk#buildpackyml-configurations) and [.NET Core Runtime version](https://github.com/paketo-buildpacks/dotnet-core-runtime#buildpackyml-configurations) |

  Consider to always specify the runtime version wherever possible in the `buildpack.yml` file. Specify the runtime ensures that your builds continue to run even if {{site.data.keyword.codeengineshort}} updates to the latest Paketo Buildpacks version including a newer default runtime version.
{: tip}

## Decide on the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large` and `xlarge` size. The size of the build defines how many CPU cores, memory and disk space is assigned to the build. A smaller build is cheaper, but typically also slower due to the lower number of CPU cores than a larger build. Also, the memory and disk requirements of your build might not be satisfiable with small builds.

If you are uncertain about which size to chose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}

## Set up your container registry
{: #build-registry}

The output of your build, the container image, is stored in a container registry. It is then available to run as application or job.

Set up your container registry and provide {{site.data.keyword.codeengineshort}} the necessary access, see [Adding access to a container registry](/docs/codeengine?topic=codeengine-add-registry).

## Create a build definition



Build definitions provide a template for your container image build. You need to specify the details of your source repository, the strategy and size you decided to use, and the container image details to store the build output.

### Creating a build definition from console
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Builds**.
4. Click **Create**. The **Create Build** side panel opens where you enter the details of your build definition.
5. In the **Source** section, enter a name for your build definition, the URL of your source repository and optionally a source revision. By default, {{site.data.keyword.codeengineshort}} builds the master branch. You can enter any other branch name, tag or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy] that you want to use. If you select **Dockerfile (Kaniko)**, you can also specify an alternate path for your Dockerfile. Select the size of your build under **Runtime resources**. Click **Next** to advance to the last section.
7. In the **Output** section you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build definition.

### Creating a build definition with the CLI
{: #build-create-cli}

Use the `code-engine builddef create` command to create a build definition.

```
ibmcloud ce builddef create --name BUILDDEF_NAME --source GIT_REPO --strategy STRATEGY --size SIZE --image PATH_TO_REGISTRY --secret SECRET_NAME
```
{: pre}

For example, to create a build definition file called `kbuild` that builds from the Git repo `https://github.com/zhangtbj/taxi` that uses the Dockerfile strategy with Kaniko and `medium` size where the result is stored to `us.icr.io/kerstenapp/codeengine` by using the container registry secret stored in `ksecretname`:

```
ibmcloud ce builddef create --name kbuild --source https://github.com/zhangtbj/taxi --strategy kaniko --size medium --image us.icr.io/kerstenapp/codeengine --secret ksecretname
```
{: pre}

Your build definition will be validated. Consider checking the status of your build definition using the `code-engine builddef get` command.

```
ibmcloud ce builddef get --name BUILDDEF_NAME
```
{: pre}

For the above sample:

```
ibmcloud ce builddef get --name kbuild
```
{: pre}

A validation failure can be that the secret does not exist.

## Create a build run

After you created a build definition, you can trigger a build run.

### Creating a build run from console

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you created your build definition.
3. From the project page, click **Builds**.
4. Find your build definition in the table, click it to view its details.
5. In the **Configuration** section, you can review the build definition. You can make corrections if needed.
6. In the **Runs** section, click the **Run** button.
7. Confirm your intention by clicking **Run** again.

The build runs. Monitor its progress in the **Runs** section.

### Creating a build run with the CLI

Use the `code-engine build run` command to run a build from a build definition.

```
ibmcloud ce build run --name BUILDRUN_NAME --builddef BUILDDEF_FILE
```
{: pre}

For example, to run a build called `kbuildrun` that uses the `kbuild` build definition:

```
ibmcloud ce build run --name kbuildrun --builddef kbuild
```
{: pre}

Your build runs. Monitor its progress using the `code-engine build get` command:

```
ibmcloud ce build get --name BUILDRUN_NAME
```
{: pre}

For the above sample:

```
ibmcloud ce build get --name kbuildrun
```
{: pre}

Check the status of the build until it succeeded.

## Use the container image in app or job



Depending on the type of your solution, you can now create an application or job. See [Deploying applications](deploy.md) and [Running jobs](deploy-job.md).
