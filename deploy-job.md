---

copyright:
  years: 2021
lastupdated: "2021-01-25"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine

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


# Running jobs in {{site.data.keyword.codeengineshort}}
{: #job-deploy} 

Learn how to run jobs in {{site.data.keyword.codeengineshort}}. A job runs one or more instances of your executable code. Unlike applications, which include an HTTP server to handle incoming requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.
{: shortdesc}

**Before you begin**

   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
   * Plan a container image for {{site.data.keyword.codeengineshort}} jobs.

## Plan a container image for {{site.data.keyword.codeengineshort}} jobs
{: #deploy-job-containerimage}

To run jobs in {{site.data.keyword.codeengineshort}}, you must first create a container image that has all of the runtime artifacts that your job needs, such as runtime libraries. You can choose from many different ways to create the image, such as using the Docker `docker build` command, but keep in mind the following key things.  
  * Unlike application images, job images do not have an HTTP server.
  * The executable in the image must exit with a code of zero to be considered successful.
  * Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).
  
You can build your job from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}.

## Create a job from a public repository
{: #create-job}

When you create a job, you can specify workload configuration information that is used each time that the job is run. You can create a job from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Creating a job with the console
{: #create-job-ui}

Create a {{site.data.keyword.codeengineshort}} job by using the [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob){: external} image in Docker Hub. This job prints `"Hello World"`. 

1. Open [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the job.
6. Specify a container image for your job. For example, specify the sample `docker.io/ibmcom/testjob` for the container image, which is a simple `Hello World` job. For this example, you do not need to modify the default values for environment variables or runtime settings. If you have your own source code that you want to turn into a container image for the job, see [building a container image](/docs/codeengine?topic=codeengine-build-image).
6. Click **Create**.
7. Run your job by clicking **Submit job** from Job runs. Note that you might need to scroll to find the Job runs section.
8. From the Submit job pane, accept all of the default values, and click **Submit job** again to run your job.

You can find details about your job run on the Job status page.

### Creating a job with the CLI
{: #create-job-cli}

To create a job configuration with the CLI, use the `job create` command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [`ibmcloud ce job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

The following example creates a job configuration that is named `testjob` and uses the container image `ibmcom/testjob`. 

```
ibmcloud ce job create --image ibmcom/testjob --name testjob 
```
{: pre}

**Example output**

```
Creating job 'testjob'...
OK
```
{: screen}

The following table summarizes the options that are used with the `job create` command in this example. For the most up-to-date information about the command and its options, see the [`ibmcloud ce job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

<table>
  <caption><code>job create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>job create</code></td>
   <td>The command to create your job.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job. This value is required. For images in [Docker Hub](https://hub.docker.com/), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job. Use a name that is unique within the project. This value is required.
     <ul>
	   <li>The name must begin with a lowercase letter.</li>
	   <li>The name must end with a lowercase alphanumeric character.</li>
	   <li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
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

- You must have an IAM API key for your {{site.data.keyword.registryshort}} instance. If you do not have an IAM API key, [create one](/docs/codeengine?topic=codeengine-add-registry#access-registry-account). 
- You must have an image in {{site.data.keyword.registryshort}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started).

### Creating a job that references an image in {{site.data.keyword.registryshort}} with the console
{: #create-job-crimage-console}

Create a job configuration that uses an image in {{site.data.keyword.registryshort}} by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then create the job configuration. 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the job; for example `myjob`.
6. Select **Container Image** from **Code** and click **Select image**. 
7. To add registry access, click **Edit image details** and then **Add registry**. 
8. From the Add Registry Access page, specify the registry name and registry server.  For example, specify `ibmcregistry1` as the registry name and specify `us.icr.io` as the registry server. 
9. Enter a name. For {{site.data.keyword.registryshort}}, it is `iamapikey`. 
10. Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. 
   a. Create an IAM API key. For more information about creating an IAM API key, see [Creating an IAM API key for a {{site.data.keyword.registryshort}} instance](/docs/codeengine?topic=codeengine-add-registry#access-registry-account).
   b. Add registry access to {{site.data.keyword.codeengineshort}}.  For more information about adding registry access, see [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce). 
11. Click **Add** to add the registry access for {{site.data.keyword.codeengineshort}}.
12. From the Select image page, the registry that was added is listed. Select the registry of your image.
13. Select the namespace and name of the image in the registry for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `testjob` in that namespace.
14. Select a value for **TAG**; for example, `latest`.
15. Click **Done**. You have selected your image in the registry to reference from your job.
16. From the Create job page, click **Create**. 
17. Run your job by clicking `Submit job` from Job runs section. Note that you might need to scroll to find the Job runs section.

If you want to add registry access before you create a job, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce). 

### Creating a job with an image in {{site.data.keyword.registryshort}} from CLI
{: #create-job-crimage-cli}

Create a job configuration that uses an image in a {{site.data.keyword.registryshort}} with the CLI, use the `job create` command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [`ibmcloud ce job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then create your job configuration.

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM key](/docs/codeengine?topic=codeengine-add-registry#access-registry-account). To create an {{site.data.keyword.cloud_notm}} IAM API key from the CLI, run the [`iam api-key-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

   ```
   ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
   ```
   {: pre}

   If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
   {: important}

2. After you create your API key, add registry access to {{site.data.keyword.codeengineshort}}. To add access to {{site.data.keyword.registryshort}} with the CLI, use the [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, create registry access to a {{site.data.keyword.registryshort}} instance called `myregistry` that is at `us.icr.io` that uses the IAM API key:

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

3. Create your job configuration and reference the `hello_repo` image in {{site.data.keyword.registryshort}}. For example, create the `mytestjob` ob to reference the `us.icr.io/mynamespace/hello_repo` by using the `myregistry` access information. 

   ```
   ibmcloud ce job create --name mytestjob --image us.icr.io/mynamespace/testjob --registry-secret myregistry
   ```
   {: pre}

   The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
   {: important}

After you create your job, you can submit it. See [Run a job](#run-job).

## Create a job from images in a private repository
{: #create-job-private}

Create your job that uses an image in a private repository or registry such as private Docker Hub. You can create a job from the console or with the CLI. 
{: shortdesc}

**Before you begin**

In order to pull images from a private repository, you must first create a private repository. For example, to create a private Docker Hub repository, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private repository, [push an image to it](https://docs.docker.com/docker-hub/repos/){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

### Creating a job that references an image in private repository with the console
{: #create-job-private-console}

Create a job configuration that uses an image in a private repository with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private repository, you must first add access to the repository, pull the image, and then create your job configuration.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the job; for example `myjob`.
6. Select **Container Image** from **Code**.
7. To add registry access, click **Edit image details** and then **Add registry**. 
8. From the Add Registry Access page, specify the registry name and registry server.  For example, specify `privatedocker` as the registry name and specify `https://index.docker.io/v1/` as the registry server. 
9. Enter a name. For Docker Hub, it is your Docker ID. 
10. Enter the password. For Docker Hub, you can use your Docker Hub password or an access token. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.
11. Click **Add** to add the registry access for {{site.data.keyword.codeengineshort}}.
12. From the Select image page, the registry that was added is listed. Select the registry of your image.
13. Select the namespace and name of the image in Docker Hub for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `testjob` in that namespace.
14. Select a value for **TAG**; for example, `latest`.
15. Click **Done**. You have selected your image in the registry to reference from your job.
16. From the Create job page, click **Create**.
17. Run your job by clicking `Submit job` from Job runs. Note that you might need to scroll to find the Job runs section.

If you want to add registry access before you create a job configuration, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce). 

### Creating a job with an image from a private repository with CLI
{: #create-job-private-cli}

To create a job configuration with an image from a private repository with CLI, use the `job create` command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [`ibmcloud ce job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private repository, you must first add access to the registry, pull the image, and then create your job configuration.

1. In order to pull images from a private repository, you must first create a private repository. For example, to create a private Docker Hub repository, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private repository, [push an image to it](https://docs.docker.com/docker-hub/repos/){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private repository in order to pull images. To add access to a private repository with the CLI, use the `registry create` command to create an image registry access secret. For example, create registry access to a Docker Hub repository called `privatedocker` that is at ``https://index.docker.io/v1/`` and uses your username and password.

   ```
   ibmcloud ce registry create --name privatedocker --server `https://index.docker.io/v1/` --username <Docker_User_Name> --password <Password>
   ```
   {: pre}

   **Example output**

   ```
   Creating image registry access secret 'privatedocker'...
   OK
   ```
   {: screen}

3. Create your job configuration and reference the image in your private Docker Hub repository. For example, create the `mytestjob` job configuration to reference the `docker.io/PrivateRepo/testjob` by using the `privatedocker` access information. 

   ```
   ibmcloud ce job create --name mytestjob --image docker.io/PrivateRepo/testjob --registry-secret privatedocker
   ```
   {: pre}

The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: important}

## Run a job
{: #run-job}

After you create your job, you can run a job based on its definition, or you can run the job with overriding properties. Run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

When you create a job, you have the option to run it immediately. However, you can submit and resubmit a job at any time. You can also submit or resubmit a job that you previously created.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select Projects from the navigation menu.
3. Select a project as the current context. 
4. From the Overview page, select Jobs from the Summary section or select Jobs from the navigation menu.
5. Click the name of your job to open the configuration.
6. Review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job time out.  
7. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
8. If any of the instances of your job failed to run, click **Submit job for failed indices** to run the job again for indices that failed. From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

You can view job logs after you add logging capabilities. For more information, see [viewing logs](/docs/codeengine?topic=codeengine-view-logs).
{: tip}

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. Each job run instance gets its own index from the array of indices that were specified when the job was created. You can use `JOB_INDEX` with each instance of your job to find its ordinal position in the set of instances that are created. The environment variable key-value pair is set to `JOB_INDEX` and the value is one of the array indices that were specified with **Array indices**, for example `JOB_INDEX=2`.

### Running a job with the CLI
{: #run-job-cli}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a job](#create-job-cli).

To run a job with the CLI, use the `jobrun submit` command. For a complete listing of options, see the [`ibmcloud ce jobrun submit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command.

The following example creates five new instances to run the container image that is specified in the `testjob` job. The resource limits and requests are applied per instance, so each instance gets 128 MB memory and 1 vCPU. This job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce jobrun submit --name testjobrun --job testjob --array-indices "1 - 5" --retrylimit 2 
```
{: pre}

The following table summarizes the options that are used with the `jobrun submit` command in this example. For the most up-to-date information about the command and its options, see the [`ibmcloud ce jobrun submit`](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

<table>
	<caption><code>jobrun</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>jobrun submit</code></td>
   <td>Use `jobrun` commands to run instances of your job.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job to be run. The `--name` and the `--image` values are required, if you do not specify the `--job` value. Use a name that is unique within the project.
    <ul>
      <li>  The name must begin with a lowercase letter.</li>
      <li>  The name must end with a lowercase alphanumeric character.</li>
      <li>  The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
    </ul>
   </td>
   </tr>
   <tr>
   <td><code>--job</code></td>
   <td>The name of the job to be run. This value is required if you do not specify the `--name`  and `image` values. </td>
   </tr>
   <tr>
   <td><code>--retrylimit</code></td>
   <td>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is `3`. </td>
   </tr>
   <tr>
   <td><code>--array-indices</code></td>
   <td>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.</td>
   </tr>
   </tbody>
</table>

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. Each job run instance gets its own index from the array of indices that were specified when the job was created. You can use `JOB_INDEX` with each instance of your job to find its ordinal position in the set of instances that are created. The environment variable key-value pair is set to `JOB_INDEX` and the value is one of the array indices that you specified with **Array indices**, for example `JOB_INDEX=2`.

### Resubmitting your job from the CLI
{: #resubmit-job-cli}

If you want to resubmit a job run based the configuration of a previous job run, use the `jobrun resubmit` command. This command requires the name of the previous job run and also allows allows other optional arguments. For a complete listing of options, see the [`ibmcloud ce jobrun resubmit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command. 
{: shortdesc}

For example, the following `jobrun resubmit` command resubmits the `testjobrun` job run. 
```
ibmcloud ce jobrun resubmit --jobrun testjobrun 
```
{: pre}

**Example output**
   
```
Getting job run 'testjobrun'...
Getting job 'testjob'...
Rerunning job run 'testjob-jobrun-m5f33'...
```
{: screen}

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

To view details of your job with the CLI, use the `job get` command. For a complete listing of options, see the [`ibmcloud ce job get`](/docs/codeengine?topic=codeengine-cli#cli-job-get) command. 
{: shortdesc}

For example, the following `job get` command displays details about the `testjob` job.

```
ibmcloud ce job get --name testjob
```
{: pre}

**Example output**
   
```
Getting job 'testjob'...
OK

Name:          testjob
ID:            abcdefgh-abcd-abcd-abcd-b1f9e6c4eb73
Project Name:  myproj
Project ID:    abcdabcd-abcd-abcd-abcd-876b6e70cd13
Age:           2m4s
Created:       2020-10-14 14:22:23 -0400 EDT

Image:                ibmcom/testjob
Resource Allocation:
  CPU:     1
  Memory:  128Mi
```
{: screen}

### Accessing job details for a specific run of your job with the CLI
{: #access-specific-jobdetails-cli}

To view details of a specific run of your job with the CLI, use the `jobrun get` command.  For a complete listing of options, see the [`ibmcloud ce jobrun  get`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command. 
{: shortdesc}

For example, the following `jobrun get` command displays details about the `testjobrun` job run.

```
ibmcloud ce jobrun get --name testjobrun
```
{: pre}

**Example output**
   
```
Getting jobrun 'testjobrun'...
OK

Name:          testjobrun
ID:            abcdefgh-abcd-abcd-abcd-1d733051eb02
Project Name:  myproj
Project ID:    abcdabcd-abcd-abcd-abcd-8e09-876b6e70cd13
Age:           2m44s
Created:       2020-10-14 14:23:13 -0400 EDT

Job Ref:              testjob
Image:                ibmcom/testjob
Resource Allocation:
  CPU:     1
  Memory:  128Mi

Runtime:
  Array Indices:       1 - 5
  Max Execution Time:  7200
  Retry Limit:         2

Status:
  Completed:          2m14s
  Instance Statuses:
    Succeeded:  5
  Conditions:
    Type      Status  Last Probe  Last Transition
    Pending   True    2m44s       2m44s
    Running   True    2m41s       2m41s
    Complete  True    2m14s       2m14s

Instances:
  Name            Running  Status     Restarts  Age
  testjobrun-1-0  0/1      Succeeded  0         2m47s
  testjobrun-2-0  0/1      Succeeded  0         2m47s
  testjobrun-3-0  0/1      Succeeded  0         2m47s
  testjobrun-4-0  0/1      Succeeded  0         2m47s
  testjobrun-5-0  0/1      Succeeded  0         2m47s
```
{: screen}

### Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The job is accepted by the system, but one or more of the instances of the job are not yet created. This status includes time before a job is scheduled as well as time that is spent downloading images over the network, which might take a while. |
| Running | The job instances are created. At least one instance is still running, or is starting or restarting. |
| Succeeded | All job instances finished successfully and none are restarting. |
| Failed | All job instances finished, and at least one instance ended in failure. That is, the instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the job could not be obtained, typically due to an error in communicating with the host. |
