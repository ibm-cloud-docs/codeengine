---

copyright:
  years: 2021
lastupdated: "2021-09-16"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.
{: shortdesc}

{{site.data.keyword.codeenginefull}} pulls source code from a repository, builds it, and then pushes the container image to a registry. You can choose public or private [repositories](/docs/codeengine?topic=codeengine-code-repositories) and [registries](/docs/codeengine?topic=codeengine-add-registry). With {{site.data.keyword.codeengineshort}}, you first set up the option for your build configuration and then you run it. After your build is complete, you can deploy the container images as applications or run them as jobs. Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build).

Note that if you build multiple versions of the same container image, the most current version of the container image is downloaded and used when you run your job or deploy your application.

## Create a build configuration
{: #build-create-config}

The first step is to create a build configuration. You must specify the details of your source repository, the build [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy), and the [build size](/docs/codeengine?topic=codeengine-plan-build#build-size) that you decided to use, and the container image details to store the container image.

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image.  The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

### Creating a build configuration from the console
{: #build-create-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you added your container registry.
3. From the project page, click **Image builds**.
4. Click **Create**. The **Specify build details** side panel opens where you enter the details of your build.
5. In the **Source** section, enter a name for your build, the URL of your source repository, and your code repo access. If your code is in a public repo, use an HTTPS URL and select **Public** for the code repo access. An example of an HTTPS URL is `https://github.com/IBM/CodeEngine`. If your code is in a private repo, use an SSH URL for the code repo URL and either select the name of an existing code repo access or [create a code repo access](/docs/codeengine?topic=codeengine-code-repositories). An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`. Optionally, select a source branch name. By default, {{site.data.keyword.codeengineshort}} builds the `main` branch. You can enter any other branch name, tag, or commit ID. Click **Next** to continue.
6. In the **Strategy** section, select the [strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) that you want to use. If you select **Dockerfile**, you can also specify an alternative path for your Dockerfile. Select the size of your build under **Build resources**. Click **Next** to advance to the last section.
7. In the **Output** section, you enter the details of your container image. Select your registry, or click **Add registry** to add a new one. Then, select the namespace, repository, and tag of the image you want to build. For {{site.data.keyword.registryshort}}, you can select from the existing images, or enter a new repository or tag.
8. Click **Done** to finish the creation of the build.

### Creating a build configuration with the CLI
{: #build-create-cli}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build` that builds from the public Git repo `https://github.com/IBM/CodeEngine`, uses the `dockerfile` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`.

Before you create your build, confirm the branch for your `--source` URL. The default `--commit` option references the `main` branch. Also, if you are using the `--strategy` option with the value of `dockerfile`, then ensure the `--dockerfile` option is correctly set to the name of the `dockerfile`. The default value for the `--strategy` option is `Dockerfile`. 
{: important}

```
ibmcloud ce build create --name helloworld-build --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --commit main --context-dir /hello --strategy dockerfile --size medium
```
{: pre}

**Example output**
```
Creating build helloworld-build...
OK
```
{: screen}

The following table summarizes the options that are used with the **`build create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command.
<table>
<caption><code>build create</code> command components</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components </th>
</thead>
<tbody>
<tr>
<td><code>--name</code></td>
<td>The name of the build. Use a name that is unique within the project. This value is required.
<ul>
<li>The name must begin and end with a lowercase alphanumeric character.</li>
<li>The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).</li>
</ul>
</td>
</tr>
<tr>
<td><code>--image</code></td>
<td>The location of the image registry. The format of the location must be <code>REGISTRY/NAMESPACE/REPOSITORY</code> or <code>REGISTRY/NAMESPACE/REPOSITORY:TAG</code> where <code>TAG</code> is optional. If <code>TAG</code> is not specified, the default is <code>latest</code>. This value is required.</td>
</tr>
<tr>
<td><code>--registry-secret</code></td>
<td>The image registry access secret that is used to access the registry. You can add the image registry access secret by running the <strong><code>registry create</code></strong> command. The image registry access secret is used to authenticate with a private registry. This value is required.</td>
</tr>
<tr>
<td><code>--source</code></td>
<td>The URL of the Git repository that contains your source code; for example, <code>https://github.com/IBM/CodeEngine</code>. </td>
</tr>
<tr>
<td><code>--commit</code></td>
<td>The commit, tag, or branch in the source repository to pull.</td>
</tr>        
<tr>
<td><code>--context-dir</code></td>
<td>The directory in the repository that contains the buildpacks file or the Dockerfile. Specify this value if your buildpacks file or Dockerfile is contained in a subdirectory.</td>
</tr>
<tr>
<td><code>--size</code></td>
<td>The size for the build, which determines the amount of resources used. Valid values are <code>small</code>, <code>medium</code>, <code>large</code>, and <code>xlarge</code>.</td>
</tr>
<tr>
<td><code>--strategy</code></td>
<td>The strategy to use for building the image. Valid values are <code>dockerfile</code> and <code>buildpacks</code>.</td>
</tr>
</tbody></table>

During this process, your build is validated. You can check the status of your build by running the [**`ibmcloud ce build get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. For example, use the following **`build get`** command to check the status of the build configuration from the previous example:

```
ibmcloud ce build get --name helloworld-build
```
{: pre}

**Example output**

```
Getting build 'helloworld-build'
OK

Name:          helloworld-build  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           2d15h
Created:       2021-03-14T14:48:19-05:00  
Status:        Succeeded  

Image:              us.icr.io/mynamespace/codeengine-helloworld
Registry Secret:    myregistry
Build Strategy:     dockerfile-medium
Timeout:            10m0s
Source:             https://github.com/IBM/CodeEngine
Commit:             main
Context Directory:  /hello
Dockerfile:         Dockerfile

Build Runs:
    Name                                  Status     Age
    helloworld-build-run                  Succeeded  2d15h
    helloworld-build-run-210223-15375203  Succeeded  2d15h
    mybuildrun                            Succeeded  2d15h 

```
{: screen}

If you receive a command validation failure, check that your secret exists. If you refer to an image registry access secret (`--registry-secret`) for your image and the secret does not exist, see [Accessing a private container registry](/docs/codeengine?topic=codeengine-add-registry). If you refer to a Git repository access secret (`--git-repo-secret`) to work with source in a private repository and the secret does not exist, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
{: tip}


## Creating a build configuration that references a Git repository access secret
{: #build-config-gitrepo}

To create a build configuration with the CLI, use the **`build create`** command. This command requires a name, an image, a source code repository, and a registry secret and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command. 
{: shortdesc}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).
- [Create a Git repository secret (if your source is private)](/docs/codeengine?topic=codeengine-code-repositories).

This example pulls code from a private repository and so references a Git repository secret. 

If your source code repository is not public, then use the `--source` option to provide the URL with the SSH protocol and use the `--git-repo-secret` option with the name of the [repository access](/docs/codeengine?topic=codeengine-code-repositories) that you created. An example of an SSH URL is `git@github.com:IBM/CodeEngine.git`.

For example, the following **`build create`** command creates a build configuration that is called `helloworld-build-private` that builds from the private Git repo `https://github.com/myprivaterepo/builds`, uses the `buildpacks` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`. 

Because the Git repo provided is private, access requires a Git repo secret. As a result, the `--source` that you specify must use the SSH protocol, such as `git@github.com:myprivaterepo/builds.git`. The value for `--source` must not use the `http` or `https` format. 

```
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

The following example runs a build that is called `helloworld-build-run` and uses the `helloworld-build` build: 

```
ibmcloud ce buildrun submit --build helloworld-build --name helloworld-build-run 
```
{: pre}

**Example output**

```
Submitting build run 'helloworld-build-run'...
Run 'ibmcloud ce buildrun get -n helloworld-build-run' to check the build run status.
OK 
```
{: screen}

The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.

<table>
<caption><code>buildrun submit</code> command components</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>--build</code></td>
<td>The name of the build configuration to use. This value is required.</td>
</tr>
<td><code>--name</code></td>
<td>The name of the build run. Use a name that is unique within the project. 
<ul>
<li>The name must begin and end with a lowercase alphanumeric character.</li>
<li>The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).</li>
</ul>
</td>
</tr>
</tbody></table>

Your build runs begins. Monitor the progress by using the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. 

For example, to check the status of the build run from the previous example:

```
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

**Example output**

```
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


