---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-02"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

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
{:terraform: .ph data-hd-interface='terraform'}
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


# Build fails in the build and push step
{: #ts-build-bldpush-stepfail}
{: troubleshoot}

{: tsSymptoms}
After you create and run a build, your build does not complete successfully and you receive a message that the build fails in the build and push step.

{: tsCauses}
The build and push step is the main step of a {{site.data.keyword.codeengineshort}} build. 

- If you chose the Dockerfile build strategy, then Kaniko analyses the Dockerfile, performs the steps that are described there to create a container image, and pushes it.

- If you chose the Buildpacks build strategy, then check the files in the source directory to determine which kind of build is requested. For example, if the source directory contains a `pom.xml`, Buildpacks assumes a Maven type and runs a `mvn -Dmaven.test.skip=true` package build. If it finds a `package.json` file, it assumes that the build is for a Node.js application and runs `npm install`. The result is packaged into an image along with the required runtime environment and pushed to the container registry.

**Example error message** 

```
Summary: Failed to execute build run
Reason:  "step-build-and-push" exited with code 1 (image: "icr.io/obs/codeengine/kaniko/executor@sha256:d60705cb55460f32cee586570d7b14a0e8a5f23030a0532230aaf707ad05cecd"); for logs run: kubectl -n <PROJECT_NAMESPACE> logs <BUILDRUN_NAME>-865rg-pod-m5lrs -c step-build-and-push
```
{: screen}

To determine the root cause, check the log of the step. Run the [**`ibmcloud ce buildrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command. Focus on the logs for the failed step,

```
ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: pre}

The following table describes error text and potential root causes for this scenario. 

| Error message contains | Strategy | Potential root causes | 
| ------------ | ------- | ------------------ |
| `Killed` | Dockerfile (Kaniko), Buildpacks | <ul><li>The memory limit is reached. </li></ul>|
| `error checking pushed permissions`<br /><br /><br />`ERROR: failed to export: failed to write image to the following tags: [...] UNAUTHORIZED`<br /><br />`ERROR: failed to export: failed to write image to the following tags: [...] unsupported status code 401` | Dockerfile (Kaniko)<br /><br />Buildpacks<br /><br /><br /><br />Buildpacks | <ul><li>The container registry secret is not defined.</li><li>The container registry secret is not of the correct type.</li><li>The container registry secret is not for the correct container registry.</li><li>The container registry secret does not allow pushing to the container registry.</li></ul> |
| `Error: error resolving dockerfile path: please provide a valid path to a Dockerfile within the build context` | Dockerfile (Kaniko) | <ul><li>The Dockerfile is not in the root directory of the source repository.</li><li>The source repository does not contain a Dockerfile at all.</li></ul> |
| `DENIED: You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan. For more information, see https://ibm.biz/BdjFwL` | Dockerfile (Kaniko), Buildpacks | <ul><li>{{site.data.keyword.registryfull}} is used and a quota limit is reached.</li></ul> |
| `ERROR: No buildpack groups passed detection.` | Buildpacks | <ul><li>The source of the build was not specified correctly. The typical reason for this error is that the sources are not in the root directory of the Git repository, but rather in a child directory.</li><li>Buildpacks is not supported to build the sources.</li></ul>
| Any other error message | Dockerfile (Kaniko), Buildpacks | <ul><li>There's a problem with the Docker build. </li><li>There's a problem with the source code</li></ul> |
{: caption="Error text and root cases for build and push steps"}

<br />

{: tsResolve}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

After you check the logs and identify potential root causes, use the following resolution actions to help you resolve the problem. 

## Resolution for memory limit during build
{: #ts-build-memorylimit}

See [Build fails when the memory limit is exceeded](/docs/codeengine?topic=codeengine-ts-build-memory-limit) for resolution information.
    
## Resolution for a container registry problem during build
{: #ts-build-containerregistryprob}

In this scenario, a registry access secret does not exist or the secret is not correct.

1. Determine which secret is used. Use the [**`ibmcloud ce build get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command to display the registry access secret that is used.

2. Determine whether a `.dockerconfigjson` key exists. Use the [**`ibmcloud ce registry get`**](/docs/codeengine?topic=codeengine-cli#cli-registry-get) command for the registry access secret. Note that the secret data is encoded with base64 and not directly visible; however, the secret contains credentials. In the command output, check the `Data` section. It must contain a key that is called `.dockerconfigjson`. If the `.dockerconfigjson` key is not displayed, then this secret is not suitable to authenticate with a container registry and you need to create a correct secret and reference it in the build. For more information, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

    **Example output**

    ```
    $ ibmcloud code-engine registry get -n <REGISTRY_SECRET>
    Getting image registry access secret <REGISTRY_SECRET>...
    OK
    
    Name:        <REGISTRY_SECRET>
    ID:          <REGISTRY_SECRET_ID>
    Project:     <PROJECT_NAME>
    Project ID:  <PROJECT_NAMESPACE>
    Age:         8s
    Created:     2021-02-12T10:26:59-06:00 

    Data:
    ---
    .dockerconfigjson: <BASE64_STRING>
    ```
    {: screen}

3. If the `.dockerconfigjson` key exists, then decode the key, which is a base64 encoded string by using the following command,

    ```
    echo "<BASE64_STRING>" | base64 -d
    {"auths":{"<REGISTRY>":{"username":"<USERNAME>","password":"<PASSWORD>","auth":"<AUTH>"}}}
    ```
    {: pre}

    The output of this command typically contains one `<REGISTRY>` key.  

4.  Confirm the following information about the key:

    a. Look at the `<REGISTRY>` value. This value must match the image of the build. 

    * If the image name is on {{site.data.keyword.registryfull_notm}}, for example `us.icr.io/aNamespace/anImage`, then the `<REGISTRY>` needs to be `us.icr.io`. 
    
    * If the image name is `docker.io/aNamespace/aRepository` or `/aNamespace/aRepository` without any hostname, then the build is using DockerHub. In this case, the `<REGISTRY>` must be `https://index.docker.io/v1/`. 

    b. Look at the `<USERNAME>` value. If the registry is an {{site.data.keyword.registryfull_notm}}, then an API key must be used for authentication. The `<USERNAME>` needs to be `iamapikey` and the password needs to be an API key. See [Automating access to {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-registry_access) for steps to create the API key.

    c. The credentials need to be validated. {{site.data.keyword.iamlong}} (IAM) allows permissions to be assigned in a fine-grained way. For example, a service ID with access to an {{site.data.keyword.registryfull_notm}} namespace and the permission to pull images, might not be allowed to push images. But, this permission is what is needed in this case. 

5. After you determine the changes that are needed, create a container registry secret that uses corrected values. Use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command; for example, 

    ```
    ibmcloud ce registry create --name <REGISTRY_SECRET> --server <REGISTRY_SERVER> --username <USERNAME> --password <PASSWORD>
    ```
    {: pre}

6. Update the build to reference the name of your registry secret.  

    a. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the name of your registry secret; for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --registry-secret <REGISTRY_SECRET>
    ```
    {: pre}
    
    b. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

## Resolution for Dockerfile not found during build
{: #ts-build-dockerfile-notfound}  

A Docker build needs a Dockerfile that specifies how the container image is to be built. If the source repository does not contain such a file, then you need to provide this file or consider buildpacks as a build strategy. For more information, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). 

1. If the Dockerfile exists, but has a different name or is not in the root directory, then additional settings need to be specified in the build.

    * If the Dockerfile is not in the root directory of the source repository, then you must specify the `--context-dir` argument and provide the path to the directory that contains the Dockerfile.
    * If the Dockerfile is named something other than `Dockerfile`, then you must specify the `--dockerfile` argument and provide the name of your Dockerfile.

2. Update the build to use the `--context-dir` or `--dockerfile` options as needed. 

    a. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the `--context-dir` or `--dockerfile` options as needed; for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> [--context-dir <CONTEXT_DIR>] [--dockerfile <DOCKERFILE_NAME>] 
    ```
    {: pre}
        
   b. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

## Resolution for {{site.data.keyword.registryfull_notm}} quota limit is reached during build
{: #ts-build-icrquota}

{{site.data.keyword.registryfull_notm}} has two service plans, a free plan and a standard plan. For the free plan, {{site.data.keyword.registryfull_notm}} applies strict limits, especially on the image size that can be stored in total (500 MB). For the standard plan, you can configure the quotas. For more information, see [About {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-registry_overview).

1. Take one of the following actions: 

    * Delete unused images from the {{site.data.keyword.registryfull_notm}} namespace to increase the available space. 
    * Upgrade from the free plan to the standard plan.
    * Increase the quotas of the {{site.data.keyword.registryfull_notm}} namespace.

    The image URL is included in the error message to help you identify which {{site.data.keyword.registryfull_notm}} namespace is affected. The namespace can be in a different {{site.data.keyword.cloud_notm}} account than your {{site.data.keyword.codeenginefull_notm}} project. 

2. After you complete the corrective actions, use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

## Resolution for build source not specified correctly
{: #ts-buildsource-notcorrect} 

The typical reason that this error occurs is that the build source is not located in the root directory of the Git repository, but in a child directory. If the build source does not reside inside the root directory, then specify the location in the build. 

1. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the `--context-dir` option to specify the path to the source in the Git repository; for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --context-dir <CONTEXT_DIR> 
    ```
    {: pre}
        
2. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}


## Resolution for build source not supported by buildpacks
{: #ts-buildpack-notsupported} 

To check whether your build source repository is supported in {{site.data.keyword.codeengineshort}}, see [Choose a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) for supported runtimes. If your language is listed, check the linked samples and ensure that you correctly structure your sources so that buildpacks can successfully detect and build them. If you cannot find a suitable buildpack for your source or the standardized way on how buildpacks runs the build does not meet your needs, then you can specify a Dockerfile, describe the container build manually in the Dockerfile, and then switch to use the `dockerfile` build strategy in the build configuration.

## Resolution for a problem with the Docker build 
{: #ts-build-dockerbuild}

If the build and push step failure problem isn't a problem with memory, a container registry secret, or a Dockerfile, then the problem is likely with the Docker build. The problem might be an error in the Dockerfile itself, for example a syntax error, or in the correctness of the operation that it performs. The problem can also be in your source code, which might fail to compile, for example, if Java&reg; code is included.

If you successfully built your project locally, but the same source code does not build in {{site.data.keyword.codeengineshort}}, then you might have files available locally that are not in your Git repository. For example, for Node.js projects, it is common to run the `npm install` command locally so that project dependencies are downloaded and placed in the `node_modules` directory inside the project directory. It is a good practice to include the `node_modules` directory in the [.gitignore file](https://git-scm.com/docs/gitignore){: external} to keep your Git repository small. A common mistake is to forget to also run `npm install` (or `npm ci`) in the Dockerfile. A Docker build that you run locally can access the local `node_modules` directory, if you copy the whole project into the container, for example, by using the `COPY . /app` command in the Dockerfile. But, the {{site.data.keyword.codeengineshort}} build runs from a freshly checked-out Git repository and cannot access the `node_modules` directory. Therefore, you must run `npm install` (or `npm ci`) in the Dockerfile as part of the build.

A good practice is to include directories like node_modules also in a [.dockerignore file](https://docs.docker.com/engine/reference/builder/#dockerignore-file){: external} so that the Docker build that you run locally behaves the same as the Code Engine build.
{: tip}

Another reason for a project to be successfully built locally but to fail as {{site.data.keyword.codeengineshort}} build are security limitations. As with applications and batch jobs, {{site.data.keyword.codeengineshort}} does not allow arbitrary system operations within the {{site.data.keyword.codeengineshort}} cluster. Most of those system operations are not relevant for Docker builds anyway. However, {{site.data.keyword.codeengineshort}} does not allow opening server sockets for privileged ports. The range is `0 to 1023`. For example, if you build a web application and your build includes a test step that brings up a web application server, then you must use ports with higher numbers for this server.

