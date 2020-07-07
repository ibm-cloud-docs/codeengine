---

copyright:
  years: 2020
lastupdated: "2020-07-07"

keywords: code engine, tutorial, batch, job

subcollection: code-engine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Tutorial: Running jobs
{: #kn-deploy-job-tutorial}

With this tutorial, run a batch job using the {{site.data.keyword.codeengineshort}} CLI or the console. 

{{site.data.keyword.codeengineshort}} provides support for running batch *jobs*. Batch jobs are stand-alone executables or run-to-completion workloads. Jobs are not intended to provide lasting endpoints to access like a {{site.data.keyword.codeengineshort}} application does. 

A job runs one or more job containers according to the job definition, which contains the workload configuration. After a job definition is created, you can then run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. A job is complete after all the job containers have completed.

Before you begin:
* If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/knative/overview){: external}. 
* If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/code-engine?topic=code-engine-kn-install-cli).


## Step 1. Create a job definition 
{: #batch-jobdef}

Job definitions are templates that define common job types and variables. When you run a job, you can override many of the variables you set in the template. You can create job definitions from the console or with the CLI.
{: shortdesc}

### Creating a job definition from the console
{: #batch-jobdef-ui}

Before you begin, [create a project](/docs/code-engine?topic=code-engine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}. 
2. From the Components page, click **Job definition** to create the job definition. 
3. From the Create job definition page, provide a name for your job definition name and a container image reference. You can also modify default runtime settings. You can specify the sample container image reference `ibmcom/testjob`. This tutorial uses a sample Docker image file is available at [ibmcom/testjob](https://hub.docker.com/r/ibmcom/testjob).
4. Click **Create**. 

### Creating a job definition with the CLI
{: #batch-jobdef-cli}

Before you begin:
* [Create and work with a project](/docs/code-engine?topic=code-engine-manage-project).
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/code-engine?topic=code-engine-kn-install-cli) environment.

To create a job definition with the CLI, run the `ibmcloud coligo jobdef create` command. This command requires a name and an image and also allows other optional arguments.

The following example creates a job definition named `testjobdef` that uses the container image `ibmcom/testjob` and assigns 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image ibmcom/testjob --name testjobdef --memory 128M --cpu 1
```
{: pre}

<table>
   <caption>jobdef create components</caption>
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
   <td>The name of the image used for this job definition. This value is required. For images in [Docker Hub](https://hub.docker.com), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the job definition. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--argument</code></td>
   <td>Set any arguments for the job definition. This value is required. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Set any environment variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set a command for the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>The amount of memory set for the job definition. The default value is 128 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>Specifies the number of CPUs to be assigned to the job definition. The default value is 1. This value is optional.</td>
   </tr>
   </tbody></table>

## Step 2. Run a job
{: #batch-runjob}

After you create your job definition, the job definition is used to describe the parameters for your job. When you run your job, you can override some parameters that are defined by the job definition. Run your job from the console or with the CLI.
{: shortdesc}

### Running a job from the console
{: #batch-runjob-ui}

Before you begin, [create a job definition from the console](#batch-jobdef-ui).

1. Navigate to your job definition page. For example:
   1. From the Projects page, click the name of your desired Project to open the Components page for your Project. 
   2. From the Components page, click the name of the job definition that you want to run your job. If you do not have any job definitions defined, [create a job definition](#batch-jobdef-ui). 


3. From your job definition page, click **Submit Job** to run a job based on the selected job definition configuration. 
4. From the Submit job page, review and optionally change configuration values such as array size, CPU, memory, number of job retries, and job timeout. **Array size** specifies the number of instances or containers to run your job. 
5. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 

You can view job logs after you add logging capabilities. See [adding log capabilities](#batch-enablejoblog-ui) and [viewing job logs from the console](#batch-viewjobresult-ui) for more information. 
{: tip}

### Running a job with the CLI
{: #batch-runjob-cli}

Before you begin, [create a job definition with the CLI](#batch-jobdef-cli).

To run a job with the CLI, use the `ibmcloud coligo job run` command. 

The following example creates three new pods to run the container image specified in the `testjobdef` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name testjobrun --jobdef testjobdef --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
```
{: pre}


<table>
   <caption>job run components</caption>
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
   <td>The name of the job to be run. This value is required. The name must begin with a lowercase letter, can contain letters, numbers, periods (.), and hyphens (-), and must be 35 characters or fewer. The name must start and end with a lowercase alphanumeric character. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--jobdef</code></td>
   <td>Identifies the job definition that contains the description of the job to be run. This value is required.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image used for this job. This value is required. For images in [Docker Hub](https://hub.docker.com), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition.</td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>Specifies the number of CPUs to assign to the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>Specifies the amount of memory to assign to the container that is running the image. This value overrides any `--memory` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 128 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--retrylimit</code></td>
   <td>Specifies the number of times to retry the job. The default value is 3. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--arraysize</code></td>
   <td>Indicates how may pods can be used to run the container specified by the job definition. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--argument</code></td>
   <td>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--command</code></td>
   <td>Set any commands for the job. This value overrides any commands that are passed in the job definition. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--env</code></td>
   <td>Specifies any environment variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environment variables that are passed in the job definition. This value is optional.</td>
   </tr>
      <tr>
   <td><code>--maxexecutiontime</code></td>
   <td>Specifies the maximum execution time for the job.  The default value is 7200 seconds. This value is optional.</td>
   </tr>
   </tbody></table>

## Step 3. Access job details
{: #batch-accessjobdetails}

Find details about your job from the console or with the CLI.
{: shortdesc}

### Accessing job details from the console
{: #batch-accessjobdetails-ui}

Job results are available in the console from the job details page after submitting your job. You can also view job details in the console by clicking on the name of your job in the Jobs pane on your job definition page. Job details include status of your instances, configuration details, and environment variables of your job. 

### Accessing job details with the CLI
{: #batch-accessjobdetails-cli}

To view job details with the CLI, use the `ibmcloud coligo job get` command. 

For example, `ibmcloud coligo job get --name testjobrun`.

**Example output**

```
Getting Job 'testjobrun'...
Name:         testjobrun-w6rmp
Namespace:    ae2f5ad7-6196
Labels:       coligo.cloud.ibm.com/job-definition=testjobdef
              jobrun=testjobrun
Annotations:  coligo.cloud.ibm.com/pod-expectations: 5
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobRun
Metadata:
  Creation Timestamp:  2020-05-08T00:13:10Z
  Generate Name:       testjobrun-
  Generation:          1
  Resource Version:    92429386
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/ae2f5ad7-6196/jobruns/testjobrun-w6rmp
  UID:                 cce00a2d-8db1-44fd-bf17-fda22e863911
Spec:
  Array Size:          5
  Job Definition Ref:  testjobdef
  Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Resources:
        Requests:
          Cpu:         1
          Memory:      128Mi
  Max Execution Time:  7200
  Retry Limit:         2
Status:
  Completion Time:  2020-05-08T00:13:51Z
  Conditions:
    Last Probe Time:       2020-05-08T00:13:46Z
    Last Transition Time:  2020-05-08T00:13:46Z
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-05-08T00:13:50Z
    Last Transition Time:  2020-05-08T00:13:50Z
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-05-08T00:13:51Z
    Last Transition Time:  2020-05-08T00:13:51Z
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Containers:
      Image:  ibmcom/testjob
      Name:   testjobdef
      Resources:
        Requests:
          Cpu:     1
          Memory:  128Mi
  Start Time:      2020-05-08T00:13:46Z
  Succeeded:       5
Events:
  Type    Reason     Age                            From                  Message
  ----    ------     ----                           ----                  -------
  Normal  Updated    <invalid> (x5 over <invalid>)  batch-job-controller  Updated JobRun "testjobrun-w6rmp"
  Normal  Completed  <invalid>                      batch-job-controller  JobRun completed successfully


Command 'job get' performed successfully
```
{: screen}

## Step 4.  View job logs 
{: #batch-viewjobresult}

After your job has completed, view the logs for information on your completed job.
{: shortdesc}

### Viewing job logs from the console
{: #batch-viewjobresult-ui}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console  from your job details page.

#### Enabling job logs from the console
{: #batch-enablejoblog-ui}

If you want to view logs for your job from the console, enable logging before you run your job. 

You only need to enable logging for {{site.data.keyword.codeengineshort}} one time per region, per account.
{: important}



1. After running a job using your job definition, the system displays the status of the instances of your job on the job details page. If logging capabilities are not set, the **Add logging** option is displayed.  When logging capabilties are set, the job details page displays **Launch logging** instead of **Add logging**.
2. Click **Add logging** on the job details page to create a log instance for your region. 
3. From the LogDNA page, specify a region, review pricing information and select your plan, and review LogDNA resource information.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

4. Click **Create** to create the logging instance.
5. Configure platform logs using one of the following ways:  

  * After you **Submit job** to run your next job, click **Add logging** from the job details page to configure platform logs. Select an IBM Log Analysis with LogDNA instance to receive platform logs. Select an instance for your region and click **Configure**.

  * [Configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui) from the [Observability dashboard](https://cloud.ibm.com/observe/logging). Click **Configure platform logs**. Select an IBM Log Analysis with LogDNA instance to receive platform log data by specifying a region and your log instance. Click **Configure**.

6. (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

7. Now that logging is enabled on the console for {{site.data.keyword.codeengineshort}}, whenever you [run a job](#batch-runjob-ui), you can click **Launch logging** from the job details page to open the LogDNA page for all jobs that are run using this job definition.
 
After enabling logging, consider keeping the LogDNA window open to easily view your job log data.
{: tip}

#### Viewing job log data from the console
{: #batch-viewjoblogdata-ui}

You must enable job logs before you can view job log data from the console.  

* After clicking **Submit Job** to run your job, from the job details page, click **Launch logging**.  This action opens the LogDNA page where you can view your job run log data. 

 

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the LogDNA page, you can modify and scope the preset filter to display log data at the job definition level or a more granular level of a specific job run. For example, the filter `_platform:Coligo app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:Coligo app:myjob` scopes the log data to the job definition level. 
{: tip}

### Viewing job logs with the CLI
{: #batch-viewjobresult-cli}

To view job logs with the CLI, use the `ibmcloud coligo job logs` command. 

For example, to view the logs for our `testjobrun` job, use the command: 

```
ibmcloud coligo job logs --name testjobrun 
```
{: pre}

**Example output**

```
Logging Job 'testjobrun' on Pod 0...

Hello World!

Command 'job logs' performed successfully
```
{: screen}

Congratulations! You have created a job definition, run a job, and viewed details and results of the job.

For more information, see [Running jobs](/docs/code-engine?topic=code-engine-kn-job-deploy).
