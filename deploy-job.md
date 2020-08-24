---

copyright:
  years: 2020
lastupdated: "2020-08-24"

keywords: code engine, job, batch

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


# Running jobs 
{: #kn-job-deploy} 

Learn how to run jobs in {{site.data.keyword.codeengineshort}}. Jobs in {{site.data.keyword.codeengineshort}} are meant to run to completion as batch or stand-alone executables. They are not intended to provide lasting endpoints to access like a {{site.data.keyword.codeengineshort}} application does.
{: shortdesc}

**Before you begin**
   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli).
   * Create a container image for {{site.data.keyword.codeengineshort}} jobs.

## Creating a container image for {{site.data.keyword.codeengineshort}} jobs
{: #deploy-job-containerimage}

To run jobs in {{site.data.keyword.codeengineshort}}, you must first create a container image that has all of the runtime artifacts that your job needs, such as runtime libraries. You can choose from many different ways to create the image, such as using the Docker `docker build` command, but keep in mind the following key things.  
  * Unlike application images, job images do not have an HTTP server.
  * The executable in the image must exit with a code of zero to be considered successful.
  * Your image must be downloadable from a publicly accessible image registry.

## Create a job definition
{: #create-job-def}

Jobs, unlike applications, which react to incoming HTTP requests, are meant to be used for running container images that contain an executable that is designed to run one time and then exit. Rather than specifying the full configuration of a job each time it is executed, you can create a *job definition*, which acts as a "template" for the job.

When you run a job, you can override many of the variables that you set in the template. You can create job definitions from the console or with the CLI.

{: shortdesc}

### Creating a job definition from the console
{: #create-job-def-ui}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).  

1. After your project is in **Active** status, click the name of your project on the Projects page.
2. From the Components page, click **Job definition** to create the job definition.
3. From the Create job definition page, provide a name for your job definition and a container image.  You can also modify default runtime settings. 
4. Click **Create**. 

### Creating a job definition with the CLI
{: #create-job-def-cli}

Before you begin:

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

To create a job definition with the CLI, run the `ibmcloud ce jobdef create` command. This command requires a name and an image and also allows other optional arguments. 

The following example creates a job definition that is named `testjobdef` that uses the container image `ibmcom/testjob`. 

```
ibmcloud ce jobdef create --image ibmcom/testjob --name testjobdef 
```
{: pre}

<table>
  <caption><code>jobdef create</code> components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>jobdef create</code></td>
   <td>The command to create your job definition.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job definition. This value is required. For images in [Docker Hub](https://hub.docker.com/), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job definition. Use a name that is unique within the project. This value is required.
     <ul>
	   <li>The name must begin with a lowercase letter.</li>
	   <li>The name must end with a lowercase alphanumeric character.</li>
	   <li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   </tbody></table>

## Running a job
{: #run-job}

After you create your job definitions, you can use that definition to describe the parameters for your job. You can override some parameters that are defined by the job definition. Run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

Before you begin, [create a job definition from the console](#create-job-def).

1. Navigate to your job definition page. For example:
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your Project to open the Components page.  
   * From the Components page, click the name of the job definition that you want to run your job. If you have not yet created any job definitions, [create a job definition](#create-job-def).
2. From your job definition page, click **Submit Job** to run a job based on the selected job definition configuration. 
3. From the Submit job pane, review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job timeout. The **Array indices** field specifies how many instances of the job to run by using a list or range of indices. For example, to run 10 instances of the job, specify `1 - 10` or `0 - 9`, or use a comma-separated list of indices such as `0 - 8, 10`.
4. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
5. If any of the instances of your job failed to run, click **Submit job for failed indices** to run the job again for indices that failed.  From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

You can view job logs after you add logging capabilities. For more information, see [viewing job logs](#view-job-logs). 
{: tip}

### Running a job with the CLI
{: #run-job-cli}

Before you begin:

* Set up your [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create a job definition](#create-job-def-cli).

To run a job with the CLI, use the `ibmcloud ce job run` command. 

The following example creates five new instances to run the container image specified in the `testjobdef` job definition. The resource limits and requests are applied per instance, so each instance gets 128 MB memory and 1 vCPU. This job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce job run --name testjobrun --jobdef testjobdef --array-indices 1-5 --retrylimit 2 
```
{: pre}

<table>
	<caption><code>job run</code> components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>job run</code></td>
   <td>The command to run your job.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job to be run. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. Use a name that is unique within the project.
    <ul>
      <li>  The name must begin with a lowercase letter.</li>
      <li>  The name must end with a lowercase alphanumeric character.</li>
      <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
    </ul>
   </td>
   </tr>
   <tr>
   <td><code>--jobdef</code></td>
   <td>The name of the job definition that contains the description of the job to be run. This value is required if you do not specify the `--name`  and `image` values. </td>
   </tr>
   <tr>
   <td><code>--retrylimit</code></td>
   <td>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is `3`. </td>
   </tr>
   <tr>
   <td><code>--array-indices</code></td>
   <td>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5, 7 - 8, 10`. This value is optional. The default value is <code>0</code>.</td>
   </tr>
   </tbody>
</table>

## Accessing the job details
{: #access-job-details}

Find details about your job from the console or with the CLI.
{: shortdesc}

View job details in the console by clicking the name of your job in the Jobs pane on your job definition page. Job details include status of your instances, configuration details, and environment variables of your job. 

To view job details with the CLI, use the `ibmcloud ce job get` command.  For example, `ibmcloud ce job get --name hello`.

### Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The Job is accepted by the system, but one or more of the instances of the job are not yet created. This status includes time before a job is scheduled as well as time that is spent downloading images over the network, which might take a while. |
| Running | The Job instances are created. At least one instance is still running, or is starting or restarting. |
| Succeeded | All Job instances finished successfully and none are restarting. |
| Failed | All Job instances finished, and at least one instance ended in failure. That is, the instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the Job could not be obtained, typically due to an error in communicating with the host. |

### Accessing job details from the console
{: #access-jobdetails-ui}

Job results are available in the console from the job details page after you submit your job. You can also view job details in the console by clicking the name of your job in the Jobs pane on your job definition page. Job details include status of your instances, configuration details, and environment variables of your job.  

### Accessing job details with the CLI
{: #access-jobdetails-cli}

To view job details with the CLI, use the `ibmcloud ce job get` command. 

For example, `ibmcloud ce job get --name testjobrun`.

**Example output**

```
Getting job 'testjobrun'...
Name:        testjobrun
Project ID:  18bb53d9-b5ec
Metadata:
  Creation Timestamp:  2020-08-14 11:42:17 -0400 EDT
  Generation:          1
  Resource Version:    217272060
  Self Link:           /apis/codeengine.cloud.ibm.com/v1alpha1/namespaces/18bb53d9-b5ec/jobruns/testjobrun
  UID:                 d25b646b-4a78-4976-a4f0-a412adeb1fed
Spec:
  Array Indices:       1-5
  Job Definition Ref:  testjobdef
  Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Commands:
      Arguments:
      Resource Requests:
        Cpu:     1
        Memory:  128Mi
  Max Execution Time:  7200
  Retry Limit:         2
Status:
  Completion Time:  2020-08-14 11:42:21 -0400 EDT
  Conditions:
    Last Probe Time:       2020-08-14 11:42:17 -0400 EDT
    Last Transition Time:  2020-08-14 11:42:17 -0400 EDT
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-08-14 11:42:19 -0400 EDT
    Last Transition Time:  2020-08-14 11:42:19 -0400 EDT
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-08-14 11:42:21 -0400 EDT
    Last Transition Time:  2020-08-14 11:42:21 -0400 EDT
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Commands:
      Arguments:
      Resource Requests:
        Cpu:     1
        Memory:  128Mi
  Succeeded:        5
OK
Command 'job get' performed successfully
```
{: screen}


## Viewing job logs
{: #view-job-logs}

After your job completes, view the logs for information about your completed job.
{: shortdesc}

### Viewing job logs from the console
{: #view-joblogs-ui}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console from your job details page. 

If you want to view logs for your job from the console, you must enable logging. 

You need only to enable logging for {{site.data.keyword.codeengineshort}} one time per region, per account.
{: important}

1. After a job runs, the system displays the status of the instances of your job on the job details page. If logging capabilities are not set, the **Add logging** option is displayed. Note, when logging capabilities are set, the job details page displays **Launch logging** instead of **Add logging**.
2. Click **Add logging** on the job details page to create a {{site.data.keyword.la_short}}  log instance for your region.
3. From the LogDNA page, specify a region, review pricing information, select your plan, and review LogDNA resource information. Click **Create** to create the logging instance.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

4. Configure LogDNA platform logs by using one of the following ways: 

  * After the LogDNA instance is configured, from a job details page, click **Add logging** to configure platform logs. When the dialogue opens, select an {{site.data.keyword.la_full}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select an IBM Log Analysis with LogDNA instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

5. Now that logging is enabled, whenever you [run a job](#run-job-ui), you can click **Launch logging** from the job details page. This action opens the LogDNA page where you can view your job run log data.

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the LogDNA page, you can modify and scope the preset filter to display log data at the job definition level or a more granular level of a specific job run. For example, the filter `_platform:{{site.data.keyword.codeengineshort}} app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:Coligo app:myjob` scopes the log data to the job definition level. 
{: note}

After logging is enabled, consider keeping the LogDNA window open to easily view your job log data. Keeping the LogDNA window open is particularly useful when you use the Lite service plan as data is not retained with this plan. 
{: tip}

### Viewing job logs with the CLI
{: #view-joblog-cli}

To view job logs with the CLI, use the `ibmcloud ce job logs` command. 

For example, to view the logs for our `testjobrun` job, use the command: 

```
ibmcloud ce job logs --name testjobrun 
```
{: pre}

**Example output**

```
Logging Job 'testjobrun' on Pod 0...

Hello World!

Command 'job logs' performed successfully
```
{: screen}



