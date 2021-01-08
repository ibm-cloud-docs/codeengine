---

copyright:
  years: 2021
lastupdated: "2021-01-08"

keywords: code engine, build, application, job, container, image, configuration, app

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
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
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Building a container image
{: #build-image}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpack.
{: shortdesc}

{{site.data.keyword.codeengineshort}} pulls source code from a repository, build it, and then pushes the container image to a registry. You can choose public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-plan-image). With {{site.data.keyword.codeengineshort}}, you first set up the option for your build configuration and then you run it. After your build is complete, you can deploy the container images as applications or run them as jobs. Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build).

## Create a build configuration
{: #build-create-config}

The first step is to create a build configuration. You must specify the details of your source repository, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.

### Creating a build configuration from the console
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create image build**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and optionally a source revision. By default, {{site.data.keyword.codeengineshort}} builds the master branch. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile (Kaniko)**, you can also specify an alternate path for your Dockerfile. Select the size of your build under **Runtime resources**. Click **Next** to advance to the last section.
7. In the **Output** section, you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository, and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

### Creating a build configuration with the CLI
{: #build-create-cli}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

To create a build configuration with the CLI, use the `code-engine build create` command.

If your source code repository is not public, then provide the URL with the SSH protocol and the `--git-repo-secret` argument with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created.

```
ibmcloud ce build create --name BUILD_NAME --source SOURCE --context-dir DIR --git-repo-secret GIT_REPO_SECRET --image IMAGE_REF --registry-secret REGISTRY_SECRET --size SIZE --strategy STRATEGY
```
{: pre}
<table>
  <caption><code>build create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>build create</code></td>
   <td>The command to create your build configuration.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the build configuration. Use a name that is unique within the project. This value is required.
     <ul>
	   <li>The name must begin with a lowercase letter.</li>
	   <li>The name must end with a lowercase alphanumeric character.</li>
	   <li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   <tr>
   <td><code>--source</code></td>
   <td>The Git repository that contains your source code. </td>
   </tr>        
<tr>
   <td><code>--context-dir</code></td>
   <td>The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpack file or Dockerfile is contained in a subdirectory.</td>
   </tr>
        <tr>
   <td><code>--git-repo-secret</code></td>
   <td>The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command.</td>
   </tr>
        <tr>
   <td><code>--image</code></td>
   <td>The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
        <tr>
   <td><code>--registry-secret</code></td>
   <td>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image.</td>
   </tr>
        <tr>
   <td><code>--size</code></td>
   <td>The size for the build, which determines the amount of resources used. Possible values are `small`, `medium`, `large`, and `xlarge`.</td>
   </tr>
        <tr>
   <td><code>--strategy</code></td>
   <td>The strategy to use for building the image. Valid values are `kaniko` and `buildpacks`. </td>
   </tr>
   </tbody></table>

For example, to create a build configuration that is called `helloworld-build` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, uses the Dockerfile strategy with Kaniko and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the container registry secret stored in `icr-mynamespace`.

```
ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine --context-dir /hello --strategy kaniko --size medium --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret icr-mynamespace
```
{: pre}

**Example output**
```
Creating build helloworld-build...
OK
```
{: screen}

During this process, your build is validated. You can check the status of your build by running the `build get` command.

```
ibmcloud ce build get --name BUILD_NAME
```
{: pre}

For example, to check the status of the build configuration from the previous example.

```
ibmcloud ce build get --name helloworld-build
```
{: pre}

**Example output**

```
Getting build 'helloworld-build'
OK

Name:          helloworld-build  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13  
Age:           7s  
Created:       2020-10-14 10:54:04 -0500 CDT  
Status:        Succeeded  

Image:            us.icr.io/mynamespace/codeengine-helloworld2  
Registry Secret:  myregistry  
Build Strategy:   kaniko-medium  
Timeout:          10m0s  
Source:           https://github.com/IBM/CodeEngine  
Dockerfile:       Dockerfile  
  
```
{: screen}

A command validation failure is that a secret does not exist. See [Accessing a container registry](/docs/codeengine?topic=codeengine-add-registry).
{: tip}

## Running a build
{: #build-run}

After you create a build configuration, you can submit a run based on that build configuration.

### Running a build from the console
{: #build-run-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you created your build.
3. From the project page, click **Image builds**.
4. Select your build configuration.
5. In the **Configuration** section, you can review the build configuration and changes values, if needed.
6. To submit your build, click **Run**.
7. Verify any additional information, such as the **Image tag** to create a specific tag for this build run or overwrite the **Timeout**.
8. Submit the build run by clicking **Run**.

Monitor your build progress in the **Runs** section.

### Creating a build run with the CLI
{: #build-run-cli}

To submit a build run from a build configuration, run the `buildrun submit` command.

```
ibmcloud ce buildrun submit --name BUILDRUN_NAME --build BUILD_NAME
```
{: pre}
<table>
  <caption><code>buildrun submit</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>buildrun submit</code></td>
   <td>The command to run your build configuration.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the build run. Use a name that is unique within the project. This value is required.
     <ul>
	   <li>The name must begin with a lowercase letter.</li>
	   <li>The name must end with a lowercase alphanumeric character.</li>
	   <li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   <tr>
   <td><code>--build</code></td>
   <td>The name of the build configuration that you want to run.</td>
   </tr>
   </tbody></table>

For example, to run a build that is called `helloworld-build-run` that uses the `helloworld-build` build:

```
ibmcloud ce buildrun submit --name helloworld-build-run --build helloworld-build
```
{: pre}

**Example output**

```
Submitting build run 'helloworld-build'...
OK 
```
{: screen}

Your build runs begins. Monitor the progress by using the `buildrun get` command.

```
ibmcloud ce buildrun get --name BUILDRUN_NAME
```
{: pre}

For example, to check the status of the build run from the previous example.

```
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

**Example output**

```
Getting build run 'helloworld-build-run'...
OK

Name:          helloworld-build-run  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13  
Age:           94s  
Created:       2020-10-14 11:42:28 -0500 CDT  
Status:          
  Reason:      Succeeded  
  Registered:  True  

Instances:    
  Name                                  Running  Status     Restarts  Age  
  helloworld-build-run-5a6fg-pod-5jl8k  0/4      Succeeded  0         98s   
```
{: screen}

For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Next steps

You can now create an application or job from your container image. See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads) and [Running jobs](/docs/codeengine?topic=codeengine-job-deploy).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
