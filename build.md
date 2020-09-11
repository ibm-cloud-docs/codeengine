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

## Create a build

Builds provide a template for your container image build. You need to specify the details of your source repository, the strategy and size you decided to use, and the container image details to store the build output.

### Creating a build from the console

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create image build**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository and optionally a source revision. By default, {{site.data.keyword.codeengineshort}} builds the master branch. You can enter any other branch name, tag or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy] that you want to use. If you select **Dockerfile (Kaniko)**, you can also specify an alternate path for your Dockerfile. Select the size of your build under **Runtime resources**. Click **Next** to advance to the last section.
7. In the **Output** section you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

### Creating a build with the CLI
{: #build-create-cli}

Use the `code-engine build create` command to create a build.

If your source code repository is not public, then make sure to provide its URL with the SSH protocol and the `--repo` argument with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) you created for it.

```
ibmcloud ce build create --name BUILD_NAME --source GIT_REPO [--repo REPO_SECRET] --strategy STRATEGY --size SIZE --image PATH_TO_REGISTRY --secret SECRET_NAME
```
{: pre}

For example, to create a build called `helloworld-build` that builds from the public Git repo `https://github.com/IBM/CodeEngine` that uses the Dockerfile strategy with Kaniko and `medium` size where the result is stored to `us.icr.io/mynamespace/codeengine-helloworld` by using the container registry secret stored in `icr-mynamespace`:

```
ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine --strategy kaniko --size medium --image us.icr.io/mynamespace/codeengine-helloworld --secret icr-mynamespace
```
{: pre}

Your build will be validated. Consider checking the status of your build using the `code-engine build get` command.

```
ibmcloud ce build get --name BUILD_NAME
```
{: pre}

For the above sample:

```
ibmcloud ce build get --name helloworld-build
```
{: pre}

A validation failure can be that a secret does not exist.

## Running a build

After you created a build, you can submit a run.

### Running a build from the console

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you created your build.
3. From the project page, click **Image builds**.
4. Find your build in the table, click it to view its details.
5. In the **Configuration** section, you can review the build. You can make corrections if needed.
6. In the **Runs** section, click the **Run** button.
7. You can overwrite the **Image tag** here to create a specific tag for this build run and overwrite the **Timeout**.
8. Submit the build run by clicking **Run**.

The build runs. Monitor its progress in the **Runs** section.

### Creating a build run with the CLI

Use the `code-engine buildrun submit` command to submit a build from a build.

```
ibmcloud ce buildrun submit --name BUILDRUN_NAME --build BUILD_NAME
```
{: pre}

For example, to run a build called `helloworld-build-run` that uses the `helloworld-build` build:

```
ibmcloud ce buildrun submit --name helloworld-build-run --build helloworld-build
```
{: pre}

Your build runs. Monitor its progress using the `code-engine buildrun get` command:

```
ibmcloud ce buildrun get --name BUILDRUN_NAME
```
{: pre}

For the above sample:

```
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

Check the status of the build until it succeeded. If your build fails, then check the [troubleshooting tips](/docs/codeengine?topic=codeengine-kn-troubleshoot-build) to determine and resolve the root cause.

## Use the container image in app or job

Depending on the type of your solution, you can now create an application or job. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).
