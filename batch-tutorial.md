---

copyright:
  years: 2020
lastupdated: "2020-08-28"

keywords: code engine, tutorial, batch, job

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


# Tutorial: Running jobs
{: #deploy-job-tutorial}

With this tutorial, run a batch job by using the {{site.data.keyword.codeengineshort}} console. 

{{site.data.keyword.codeengineshort}} supports running batch *jobs*. Batch jobs are stand-alone executables or run-to-completion workloads. Jobs are not intended to provide lasting endpoints to access like a {{site.data.keyword.codeengineshort}} application does. 

A job runs one or more job containers according to the job definition, which contains the workload configuration. After a job definition is created, you can then run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. A job is complete after all the job containers have completed.

**Before you begin**

To use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 


## Step 1. Create a job definition 
{: #batch-jobdef-ui}

Job definitions are templates that define common job types and variables. When you run a job, you can override many of the variables you set in the template. 
{: shortdesc}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Components page, click **Job definition** to create the job definition. 
3. From the Create job definition page, provide a name for your job definition name and a container image reference. You can also modify default runtime settings. You can specify the sample container image reference `ibmcom/testjob`. This tutorial uses a sample Docker image file is available at [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob).
4. Click **Create**. 



## Step 2. Run a job
{: #batch-runjob-ui}

When you run your job, you can override some parameters that are defined by the job definition. 
{: shortdesc}

Before you begin, [create a job definition from the console](#batch-jobdef-ui).

1. Navigate to your job definition page. For example:
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your Project to open the Components page.  
   * From the Components page, click the name of the job definition that you want to run your job. If you have not yet created any job definitions, [create a job definition](#batch-jobdef-ui). 

2. From your job definition page, click **Submit Job** to run a job based on the selected job definition configuration. 
3. From the Submit job pane, review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job timeout. The **Array indices** field specifies how many instances of the job to run by using a list or range of indices. For example, to run 10 instances of the job, specify `1-10` or `0-9`, or use a comma-separated list of indices such as `0-8,10`.
4. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
5. If any of the instances of your job failed to run, click **Submit job for failed indices** to run the job again for indices that failed.  From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

You can view job logs after you add logging capabilities. For more information, see [adding log capabilities](#batch-enablejoblog-ui) and [viewing job logs](#batch-viewjobresult-ui). 
{: tip}

`JOB_INDEX` is an environment variable that is provided by {{site.data.keyword.codeengineshort}} when running a job and gets automatically injected into each instance of your job. There's one `JOB_INDEX` per instance. Each instance gets its own index from the array of indices that was provided when the job was created. You can use `JOB_INDEX` with each instance of your job to know its ordinal position in the set of instances that are created. The key-value pair for this environment variable is as follows:  the key is `JOB_INDEX`, and the value is one of the array indices that you specified using **Array indices**.
{: note}



## Step 3. Access job details
{: #batch-accessjobdetails-ui}

Find details about your job.
{: shortdesc}

After you submit your job, the job results are available in the console from the job details page. In the console, you can also view job details by clicking the name of your job in the Jobs pane on your job definition page. Job details include status of instances, configuration details, and environment variables of your job. 



## Step 4.  View job logs 
{: #batch-viewjobresult-ui}

After your job completes, view the logs for information on your completed job.
{: shortdesc}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console from your job details page.

### Enabling job logs 
{: #batch-enablejoblog-ui}

If you want to view logs for your job from the console, you must enable logging. 

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: important}

1. After you run a job by using your job definition, the system displays the status of the instances of your job on the job details page. If you do not previously set logging capabilities, the **Add logging** option is displayed. Note, when logging capabilities are set, the job details page displays **Launch logging** instead of **Add logging**.
2. Click **Add logging** on the job details page to create a {{site.data.keyword.la_short}} log instance for your region. 
3. From the LogDNA page, specify a region, review pricing information, select your plan, and review LogDNA resource information. Click **Create** to create the logging instance.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

4. Configure LogDNA platform logs by using one of the following ways: 

  * After the LogDNA instance is configured, from a job details page, click **Add logging** to configure platform logs. When the dialogue opens, select an {{site.data.keyword.la_full_notm}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select an {{site.data.keyword.la_full_notm}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

5. Now that logging is enabled on the {{site.data.keyword.codeengineshort}} console, whenever you [run a job](#batch-runjob-ui), you can click **Launch logging** from the job details page to open the LogDNA page for all jobs that are run with this job definition.
 
After logging is enabled, consider keeping the LogDNA window open to easily view your job log data. Keeping the LogDNA window open is particularly useful when you use the Lite service plan as data is not retained with this plan. 
{: tip}

### Viewing job log data 
{: #batch-viewjoblogdata-ui}

You must [enable job logs](#batch-enablejoblog-ui) before you can view job log data from the console. 

* After you click **Submit Job** to run your job, from the job details page, click **Launch logging**.  This action opens the LogDNA page where you can view your job run log data. 

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the LogDNA page, you can modify and scope the preset filter to display log data at the job definition level or a more granular level of a specific job run. For example, the filter `_platform:{{site.data.keyword.codeengineshort}} app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:Coligo app:myjob` scopes the log data to the job definition level. 
{: tip}



## What have you seen?
You created a job definition, ran a job, and viewed the results and details of the job, including job log data.

For more information, see [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).
