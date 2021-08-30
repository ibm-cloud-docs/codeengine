---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-30"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

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


# Running jobs in {{site.data.keyword.codeengineshort}}
{: #job-deploy} 

Learn how to run jobs in {{site.data.keyword.codeenginefull}}. A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.
{: shortdesc}

**Before you begin**

   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
   * Plan a container image for {{site.data.keyword.codeengineshort}} jobs.

{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Batch CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-batch).

## Plan a container image for {{site.data.keyword.codeengineshort}} jobs
{: #deploy-job-containerimage}

To run jobs in {{site.data.keyword.codeengineshort}}, you must first create a container image that has all of the runtime artifacts that your job needs, such as runtime libraries. You can choose from many different ways to create the image, such as using the Docker `docker build` command, but keep in mind the following key things.  
  * Unlike application images, job images do not have an HTTP Server.
  * The executable in the image must exit with a code of zero to be considered successful.
  * Your image can be downloaded from either a public or private image registry. For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).
  
You can build your job from source code by using the [build container images](/docs/codeengine?topic=codeengine-build-image) feature available in {{site.data.keyword.codeengineshort}}.

Note that each time your job runs, the most current version of your referenced container image is downloaded and run. 

## Create a job from a public registry
{: #create-job}

When you create a job, you can specify workload configuration information that is used each time that the job is run. You can create a job from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Creating a job with the console
{: #create-job-ui}

Create a {{site.data.keyword.codeengineshort}} job by using the [`ibmcom/firstjob`](https://hub.docker.com/r/ibmcom/firstjob){: external} image in Docker Hub. This job prints `Hi from a batch job! My index is:`. 

1. Open [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run a container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Specify a container image for your job. For example, specify the sample `docker.io/ibmcom/firstjob` for the container image. If you have your own source code that you want to turn into a container image for the job, see [building a container image](/docs/codeengine?topic=codeengine-build-image).
7. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](#deploy-job-options).
8. Click **Create**.
9. From your job page, in the Job runs pane, click **Submit job** to open the Submit job pane. Note that you might need to scroll to find the Job runs pane. 
10. From the Submit job pane, accept all of the default values, and click **Submit job** again to run your job. 

From the Submit job pane, you can review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. After you submit this job, the system displays the status of the instances of your job on the Job details page. If you specify **Number of instances** instead of **Array indices** in the Submit job pane, from the `Configuration` section of the Job details page, this information is provided as **Array indices**.
{: note}

You can find details about your job run on the Job status page.

### Creating a job with the CLI
{: #create-job-cli}

To create a job configuration with the CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

The following **`job create`** command creates a job configuration that is named `myjob` and uses the container image `ibmcom/firstjob`. 

```
ibmcloud ce job create --name myjob  --image ibmcom/firstjob
```
{: pre}

**Example output**

```
Creating job 'myjob'...
OK
```
{: screen}

The following table summarizes the options that are used with the **`job create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

<table>
  <caption><code>job create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image that is used for runs of the job. This value is required. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `TAG` is not specified, the default is `latest`. For images in [Docker Hub](https://hub.docker.com/), you can specify the image with `NAMESPACE/REPOSITORY`, as the default for `REGISTRY` is `docker.io`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job. Use a name that is unique within the project. This value is required.
     <ul>
	   <li>The name must begin and end with a lowercase alphanumeric character.</li>
	   <li>The name must be 63 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   </tbody></table>

After you create your job, you can submit it. See [Run a job](#run-job).
	
## Create a job from images in {{site.data.keyword.registryshort}}
{: #create-job-crimage}

Create your job configuration that uses an image in {{site.data.keyword.registryshort}}. You can create a job from the console or with the CLI. 
{: shortdesc}

**Before you begin**

- You must have an image in {{site.data.keyword.registryshort}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started). Or, you can [build one from source](#run-job-source-code).
- Verify that you can access the registry. See [Setting up authorities for container registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

### Creating a job that references an image in {{site.data.keyword.registryshort}} with the console
{: #create-job-crimage-console}

Create a job configuration that uses an image in {{site.data.keyword.registryshort}} by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically pull images from {{site.data.keyword.registryshort}} namespaces in your account. To pull images from a different {{site.data.keyword.registryshort}} account or from a private DockerHub account, see [Create a job from images in a private registry](#create-job-private).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Container image** and click **Configure image**. 
7. Select a container registry location, such as `IBM Registry, Dallas`.
8. Select `Automatic` for **Registry access**.
9. Select the namespace and name of the image in the registry for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `hello_repo` in that namespace.
10. Select a value for **Tag**; for example, `latest`.
11. Click **Done**.
12. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](#deploy-job-options).
13. From the Create job page, click **Create**. 
14. Run your job by clicking `Submit job` from Job runs pane. Note that you might need to scroll to find the Job runs pane.

If you want to add registry access before you create a job, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

### Creating a job with an image in {{site.data.keyword.registryshort}} with the CLI
{: #create-job-crimage-cli}

Create a job configuration that uses an image in a {{site.data.keyword.registryshort}} with the CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then create your job configuration.

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key). To create an {{site.data.keyword.cloud_notm}} IAM API key from the CLI, run the [**`iam api-key-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

   ```
   ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
   ```
   {: pre}

   If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
   {: important}

2. After you create your API key, add registry access to {{site.data.keyword.codeengineshort}}. To add access to {{site.data.keyword.registryshort}} with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a {{site.data.keyword.registryshort}} instance called `myregistry`. Note, even though the `--server` and `--username` options are specified in the example command, the default value for the `--server` option is `us.icr.io` and the `--username` option defaults to `iamapikey` when the server is `us.icr.io`. 

   ```
   ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password APIKEY
   ```
   {: pre}

   **Example output**

   ```
   Creating image registry access secret 'myregistry'...
   OK
   ```
   {: screen}

3. Create your job configuration and reference the `hello_repo` image in {{site.data.keyword.registryshort}}. For example, the following **`job create`** command creates the `myhellojob` job to reference the `us.icr.io/mynamespace/hello_repo` by using the `myregistry` access information. 

   ```
   ibmcloud ce job create --name myhellojob --image us.icr.io/mynamespace/hello_repo --registry-secret myregistry
   ```
   {: pre}

   The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
   {: note}

After you create your job, you can submit it. See [Run a job](#run-job).

## Create a job from images in a private registry
{: #create-job-private}

Create your job that uses an image in a private registry such as private Docker Hub. You can create a job from the console or with the CLI. 
{: shortdesc}

**Before you begin**

In order to pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

### Creating a job that references an image in private registry with the console
{: #create-job-private-console}

Create a job configuration that uses an image in a private registry with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private registry, you must first add access to the registry, pull the image, and then create your job configuration.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Container image** and click **Configure image**.
7. Enter `docker.io` for **Registry server**.
8. From **Registry access**, select **Create registry access**.
9. From the Add Registry Access page, choose your registry source. For example, **DockerHub**.
10. Enter a username. For Docker Hub, it is your Docker ID.
11. Enter the password. For Docker Hub, you can use your Docker Hub password or an access token. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.
12. Click **Create** to add the registry access for {{site.data.keyword.codeengineshort}}.
13. From the Select image page, the registry that was added is listed. Select the registry of your image.
14. Select the namespace and name of the image in Docker Hub for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `testjob` in that namespace.
14. Select a value for **Tag**; for example, `latest`.
15. Click **Done**. You selected your image in the registry to reference from your job.
16. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](#deploy-job-options).
17. From the Create job page, click **Create**.
18. After your job is created, the job page for your specific job opens. Run your job by clicking `Submit job` from the Job runs pane. Note that you might need to scroll to find the Job runs pane.

If you want to add registry access before you create a job configuration, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

### Creating a job with an image from a private registry with CLI
{: #create-job-private-cli}

To create a job configuration with an image from a private registry with CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private registry, you must first add access to the registry, pull the image, and then create your job configuration.

1. In order to pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private registry in order to pull images. To add access to a private registry with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a Docker Hub registry called `privatedocker` that is at ``https://index.docker.io/v1/`` and uses your username and password.

   ```
   ibmcloud ce registry create --name privatedocker --server https://index.docker.io/v1/ --username <Docker_User_Name> --password <Password>
   ```
   {: pre}

   **Example output**

   ```
   Creating image registry access secret 'privatedocker'...
   OK
   ```
   {: screen}

3. Create your job configuration and reference the image in your private Docker Hub registry. For example, create the `mytestjob` job configuration to reference the `docker.io/privaterepo/testjob` by using the `privatedocker` access information. 

   ```
   ibmcloud ce job create --name mytestjob --image docker.io/privaterepo/testjob --registry-secret privatedocker
   ```
   {: pre}

The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: note}

## Creating a job from source code
{: #run-job-source-code}

You can create your job from source code. Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
{: shortdesc}

Before you begin, [plan for your build](/docs/codeengine?topic=codeengine-plan-build). You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile). Each time you run the job, the most current version of the dependent build artifacts, including the buildpacks and container image, are used during the build process and are included in the resulting container image.

{{site.data.keyword.codeengineshort}} can automatically push images to {{site.data.keyword.registryshort}} namespaces in your account and even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private DockerHub account, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start from source code**.
3. Select **Job**.
5. Enter a name for the job. Use a name for your job that is unique within the project. 
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select a source repository and Branch name, for example, `https://github.com/IBM/CodeEngine` and `Main`.  Click **Next**.
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Select a container registry location, such as `IBM Registry, Dallas`. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Select your **Registry access**. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `Automatic`.
12. Select a namespace, name, and a tag for your image.
13. Click **Done**.
14. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](#deploy-job-options).
15. Click **Create**.

Need help? Check out [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Run a job
{: #run-job}

After you create your job, you can run a job based on its definition, or you can run the job with overriding properties. Run your job from the console or with the CLI.
{: shortdesc}

Job runs that are created by subscriptions are deleted after 10 minutes. For more information about subscriptions, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events).
{: note}

Each time your job runs, the most current version of your referenced container image is downloaded and run. Submitted batch jobs are run in parallel, if possible. If the number or size of the submitted jobs exceeds the configured quota limits, such as maximum number of running instances, then {{site.data.keyword.codeengineshort}} queues the jobs and delays running them until enough jobs finish. For more information about quotas and limits for jobs, including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
{: note}

### Running a job from the console
{: #run-job-ui}

When you create a job, you can run it immediately. However, you can submit and resubmit a job at any time. You can also submit or resubmit a job that you previously created.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select Projects from the navigation menu.
3. Select a project as the current context. 
4. From the Overview page, select Jobs from the Summary section or select Jobs from the navigation menu.
5. Click the name of your job to open the configuration.
6. Click **Submit job** to open the Submit job dialog. Review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. For more information about these options, see [Options for creating and running a job](#deploy-job-options).
7. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
8. If any of the instances of your job failed to run, click **Rerun failed indices** to run the job again for indices that failed. From the Submit job pane, review and optionally change the configuration values. The **Array indices** field automatically lists the indices of the failed job run instances. After you review and and optionally change configuration values, click **Submit job** to run your job.

You can view job logs after you add logging capabilities. For more information, see [viewing logs](/docs/codeengine?topic=codeengine-view-logs).
{: tip}

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [<img src="images/kube.png" alt="Kubernetes icon"/>Inside {{site.data.keyword.codeengineshort}}: Automatically injecting environment variables](#inside-env-variables).
{: note}

### Running a job with the CLI
{: #run-job-cli}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a job](#create-job-cli).

To run a job with the CLI, use the **`jobrun submit`** command. For a complete listing of options, see the [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command. 

With the CLI, you can [run a job based on a job configuration](#run-job-cli-withjobconfig) or you can [run a job without first creating a job configuration](#run-job-cli-withoutjobconfig). 

#### Running a job with the CLI based on a job configuration 
{: #run-job-cli-withjobconfig}

By creating a job configuration, you can more easily run your job multiple times.

For example, the following **`jobrun submit`** command creates five new instances to run the container image that is specified in the defined `myjob` job configuration. To reference a defined job configuration, use the `--job` option. While the `--name` option is not required if the `--job` option is specified, the following example command specifies the `--name` option to provide a name for this job run. For jobs, the default value for `cpu` is `1` and the default value for `memory` is `4G`. The resource limits and requests are applied per instance, so each instance gets 4 G memory and 1 vCPU. This job allocates 5 \* 4 G = 20 G memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce jobrun submit --name testjobrun --job myjob --array-indices "1 - 5"
```
{: pre}

The following table summarizes the options that are used with the **`jobrun submit`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

<table>
	<caption><code>jobrun submit</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>--name</code></td>
   <td>The name of this job run. The `--name` and the `--image` values are required, if you do not specify the `--job` value. Use a name that is unique within the project.
    <ul>
      <li>  The name must begin and end with a lowercase alphanumeric character.</li>
      <li>  The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
    </ul>
   </td>
   </tr>
   <tr>
   <td><code>--job</code></td>
   <td>The name of the job to be run. This value is required if you do not specify the `--name`  and `--image` values. </td>
   </tr>
   <tr>
   <td><code>--array-indices</code></td>
   <td>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.</td>
   </tr>
   </tbody>
</table>

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [<img src="images/kube.png" alt="Kubernetes icon"/>Inside {{site.data.keyword.codeengineshort}}: Automatically injecting environment variables](#inside-env-variables).
{: note} 

#### Running a job with the CLI without first creating a job configuration 
{: #run-job-cli-withoutjobconfig}

With the CLI, you can submit a job run without first creating a job configuration. You can specify the same configuration options on the `jobrun submit` and `jobrun resubmit` commands that are available with the `job create` command.

For example, the following [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command submits a job run to reference the `us.icr.io/mynamespace/myhello_bld` image by using the `myregistry` access information. Because this job run is not referencing a defined job configuration, you must specify values for the `--name` and `image` options. Use `--name` to specify the name of this job run and use `--image` to provide the name of the image that is used for this job run. The `--array-indices` option creates five new instances to run the container image. For job runs, the default value for `cpu` is `1` and the default value for `memory` is `4G`. The resource limits and requests are applied per instance, so each instance gets 4 G memory and 1 vCPU. This job run allocates 5 \* 4 G = 20 G memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce jobrun submit --name myhellojob-jobruna --image us.icr.io/mynamespace/myhello_bld --registry-secret myregistry   --array-indices "1 - 5"  
```
{: pre}

Run the `jobrun get -n myhellojob-jobrun` command to check the job run status. 

  **Example output**

  ```
  Name:          myapp
  ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
  Project Name:  myproject
  Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
  Age:           3m6s
  Created:       2021-06-04T11:56:22-04:00

  Image:                us.icr.io/mynamespace/myhello_bld
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G
  Registry Secrets:
    myregistry

  Runtime:
    Array Indices:       1 - 5
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          9s
    Instance Statuses:
      Succeeded:  5
    Conditions:
      Type      Status  Last Probe  Last Transition
      Pending   True    16s         16s
      Running   True    13s         13s
      Complete  True    9s          9s

  Events:
    Type    Reason     Age                Source                Messages
    Normal  Updated    11s (x8 over 18s)  batch-job-controller  Updated JobRun "myhellojob-jobruna"
    Normal  Completed  11s                batch-job-controller  JobRun completed successfully

  Instances:
    Name                    Running  Status     Restarts  Age
    myhellojob-jobruna-1-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-2-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-3-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-4-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-5-0  0/1      Succeeded  0         18s
  ```
  {: screen}

Job runs that are submitted (or resubmitted) with the CLI that do not reference a defined job configuration are not viewable from the console. 
{: note}

### Resubmitting your job with the CLI
{: #resubmit-job-cli}

If you want to resubmit a job run based the configuration of a previous job run, use the **`jobrun resubmit`** command. This command requires the name of the previous job run and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command. 
{: shortdesc}

For example, the following **`jobrun resubmit`** command resubmits the `testjobrun` job run. 

```
ibmcloud ce jobrun resubmit --jobrun testjobrun 
```
{: pre}

**Example output**
   
```
Getting job run 'testjobrun'...
Getting job 'myjob'...
Rerunning job run 'myjob-jobrun-fji48'...
Run 'ibmcloud ce jobrun get -n myjob-jobrun-fji48' to check the job run status.
```
{: screen}

For example, the following **`jobrun resubmit`** command resubmits the `myhellojob-jobruna` job run, which was run without first creating the job configuration. Because the referenced job run does not have a related job configuration, you must specify the `--name` option to specify a name this job run. 

```
ibmcloud ce jobrun resubmit --jobrun myhellojob-jobruna --name myhellojob-jobrunb
```
{: pre}

Run the `jobrun get -n myhellojob-jobrunb` command to check the job run status. 

**Example output**
   
```
Getting job run 'testjobrun'...
Getting job 'myjob'...
Rerunning job run 'myjob-jobrun-fji48'...
Run 'ibmcloud ce jobrun get -n myjob-jobrun-fji48' to check the job run status.

  Name:          myapp
  ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
  Project Name:  myproject
  Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
  Age:           3m6s
  Created:       2021-06-04T11:56:22-04:00

  Image:                us.icr.io/mynamespace/myhello_bld
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G
  Registry Secrets:
    myregistry

  Runtime:
    Array Indices:       1 - 5
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          91s
    Instance Statuses:
      Succeeded:  5
    Conditions:
      Type      Status  Last Probe  Last Transition
      Pending   True    96s         96s
      Running   True    92s         92s
      Complete  True    91s         91s

  Events:
    Type    Reason     Age                Source                Messages
    Normal  Updated    93s (x7 over 97s)  batch-job-controller  Updated JobRun "myhellojob-jobrunb"
    Normal  Completed  93s                batch-job-controller  JobRun completed successfully

  Instances:
    Name                    Running  Status     Restarts  Age
    myhellojob-jobrunb-1-0  0/1      Succeeded  0         97s
    myhellojob-jobrunb-2-0  0/1      Succeeded  0         97s
    myhellojob-jobrunb-3-0  0/1      Succeeded  0         97s
    myhellojob-jobrunb-4-0  0/1      Succeeded  0         97s
    myhellojob-jobrunb-5-0  0/1      Succeeded  0         97s
```
{: screen}

Job runs that are submitted (or resubmitted) with the CLI that do not reference a defined job configuration are not viewable from the console. 
{: note}

## Update a job
{: #update-job}

You can make changes to a defined job and run the updated job from the console or with the CLI. Changes to your job might include updating the code container image, code arguments or commands, runtime instance resources, or environment variables.
{: shortdesc}

Each time your job runs, the most current version of your referenced container image is downloaded and run. Submitted batch jobs are run in parallel, if possible. If the number or size of the submitted jobs exceeds the configured quota limits, such as maximum number of running instances, then {{site.data.keyword.codeengineshort}} queues the jobs and delays running them until enough jobs finish. For more information about quotas and limits for jobs, including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
{: note}

### Updating a job from the console
{: #update-job-ui}

When the job is in ready state, you can update the job. Let's update the `myjob` job that you created previously to change the container image from `ibmcom/firstjob` to `ibmcom/testjob` and then subsequently update an environment variable. When a request is sent to this [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob){: external} sample job, the job reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. 

1. Navigate to your job page. 
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
   * From the Jobs page, click the name of the job that you want to update. 

2. To update the image reference of your job, provide the name of your image or configure an image. Update the name of the image for this job from `ibmcom/firstjob` to `ibmcom/testjob`. Click **Save**. 
3. Click **Submit job**.
4. From the Submit job pane, accept all of the default values, and click **Submit job** again to run your job.  
5. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the job is `Hello World!`.
6. To update the job again and add an environment variable, navigate to your job page. 
7. Click **Environment variables** to open the tab and then click **Add**. Add a literal environment variable with the name of `TARGET` with a value of `Sunshine`. The `ibmcom/testjob` outputs the message, `Hello <value_of_TARGET>!>`.
8. Click **Add**.
9. Click **Save** to save the update to the job. 
10. Click **Submit job**.
11. From the Submit job pane, this time change the CPU value to one of the valid CPU choices for the specified memory. Notice that you must use [valid memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). Click **Submit job** again to run this job. The system displays the status of your job on the Job details page. Notice the updated CPU value in the `Configuration` section of the job details.
12. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the updated job is `Hello Sunshine!`.

### Updating a job with the CLI
{: #update-job-cli}

With the CLI, you can update an existing job configuration or specify your changes on a new job run. 

#### Updating a job configuration with the CLI
{: #update-jobconfig-cli}

You can update an existing job configuration with the [**`ibmcloud ce job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command. 

1. Use the **`job update`** command to update the `myjob` job to reference a different image. 

```
ibmcloud ce job update --name myjob --image ibmcom/testjob 
```
{: pre}

Run the `ibmcloud ce job get -n myjob` command to display details of the updated job.

**Example output**

```
Name:          myapp
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m6s
Created:       2021-06-04T11:56:22-04:00

Image:                ibmcom/testjob
Resource Allocation:
  CPU:     1
  Memory:  4G

Runtime:
  Array Indices:       0
  Max Execution Time:  7200
  Retry Limit:         3
```
{: screen}

2. Run the [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command to run a job that references this updated job configuration. For the **`jobrun submit`** command, use the `--job` option to reference a defined job configuration. While the `--name` option is not required if the `--job` option is specified, the following example command specifies the `--name` option to provide a name for this job run. 

```
ibmcloud ce jobrun submit --name myjobrun1 --job myjob
```
{: pre}

3. Run **`ibmcloud ce jobrun get -n myjobrun1`** to view details of this job run. Note that the referenced image is `ibmcom/testjob`, which is based on the updated job configuration.

**Example output**

```
Getting jobrun 'myjobrun1'...
Getting instances of jobrun 'myjobrun1'...
Getting events of jobrun 'myjobrun1'...
OK

Name:          myjobrun1
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m6s
Created:       2021-06-15T11:56:22-04:00

Job Ref:              myjob
Image:                ibmcom/testjob
Resource Allocation:
  CPU:                1
  Ephemeral Storage:  4G
  Memory:             4G

Runtime:
  Array Indices:       0
  Max Execution Time:  7200
  Retry Limit:         3

Status:
  Completed:          11s
  Instance Statuses:
    Succeeded:  1
  Conditions:
    Type      Status  Last Probe  Last Transition
    Pending   True    15s         15s
    Running   True    11s         11s
    Complete  True    11s         11s

Events:
  Type    Reason     Age                Source                Messages
  Normal  Updated    16s (x3 over 20s)  batch-job-controller  Updated JobRun "myjobrun1"
  Normal  Completed  16s                batch-job-controller  JobRun completed successfully

Instances:
  Name           Running  Status     Restarts  Age
  myjobrun1-0-0  0/1      Succeeded  0         20s
```
{: screen}

#### Updating a job run with the CLI  
{: #update-jobrun-cli}

You can specify changes for a job run with the [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command. The **`jobrun submit`** command resubmits a job run that references a previous job run. 

1. Use the **`jobrun resubmit`** command to resubmit the `myjobrun1` job run and change the array indices from `0` to `1-4`. While the `--name` option is not required for the **`jobrun resubmit`** command, the following example command specifies the `--name` option to provide a name for this job run. 

```
ibmcloud ce jobrun resubmit -jobrun myjobrun1 --array-indices "1-4" --name myjobrunresubmit
```
{: pre}

2. Run the `ibmcloud ce jobrun get -n myjobrunresubmit` command to display details of the updated job run. Note that the value of array indices is updated for this job run.

**Example output**

```
Getting jobrun 'myjobrunresubmit'...
Getting instances of jobrun 'myjobrunresubmit'...
Getting events of jobrun 'myjobrunresubmit'...
OK

Name:          myjobrunresubmit2. 
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m6s
Created:       2021-06-04T11:56:22-04:00

Job Ref:              myjob
Image:                ibmcom/testjob
Resource Allocation:
  CPU:                1
  Ephemeral Storage:  4G
  Memory:             4G

Runtime:
  Array Indices:       1-4
  Max Execution Time:  7200
  Retry Limit:         3

Status:
  Completed:          34s
  Instance Statuses:
    Succeeded:  4
  Conditions:
    Type      Status  Last Probe  Last Transition
    Pending   True    38s         38s
    Running   True    36s         36s
    Complete  True    34s         34s

Events:
  Type    Reason     Age                Source                Messages
  Normal  Updated    36s (x7 over 40s)  batch-job-controller  Updated JobRun "myjobrunresubmit"
  Normal  Completed  36s                batch-job-controller  JobRun completed successfully

Instances:
  Name                  Running  Status     Restarts  Age
  myjobrunresubmit-1-0  0/1      Succeeded  0         40s
  myjobrunresubmit-2-0  0/1      Succeeded  0         40s
  myjobrunresubmit-3-0  0/1      Succeeded  0         40s
  myjobrunresubmit-4-0  0/1      Succeeded  0         40s
```
{: screen}

Job runs that are submitted (or resubmitted) with the CLI that do not reference a defined job configuration are not viewable from the console. 
{: note}

## Options for creating and running a job
{: #deploy-job-options}

Learn about the options that you can specify when you create or run your job. Note that options can vary between the console and the CLI.
{: shortdesc}
	
### Memory and CPU for jobs
{: #deploy-job-combo}

When you deploy your job, you can specify the amount of memory and CPU that your job can consume. These amounts can vary, depending on if your job is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

By default, your job is assigned 4 G of memory and 1 vCPU. For more information about selecting memory and CPU, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

### Creating and running a job with commands and arguments
{: #job-cmd-args}

You can define commands and arguments for your job to use at run time when you create or run your job. 
{: shortdesc}

You can add commands and arguments to your job by using the CLI or the console.

To add commands and arguments through the console, use the `Command` and `Arguments` fields.

To add commands and arguments by using the CLI, add the `--cmd` and `--args` options to your [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) or your [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command.

For more information about defining commands and arguments, see [Defining commands and arguments for your Code Engine workloads](/docs/codeengine?topic=codeengine-cmd-args).

### Creating and running a job with environment variables 
{: #job-option-envvar}

You can define and set environment variables as key-value pairs that can be used by your job at run time. 
{: shortdesc}

You can define environment variables when you create your job, or when you update an existing job from the console or with the CLI. You can create environment variables for your jobs that fully reference a configmap (or secret) or reference individual keys in a configmap (or secret). 

For more information about defining environment variables, see [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

### Creating and running a job with secrets and configmaps 
{: #job-option-secconfigmap}

In {{site.data.keyword.codeengineshort}}, secrets and configmaps can be consumed by your job by using environment variables. 
{: shortdesc}

Both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

Your job can use environment variables to fully reference a configmap (or secret) or reference individual keys in a configmap (or secret).

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#configmap-ref).

## Access the job details
{: #access-job-details}

Find details about your job from the console or with the CLI.
{: shortdesc}

### Accessing job details from the console
{: #access-jobdetails-ui}

Job results are available in the console from the job details page after you submit your job. You can also view job details in the console by clicking the name of your job in the Jobs pane on your job page. 

Job details include status of your instances, configuration details, and environment variables of your job.  

### Accessing job details with the CLI
{: #access-jobdetails-cli}

To view details of your job with the CLI, use the **`job get`** command. For a complete listing of options, see the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command. 
{: shortdesc}

For example, the following **`job get`** command displays details about the `myjob` job.

```
ibmcloud ce job get --name myjob
```
{: pre}

**Example output**
   
```
Getting job 'myjob'...
OK

Name:          myjob
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m4s
Created:       2021-02-17T15:41:12-05:00

Image:                ibmcom/firstjob
Resource Allocation:
  CPU:     1
  Memory:  4G
  
Runtime:
  Array Indices:       0
  Max Execution Time:  7200
  Retry Limit:         3
```
{: screen}

### Accessing job details for a specific run of your job with the CLI
{: #access-specific-jobdetails-cli}

To view details of a specific run of your job with the CLI, use the **`jobrun get`** command. For a complete listing of options, see the [**`ibmcloud ce jobrun  get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command. 
{: shortdesc}

For example, the following **`jobrun get`** command displays details about the `testjobrun` job run.

```
ibmcloud ce jobrun get --name testjobrun
```
{: pre}

**Example output**
   
```
Getting jobrun 'testjobrun'...
Getting instances of jobrun 'testjobrun'...
Getting events of jobrun 'testjobrun'...
OK

Name:          testjobrun
ID:            abcdefgh-abcd-abcd-abcd-1d733051eb02
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m44s
Created:       2021-02-09T13:32:25-05:00

Job Ref:              myjob
Image:                ibmcom/firstjob
Resource Allocation:
  CPU:                1
  Ephemeral Storage:  400M
  Memory:             4G

Runtime:
  Array Indices:       1 - 5
  Max Execution Time:  7200
  Retry Limit:         2

Status:
  Completed:          4m
  Instance Statuses:
    Succeeded:  5
  Conditions:
    Type      Status  Last Probe  Last Transition
    Pending   True    4m6s        4m6s
    Running   True    4m3s        4m3s
    Complete  True    4m          4m

Events:
  Type    Reason     Age                  Source                Messages
  Normal  Updated    4m3s (x8 over 4m9s)  batch-job-controller  Updated JobRun "testjobrun"
  Normal  Completed  4m3s                 batch-job-controller  JobRun completed successfully

Instances:
  Name            Running  Status     Restarts  Age
  testjobrun-1-0  0/1      Succeeded  0         4m9s
  testjobrun-2-0  0/1      Succeeded  0         4m9s
  testjobrun-3-0  0/1      Succeeded  0         4m9s
  testjobrun-4-0  0/1      Succeeded  0         4m9s
  testjobrun-5-0  0/1      Succeeded  0         4m9s
```
{: screen}

### Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The job is accepted by the system, but one or more of the instances of the job are not yet created. This status includes time before a job is scheduled and time that is spent downloading images over the network, which might take a while. |
| Running | The job instances are created. At least one instance is still running, or is starting or restarting. |
| Succeeded | All job instances finished successfully and none are restarting. |
| Failed | All job instances finished, and at least one instance ended in failure. That is, the instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the job cannot be obtained, typically due to an error in communicating with the host. |

## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}:  Automatically injected environment variables
{: #inside-env-variables}
	
When you run a job, {{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the job run instance. The following table lists automatically injected environment variables into each instance of your running job. The following examples of automatically injected environment variables are based on a job that is named `myjob`, which references the {{site.data.keyword.codeengineshort}} sample image, `ibmcom/codeengine`.

| Environment variable | Description | Example |
|----------------|---------------------|---------|
| `CE_DOMAIN`    | The domain name of the project.                                           | `CE_DOMAIN=us-south.codeengine.appdomain.cloud` |
| `CE_JOB`       | The name of the defined job configuration that was used for the job run.  | `CE_JOB=myjobdef` |
| `CE_JOBRUN`    | The name of the job run.                                                  | `CE_JOBRUN=myjob-jobrun-f5kxz` |
| `CE_SUBDOMAIN` | The subdomain associated with the project in which your job is running. If you are familiar with Kubernetes, `CE_SUBDOMAIN` maps to the Kubernetes namespace that is associated with your project.                       | `CE_SUBDOMAIN=01234567-abcd` |
| `HOME`         | Your home directory that is running the job.                              | `HOME=/root` |
| `HOSTNAME`     | The name of instance that your app is deployed to.                        | `HOSTNAME=myjob-jobrun-6bgmg-0-0` |
| `JOB_INDEX`    | The index of a specific job run instance.                                 | `JOB_INDEX=1` |
| `PATH`         | The list of directories in which the system looks for executables.        | `PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` |
| `PWD`          | The current working directory.                                            | `PWD=/` |
{: caption="Automatically injected environment variables when deploying {{site.data.keyword.codeengineshort}} jobs"}

Note that each job run instance gets its own index from the array of indices that were specified when the job was created. The `JOB_INDEX` environment variable contains the index value.

While the job itself doesn't have a URL associated with it, the `CE_DOMAIN` and `CE_SUBDOMAIN` values might be useful if you need to reference an applications that is running in the same project. The full external URL of this application is `appName.CE_SUBDOMAIN.CE_DOMAIN`. To reference the private URL of an application, use `appName.CE_SUBDOMAIN`.
