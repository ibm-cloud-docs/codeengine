---

copyright:
  years: 2020
lastupdated: "2020-12-15"

keywords: code engine, troubleshooting for code engine

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


# Troubleshooting tips for builds 
{: #troubleshoot-build}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} builds.
{: shortdesc}

## Why is my build failing?
{: #ts-build-fail}
{: troubleshoot}

{: tsSymptoms}
After you create and run a build, your build does not complete successfully. 

{: tsCauses}
There are several reasons why your build did not complete. 

1. The build is not registered correctly and a secret does not exist. You receive a similar error message: `The Build is not registered correctly, build: <BUILD_NAME>, registered status: False, reason: secret <SECRET_NAME> does not exist.`

2. The build is not registered correctly and a `clusterBuildStrategy` does not exist. You  receive a similar error message: `The Build is not registered correctly, build: <BUILD_NAME>, registered status: False, reason: clusterBuildStrategy kaniko-xsmall does not exist.`

3. The Git source step fails. You receive a similar error message: `"step-git-source-source-hnv7s" exited with code 1 (image: "icr.io/obs/codeengine/tekton-pipeline/git-init-4874978a9786b6625dd8b6ef2a21aa70@sha256:2d9b1e88d586b7230bc0e4d9dca12045d2159571fc242e26d57a82af22e7b0ae"); for logs run: kubectl -n <PROJECT_NAMESPACE> logs <BUILDRUN_NAME>-865rg-pod-m5lrs -c step-git-source-source-hnv7s.`

4. The ephemeral storage limit is reached. You receive a similar error message: `Pod ephemeral local storage usage exceeds the total limit of containers 1Gi.`

5. The memory limit is reached. The error message that you receive includes `Status reason: OOMKilled`.

6. The build and push step fails.  You receive a similar error message: `Status reason: "step-build-and-push" exited with code 1 (image: "icr.io/obs/codeengine/kaniko/executor@sha256:d60705cb55460f32cee586570d7b14a0e8a5f23030a0532230aaf707ad05cecd"); for logs run: kubectl -n <PROJECT_NAMESPACE> logs <BUILDRUN_NAME>-dgk78-pod-4hs6r -c step-build-and-push.`

{: tsResolve}
Try one of these solutions.

**Before you begin**

Take the following steps to help you troubleshoot the problem with your build.

*   Whether you are running the build in the console or in the CLI, use the CLI for troubleshooting. 
    1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command.  
    2. Review the `Reason` in the command output. 

*   Some build issues use the `kubectl` command-line tool for troubleshooting and resolution. This tool is installed as part of the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started) installation.  Run the `ibmcloud ce project current` command to determine your current project. The output of this command also provides information about how to set up `kubectl` to connect to a {{site.data.keyword.codeengineshort}} project.      

### 1. The build is not registered correctly and a secret does not exist
{: #ts-build-notreg-nosecret}

If you receive a message that the build is not registered correctly and a secret does not exist, then the `BUILD_NAME` was not correctly defined. 

**Example error message** 

```
The Build is not registered correctly, build: <BUILD_NAME>, registered status: False, reason: secret <SECRET_NAME> does not exist.
```
{: screen}

The `BUILD_NAME` build references a secret that does not exist. The secret can be an image registry access secret or a Git repository access secret. Correct the build to reference existing secrets. 

1. Check your secrets. In a build, secrets are used for the following purposes:
    * To authenticate at the container registry. To list existing registry access secrets, run the [`ibmcloud ce registry list`](/docs/codeengine?topic=codeengine-cli#cli-registry-list) command. To create a registry access secret, run the [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command. For more information about registry access secrets, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).
    * To authenticate at a private source code repository. To list existing repository access secrets, run the [`ibmcloud ce repo list`](/docs/codeengine?topic=codeengine-cli#cli-repo-list) command.  To create a repository access secret, run the [`ibmcloud ce repo create`](/docs/codeengine?topic=codeengine-cli#cli-repo-create) command. For more information about repository access secrets, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

2. After secrets are defined, use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration. If you are referencing an image registry access secret, specify the name of the secret by using the `--registry-secret` option with the `build update` command. If you are referencing a Git repository access secret to access a private repository that contains the source code to build your container image, specify the `--git-repo-secret` option with the `build update` command. For example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> [--registry-secret <REGISTRY_ACCESS_SECRET>] [--git-repo-secret <GIT_REPO_SECRET>] 
    ```
    {: pre}

3. Use the  [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}


### 2. The build is not registered correctly and a `clusterBuildStrategy` does not exist
{: #ts-build-notreg-nobldstrategy}

This problem occurs if you use `kubectl` to create the build. 

**Example error message** 

```
The Build is not registered correctly, build: <BUILD_NAME>, registered status: False, reason: clusterBuildStrategy kaniko-xsmall does not exist.
```
{: screen}

The {{site.data.keyword.codeengineshort}} supports the following build strategies in the CLI and console:

* `buildpacks-v3-small`
* `buildpacks-v3-medium`
* `buildpacks-v3-large`
* `buildpacks-v3-xlarge`
* `kaniko-small`
* `kaniko-medium`
* `kaniko-large`
* `kaniko-xlarge`

To resolve this problem with `kubectl`, use the `$ kubectl edit build <BUILD_NAME>` command. In your system editor, specify a valid build strategy on the path `spec.strategy.name`. Save and close this file and use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. 

### 3. Git source step fails  
{: #ts-build-gitsource-stepfail}

To determine the root cause, check the logs of the step that performs the Git clone operation. 

**Example error message** 

```
step-git-source-source-hnv7s" exited with code 1 (image: "icr.io/obs/codeengine/tekton-pipeline/git-init-4874978a9786b6625dd8b6ef2a21aa70@sha256:2d9b1e88d586b7230bc0e4d9dca12045d2159571fc242e26d57a82af22e7b0ae"); for logs run: kubectl -n <PROJECT_NAMESPACE> logs <BUILDRUN_NAME>-865rg-pod-m5lrs -c step-git-source-source-hnv7s
```
{: screen}

Run the [`ibmcloud ce buildrun logs`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs)` command. Focus on the those logs for the failed step,

```
ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: pre}

```
[...]

<BUILDRUN_NAME>-865rg-pod-m5lrs/step-git-source-source-hnv7s:

{"level":"error","ts":1598000672.677071,"caller":"git/git.go:41","msg":"Error running git [fetch --recurse-submodules=yes --depth=1 origin --update-head-ok --force master]: exit status 128\nfatal: could not read Username for 'https://github.com': No such device or address\n","stacktrace":"github.com/tektoncd/pipeline/pkg/git.run\n\tgithub.com/tektoncd/pipeline/pkg/git/git.go:41\ngithub.com/tektoncd/pipeline/pkg/git.Fetch\n\tgithub.com/tektoncd/pipeline/pkg/git/git.go:119\nmain.main\n\tgithub.com/tektoncd/pipeline/cmd/git-init/main.go:52\nruntime.main\n\truntime/proc.go:203"}
{"level":"fatal","ts":1598000672.6772535,"caller":"git-init/main.go:53","msg":"Error fetching git repository: failed to fetch [busybox]: exit status 128","stacktrace":"main.main\n\tgithub.com/tektoncd/pipeline/cmd/git-init/main.go:53\nruntime.main\n\truntime/proc.go:203"}

[...] 
```
{: screen}

Alternatively, if `kubectl` is available, you can run the command from the status reason.

The error text is different based on what went wrong. The following table describes error text and potential root causes for this scenario. 

| Error message contains | Potential root causes | 
| --------- | -------- |
| <code>No such device or address</code> | <ul><li>The repository does not exist.</li><li>The source URL was provided by using HTTPS protocol, but the repository is private and therefore requires the SSH protocol. The wrong protocol was used.</li></ul>|
| <code>Host key verification failed</code>  | <ul><li>The source URL was provided by using SSH protocol, but no secret was provided. The wrong protocol was used or a secret is missing or incorrect.</li></ul> |
| <code>Couldn't find remote ref</code> | <ul><li>The revision (branch name, tag name, commit ID) specified in the build does not exist.</li></ul> |
{: caption="Error text and root cases for Git source failed step."}

<br />

#### Resolution for a non-existent repository
{: #ts-build-noexistrepo}

Use the following commands to update the existing build 
to reference your Git repository source and submit the build run.

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration; for example:  

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> 
    ```
    {: pre}
     
2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

#### Resolution for a wrong protocol or missing secret
{: #ts-build-wrongprotocol}

The URL to a Git repository can be specified by using either the HTTPS or SSH protocol. GitHub and GitLab provide a way to toggle the URL format in the Git UI. The HTTPS protocol requires no authentication but can be used only if the repository is public. For private repositories, you must use the SSH protocol and provide a secret for the repository. Repositories in a GitHub Enterprise setup can be public but still require authentication (such as repositories in `github.ibm.com`), and those GitHub Enterprise repositories can also be used only by using SSH protocol.

**For public repositories**
<br>
If the failure happened for a public repository, then update the existing build to use the HTTPS URL of the Git repository, and run the build. 

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the HTTPS URL of the Git repository; for example:

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> 
    ```
    {: pre}
     
2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

**For private repositories**
<br>
If the failure happened for a private repository, then create a Git repository access secret and use the SSH protocol. 

1. To create a repository access secret, run the following command. The `SSH_KEY_PATH` needs to point to the private key file that matches the public key in your account or the deployment key in the repository. The `GIT_REPO_HOST` is the host of your Git repository, for example `github.com` or `gitlab.com`. For more information, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). 

    ```
    ibmcloud ce repo create --name <GIT_REPO_SECRET> --key-path <SSH_KEY_PATH> --host <GIT_REPO_HOST>
    ```
    {: pre}

2. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the SSH URL of the Git repository and reference the Git repository access secret. For example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> --git-repo-secret <GIT_REPO_SECRET>
    ```
    {: pre}

#### Resolution for a wrong revision
{: #ts-build-wrongrevision}

A build configuration specifies the source repository by using its URL and optionally a revision. The revision can be either the name of a branch or tag, or a commit identifier. By default, the master branch is built. Review the error message for information about something that was specified but does not exist. 

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use a correct revision; for example: 

    ```
    ibmcloud ce build update --name <BUILD_NAME> --revision <REVISION> 
    ```
    {: pre}

2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

### 4. Ephemeral storage limit reached
{: #ts-build-ephemeral-limit} 

When a build runs, it needs to load the source code. When you use a Docker build, the base image needs to be downloaded and the necessary steps to build the target image need to be performed. The build run needs disk space for these steps, which is released once the build run is finished. This disk space is called *ephemeral* local storage. Depending on whether you choose a `small`, `medium`, `large`, or `xlarge` size for your build, a maximum amount of ephemeral storage is available to a build run. When the maximum ephemeral storage is reached, the build run is terminated with an error message; for example: 

**Example error message** 

```
Pod ephemeral local storage usage exceeds the total limit of containers 1Gi.
```
{: screen}

To resolve this problem, use a larger size for the build. 

A larger build size also means that more memory and CPU cores are assigned to the build runs. Increasing this size will probably speed up the build runs, but also increases their cost.
{: important}

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use a larger size; for example: 

    ```
    ibmcloud ce build update --name <BUILD_NAME> --size <SIZE>
    ```
    {: pre}
     

2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

### 5. Memory limit reached
{: #ts-build-memory-limit}

When a build runs, it is running steps, which include code compilations or container image packaging. These steps require memory. Depending on whether you choose a `small`, `medium`, `large`, or `xlarge` size for your build, a maximum amount of memory is available to a build run. When the maximum memory is reached, the build run is terminated with an error message; for example: 

**Example error message** 

```
Status reason: OOMKilled
```
{: screen}

To resolve this problem, use a larger size for the build. 

A larger build size also means that more memory and CPU cores are assigned to the build runs. Increasing this size will probably speed up the build runs, but also increases their cost. 
{: important}

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use a larger size; for example: 

    ```
    ibmcloud ce build update --name <BUILD_NAME> --size <SIZE>
    ```
    {: pre}
     

2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

### 6. Build and push step fails
{: #ts-build-bldpush-stepfail}

The build and push step is the main step of a {{site.data.keyword.codeenginefull_notm}} build. In this step, depending on if you chose the Docker build using Kaniko or the Buildpacks build strategy, one of the following happens,

- Kaniko analyses the customers Dockerfile, performs the steps described there to create a container image and pushes it.

- Buildpacks check the files in the source directory to determine which kind of build is requested. For example, if the source directory contains a `pom.xml`, Buildpacks assumes a Maven type and runs a `mvn -Dmaven.test.skip=true` package build. If it finds a `package.json` file, it assumes that the build is for a Node.js application and runs `npm install`. The result is packaged into an image along with the required runtime environment and pushed to the container registry.

**Example error message** 

```
Status reason: "step-build-and-push" exited with code 1 (image: "icr.io/obs/codeengine/kaniko/executor@sha256:d60705cb55460f32cee586570d7b14a0e8a5f23030a0532230aaf707ad05cecd"); for logs run: kubectl -n <PROJECT_NAMESPACE> logs <BUILDRUN_NAME>-865rg-pod-m5lrs -c step-build-and-push
```
{: screen}

To determine the root cause, check the log of the step. Run the [`ibmcloud ce buildrun logs`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command. Focus on the those logs for the failed step,

```
ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: pre}

Alternatively, if `kubectl` is available, you can run the command from the status reason.

The following table describes error text and potential root causes for this scenario. 

| Error message contains | Strategy | Potential root causes | 
| ------------ | ------- | ------------------ |
| `Killed` | Dockerfile (Kaniko), Buildpacks | <ul><li>The memory limit is reached. </li></ul>|
| `error checking pushed permissions`<br /><br />`ERROR: failed to export: failed to write image to the following tags: [...] UNAUTHORIZED`<br /><br />`ER/ROR: failed to export: failed to write image to the following tags: [...] unsupported status code 401` | Dockerfile (Kaniko)<br /><br />Buildpacks<br /><br />Buildpacks | <ul><li>The container registry secret is not defined.</li><li>The container registry secret is not of the correct type.</li><li>The container registry secret is not for the correct container registry.</li><li>The container registry secret does not allow pushing to the container registry.</li></ul> |
| `Error: error resolving dockerfile path: please provide a valid path to a Dockerfile within the build context` | Dockerfile (Kaniko) | <ul><li>The Dockerfile is not in the root directory of the source repository.</li><li>The source repository does not contain a Dockerfile at all.</li></ul> |
| `DENIED: You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan. For more information, see https://ibm.biz/BdjFwL` | Dockerfile (Kaniko), Buildpacks | <ul><li>{{site.data.keyword.registryfull}} is used and a quota limit is reached.</li></ul> |
| `ERROR: No buildpack groups passed detection.` | Buildpacks | <ul><li>The source of the build was not specified correctly. The typical reason for this error is that the sources are not in the root directory of the Git repository, but rather in a child directory.</li><li>Buildpacks is not supported to build the sources.</li></ul>
| Any other error message | Dockerfile (Kaniko), Buildpacks | <ul><li>There's a problem with the Docker build. </li><li>There is a problem with thesource code</li></ul> |
{: caption="Error text and root cases for build and push steps"}

<br />

#### Resolution for memory limit
{: #ts-build-memorylimit}

1. Use the following command to confirm the memory limit problem:

    ```
    kubectl -n <PROJECT_NAMESPACE> get pod <BUILDRUN_NAME>-865rg-pod-m5lrs -o yaml
    ```
    {: pre}

2. Review the command output. If the output includes `reason: OOMKilled`, then see the [Memory limit reached](#ts-build-memory-limit) for resolution information.   
    
#### Resolution for a container registry problem
{: #ts-build-containerregistryprob} 

In this scenario, a registry access secret does not exist or the secret is not correct. 

1. Determine which secret is used. Use the [`ibmcloud ce build get`](/docs/codeengine?topic=codeengine-cli#cli-build-get) command to display the registry access secret that is used. 

2. Determine whether a `.dockerconfigjson` key exists. Use the [`ibmcloud ce registry get`](/docs/codeengine?topic=codeengine-cli#cli-registry-get) command for the registry access secret. Be aware that the secret data is encoded with base64 and not directly visible; however, the secret contains credentials. In the command output, check the `Data` section. It must contain a key that is called `.dockerconfigjson`. If the `.dockerconfigjson` key is not displayed, then this secret is not suitable to authenticate with a container registry and you need to create a correct secret and reference it in the build. For more information, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

    **Example output**

    ```
    $ ibmcloud code-engine registry get -n <REGISTRY_SECRET>
    Getting image registry access secret <REGISTRY_SECRET>...
    OK
    
    Name:        <REGISTRY_SECRET>
    Project:     <PROJECT_NAME>
    Project ID:  <PROJECT_NAMESPACE>
    Created:     Tue, 18 Aug 2020 21:47:59 +0200
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
    
    * If the image name is `docker.io/aNamespace/aRepository` or `/aNamespace/aRepository` without any host name, then the build is using DockerHub. In this case, the `<REGISTRY>` must be `https://index.docker.io/v1/`. 

    b. Look at the `<USERNAME>` value. If the registry is an {{site.data.keyword.registryfull_notm}}, then an API key must be used for authentication. The `<USERNAME>` needs to be `iamapikey` and the password needs to be an API key. See [Automating access to {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-registry_access) for steps to create the API key.

    c. The credentials need to be validated. {{site.data.keyword.iamlong}} (IAM) allows permissions to be assigned in a fine-grained way. For example, a service ID with access to an {{site.data.keyword.registryfull_notm}} namespace and the permission to pull images, might not be allowed to push images. But, this permission is what is needed in this case. 

5. After you determine the changes that are needed, create a container registry secret that uses corrected values. Use the [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command; for example:   

    ```
    ibmcloud ce registry create --name <REGISTRY_SECRET> --server <REGISTRY_SERVER> --username <USERNAME> --password <PASSWORD>
    ```
    {: pre}

6. Update the build to reference the name of your registry secret.  

    a. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the name of your registry secret; for example: 

    ```
    ibmcloud ce build update --name <BUILD_NAME> --registry-secret <REGISTRY_SECRET>
    ```
    {: pre}
    
    b. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

#### Resolution for Dockerfile not found
{: #ts-build-dockerfile-notfound}  

A Docker build needs a Dockerfile that specifies how the container image is to be built. If the source repository does not contain such a file, then you need to provide this file or consider buildpacks as a build strategy. For more information, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). 

1. If the Dockerfile exists, but has a different name or is not in the root directory, then additional settings need to be specified in the build.

    * If the Dockerfile is not in the root directory of the source repository, then you must specify the `--context-dir` argument and provide the path to the directory that contains the Dockerfile.
    * If the Dockerfile is named something other than `Dockerfile`, then you must specify the `--dockerfile` argument and provide the name of your Dockerfile.

2. Update the build to use the `--context-dir` or `--dockerfile` options as needed. 

    a. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the `--context-dir` or `--dockerfile` options as needed; for example:

    ```
    ibmcloud ce build update --name <BUILD_NAME> [--context-dir <CONTEXT_DIR>] [--dockerfile <DOCKERFILE_NAME>] 
    ```
    {: pre}
        
   b. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

#### Resolution for {{site.data.keyword.registryfull_notm}} quota limit reached 
{: #ts-build-icrquota}

{{site.data.keyword.registryfull_notm}} has two service plans, a free plan and a standard plan.  For the free plan, {{site.data.keyword.registryfull_notm}} applies strict limits, especially on the image size that can be stored in total (500 MB). For the standard plan, you can configure the quotas. For more information, see [About {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-registry_overview).

1. Take one of the following actions: 

    * Delete unused images from the {{site.data.keyword.registryfull_notm}} namespace to increase the available space. 
    * Upgrade from the free plan to the standard plan.
    * Increase the quotas of the {{site.data.keyword.registryfull_notm}} namespace.

    The image URL is included in the error message to help you identify which {{site.data.keyword.registryfull_notm}} namespace is affected.  The namespace can be in a different {{site.data.keyword.cloud_notm}} account than your {{site.data.keyword.codeenginefull_notm}} project. 

2. After you complete the corrective actions, use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

#### Resolution for build source not specified correctly
{: #ts-buildsource-notcorrect} 

The typical reason that this error occurs is that the build source is not located in the root directory of the Git repository, but in a child directory. If the build source does not reside inside the root directory, then specify the location in the build. 

1. Use the [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the `--context-dir` option to specify the path to the source in the Git repository; for example:

    ```
    ibmcloud ce build update --name <BUILD_NAME> --context-dir <CONTEXT_DIR> 
    ```
    {: pre}
        
2. Use the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. Make sure to use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --name <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}


#### Resolution for build source not supported by buildpacks
{: #ts-buildpack-notsupported} 

To check whether your build source repository is supported in {{site.data.keyword.codeengineshort}}, see [Choose a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) for supported runtimes. If your language is listed, check the linked samples and ensure that you correctly structure your sources so that buildpacks can successfully detect and build them. If you cannot find a suitable buildpack for your source or the standardized way on how buildpacks runs the build does not meet your needs, then you can specify a Dockerfile, describe the container build manually in the Dockerfile, and then switch to use the `kaniko` build strategy in the build configuration.

#### Resolution for a problem with the Docker build 
{: #ts-build-dockerbuild}

If the build and push step failure problem isn't a problem with memory, a container registry secret, or a Dockerfile, then the problem is likely with the Docker build. The problem might be an error in the Dockerfile itself, for example a syntax error, or in the correctness of the operation that it performs. The problem can also be in your source code, which might fail to compile, for example, if Java code is included. 

Run a Docker build locally on your machine with the same source to verify that it succeeds.

If the local Docker build succeeds but the same source code does not build in {{site.data.keyword.codeengineshort}}, then the problem might be a security limitation. As with applications and batch jobs, {{site.data.keyword.codeengineshort}} does not allow arbitrary system operations within the {{site.data.keyword.codeengineshort}} cluster. Most of those system operations are not relevant for Docker builds anyway. However, {{site.data.keyword.codeengineshort}} does not allow opening server sockets for privileged ports. The range is `0 to 1023`. For example, if you build a web application and your build includes a test step that brings up a web application server, then you must use ports with higher numbers for this server. 


