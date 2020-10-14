---

copyright:
  years: 2020
lastupdated: "2020-10-14"

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
{: #job-deploy} 

Learn how to run jobs in {{site.data.keyword.codeengineshort}}. A job runs one or more instances of your executable code. Unlike applications, which include an HTTP server to handle incoming requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.

{: shortdesc}

**Before you begin**

   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli).
   * Plan a container image for {{site.data.keyword.codeengineshort}} jobs.

## Plan a container image for {{site.data.keyword.codeengineshort}} jobs
{: #deploy-job-containerimage}

To run jobs in {{site.data.keyword.codeengineshort}}, you must first create a container image that has all of the runtime artifacts that your job needs, such as runtime libraries. You can choose from many different ways to create the image, such as using the Docker `docker build` command, but keep in mind the following key things.  
  * Unlike application images, job images do not have an HTTP server.
  * The executable in the image must exit with a code of zero to be considered successful.
  * Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).
  
You can build your job from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}.

## Create a job 
{: #create-job}

When you create a job, you can specify workload configuration information that is used each time that the job is run. You can create a job from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Creating a job from the console
{: #create-job-ui}

Create a {{site.data.keyword.codeengineshort}} job by using the [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob){: external} image in Docker Hub. This job prints `"Hello World"`. 

1. Open [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the job.
6. Specify a container image for your job. For example, specify the sample `docker.io/ibmcom/testjob` for the container image, which is a simple `Hello World` job. For this example, you do not need to modify the default values for environment variables or runtime settings. If you have your own source code that you want to turn into a container image for the job, see [building a container image](/docs/codeengine?topic=codeengine-build-image).
6. Click **Deploy**.

### Creating a job with the CLI
{: #create-job-cli}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

To create a job with the CLI, use the `job create` command. This command requires a name and an image and also allows other optional arguments. 

The following example creates a job that is named `testjob` that uses the container image `ibmcom/testjob`. 

```
ibmcloud ce job create --image ibmcom/testjob --name testjob 
```
{: pre}

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

## Run a job
{: #run-job}

After you create your job, you can run a job based on its definition, or you can run the job with overriding properties. Run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #run-job-ui}

Before you begin, [create a job from the console](#create-job).

1. Navigate to your job page. For example,
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your Project.  
   * From the Jobs page, click the name of the job that you want to run. If you did not yet create a job, [create a job](#create-job).
2. From your Job page, click **Submit job**.
3. From the Submit job pane, review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job time out.   
4. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
5. If any of the instances of your job failed to run, click **Submit job for failed indices** to run the job again for indices that failed. From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

You can view job logs after you add logging capabilities. For more information, see [viewing job logs](#view-job-logs). 
{: tip}

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. Each job run instance gets its own index from the array of indices that were specified when the job was created. You can use `JOB_INDEX` with each instance of your job to find its ordinal position in the set of instances that are created. The environment variable key-value pair is set to `JOB_INDEX` and the value is one of the array indices that were specified with **Array indices**, for example `JOB_INDEX=2`.

### Running a job with the CLI
{: #run-job-cli}

**Before you begin**

* Set up your [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create a job](#create-job-cli).

To run a job with the CLI, use the `jobrun submit` command. 

The following example creates five new instances to run the container image that is specified in the `testjob` job. The resource limits and requests are applied per instance, so each instance gets 128 MB memory and 1 vCPU. This job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce jobrun submit --name testjobrun --job testjob --array-indices "1 - 5" --retrylimit 2 
```
{: pre}

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
   <td>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9`, `1-5,7-8,10`, or `"1 - 10"`. This value is optional. The default value is <code>0</code>.</td>
   </tr>
   </tbody>
</table>

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. Each job run instance gets its own index from the array of indices that were specified when the job was created. You can use `JOB_INDEX` with each instance of your job to find its ordinal position in the set of instances that are created. The environment variable key-value pair is set to `JOB_INDEX` and the value is one of the array indices that you specified with **Array indices**, for example `JOB_INDEX=2`.

### Resubmitting your job from the CLI
{: #resubmit-job-cli}

If you want to rerun your job run, by using the `jobrun resubmit` command.

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

To view details of your job with the CLI, use the `job get` command.

```
ibmcloud ce job get --name testjob
```
{: pre}

**Example output**
   
```
Getting job 'testjob'...
   
Name:              testjob
Project:           myproject

[...]

Spec:
  Array Indices:       0
  Max Execution Time:  7200
  Retry Limit:         3
  Template:
    Containers:
      Arguments:
      Commands:
      Environment Variables:
      Image:                  ibmcom/testjob
      Name:                   testjob
      Resource Requests:
        Cpu:                1
        Ephemeral Storage:  500Mi
        Memory:             128Mi
Service Bindings:
```
{: screen}

### Accessing job details for a specific run of your job with the CLI
{: #access-specific-jobdetails-cli}

To view details of a specific run of your job with the CLI, use the `jobrun get` command. 

```
ibmcloud ce jobrun get --name testjobrun
```
{: pre}

**Example output**
   
```
Getting job run 'testjobrun'...
OK

Name:               testjobrun
Project:            myproject
[...]
   
Running Instances:
  Name            Ready  Status     Restarts  Age
  testjobrun-1-0  0/1    Succeeded  0         19m
  testjobrun-2-0  0/1    Succeeded  0         19m
  testjobrun-3-0  0/1    Succeeded  0         19m
  testjobrun-4-0  0/1    Succeeded  0         19m
  testjobrun-5-0  0/1    Succeeded  0         19m
[...] 

Spec:
  Job Ref:  testjob
  Job Spec:
    Array Indices:       1 - 5
    Max Execution Time:  7200
    Retry Limit:         2
    Template:
      Containers:
        Arguments:
        Commands:
        Environment Variables:
        Image:                  ibmcom/testjob
        Name:                   testjob
        Resource Requests:
          Cpu:                1
          Ephemeral Storage:  500Mi
          Memory:             128Mi
Status:
  Start Time:       2020-09-13 06:15:05 -0400 EDT
  Completion Time:  2020-09-13 06:15:09 -0400 EDT
  Conditions:
Last Probe Time:       2020-09-13 06:15:05 -0400 EDT
    Last Transition Time:  2020-09-13 06:15:05 -0400 EDT
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-09-13 06:15:08 -0400 EDT
    Last Transition Time:  2020-09-13 06:15:08 -0400 EDT
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-09-13 06:15:09 -0400 EDT
    Last Transition Time:  2020-09-13 06:15:09 -0400 EDT
    Status:                True
    Type:                  Complete
  Effective Job Spec:
    Array Indices:       1 - 5
    Max Execution Time:  7200
    Retry Limit:         2
    Template:
      Containers:
        Arguments:
        Commands:
        Environment Variables:
        Image:                  ibmcom/testjob
        Name:                   testjob
    Resource Requests:
          Cpu:                1
          Ephemeral Storage:  500Mi
          Memory:             128Mi
  Instances:
    Failed:     0
    Pending:    0
    Running:    0
    Succeeded:  5
    Unknown:    0
```
{: screen}

## View job logs
{: #view-job-logs}

After your job completes, view the logs for information about your completed job.
{: shortdesc}

### Viewing job logs from the console
{: #view-joblogs-ui}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console from your job details page. 

If you want to view logs for your job from the console, you must enable logging. 

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: important}

After you run a job, the system displays the status of the instances of your job on the job details page. If logging capabilities are not set, the **Add logging** option is displayed. Note, when logging capabilities are set, the job details page displays **Launch logging** instead of **Add logging**.

After you enable logging, you can keep the {{site.data.keyword.la_short}} window open to view your job log data. Keeping the {{site.data.keyword.la_short}} window open is useful when you use the Lite service plan as data is not retained with this plan. 
{: tip}

1. Click **Add logging** on the job details page to create a {{site.data.keyword.la_short}} log instance for your region.
2. From the {{site.data.keyword.la_short}} page, specify a region, review pricing information, select your plan, and review {{site.data.keyword.la_short}} resource information. Click **Create** to create the logging instance.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

3. Configure {{site.data.keyword.la_short}} platform logs by using one of the following ways: 

   * After the {{site.data.keyword.la_short}} instance is configured, from a job details page, click **Add logging** to configure platform logs. When the dialog opens, select a {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

   * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select the {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

   * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

4. Now that you enabled logging, you can click **Launch logging** from the job details page to open the {{site.data.keyword.la_short}} page for all jobs that are run.

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the {{site.data.keyword.la_short}} page, you can modify and scope the preset filter to display log data at the job level or a more granular level of a specific job run. For example, the filter `_platform:{{site.data.keyword.codeengineshort}} app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:Code Engine app:myjob` scopes the log data to the job level. 
{: tip}


### Viewing job logs with the CLI
{: #view-joblog-cli}

To view job logs for a specific run with the CLI, use the `jobrun logs` command. The `jobrun get` command displays details about your run, including the running instances of the run. 

For example, to view the logs for the `testjobrun` job, use the command: 

```
ibmcloud ce jobrun logs --instance testjobrun-1-0 
```
{: pre}

**Example output**

```
Logging job run instance 'testjobrun-1-0'...
OK

Hello World!
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
