---

copyright:
  years: 2020
lastupdated: "2020-09-15"

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
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, run a batch job by using the {{site.data.keyword.codeengineshort}} console. Jobs in {{site.data.keyword.codeengineshort}} are meant to run to completion as batch or stand-alone executables and are used for running container images that is designed to run one time and then exit. They are not intended to provide lasting endpoints to access such as an {{site.data.keyword.codeengineshort}} application.
{: shortdesc}

**Before you begin**

To use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 

## Creating a job 
{: #batch-jobcreate}
{: step}

Create a {{site.data.keyword.codeengineshort}} job that uses the [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob){: external}  image in Docker Hub. This job prints `"Hello World"`. 
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the job configuration and specify `docker.io/ibmcom/testjob` for the container image. Use a name for your job that is unique within the project. For this example, you do not need to modify the default values for environment variables or runtime settings.
6. Click **Deploy**.


## Running a job
{: #batch-jobrun-ui}
{: step}

After you create your job and specify your workload configuration information, you are ready to run your job. You can override some configuration information.  
{: shortdesc}

1. Navigate to your job page. 
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your Project. Click **Jobs** to open a listing of your jobs.   
   * From the Jobs page, click the name of the job that you want to run. 

2. From your job page, in the Jobs pane, click **Submit job**. 
3. From the Submit job pane, review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job timeout. The **Array indices** field specifies how many instances of the job to run by using a list or range of indices. For example, to run 10 instances of the job, specify `1-10` or `0-9`, or use a comma-separated list of indices such as `0-8,10`. Click **Submit job** again to run your job. The system displays the status of the instances of your job on the job details page.  

## Access job details
{: #batch-accessjobdetails-ui}
{: step}

Find details about your job.
{: shortdesc}

After you submit your job, the job results are available in the console from the job details page. In the console, you can also view job details by clicking the name of your job in the Jobs pane on your job page. Job details include status of instances, configuration details, and environment variables of your job. 

If any of the instances of your job failed to run, you can take the following actions.

1. Click **Submit job for failed indices** to run the job again for indices that failed.  From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

2. Click **Submit job** to submit the job for the failed indices.

You can view job logs after you add logging capabilities. For more information, see [adding log capabilities](#batch-enablejoblog-ui) and [viewing job logs](#batch-viewjobresult-ui). 
{: tip}



## View job logs 
{: #batch-viewjobresult-ui}
{: step}

After your job completes, view the logs for information on your completed job.
{: shortdesc}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console from your job details page.

### Enabling job logs 
{: #batch-enablejoblog-ui}

If you want to view logs for your job from the console, you must enable logging. 

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: important}

1. After you run a job, the system displays the status of the instances of your job on the job details page. If you did not previously set logging capabilities, the **Add logging** option is displayed. Note, when logging capabilities are set, the job details page displays **Launch logging** instead of **Add logging**.
2. Click **Add logging** on the job details page to create a {{site.data.keyword.la_short}} log instance for your region. 
3. From the {{site.data.keyword.la_short}} page, specify a region, review pricing information, select your plan, and review {{site.data.keyword.la_short}} resource information. Click **Create** to create the logging instance.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

4. Configure {{site.data.keyword.la_short}} platform logs by using one of the following ways: 

  * After the {{site.data.keyword.la_short}} instance is configured, from a job details page, click **Add logging** to configure platform logs. When the dialog opens, select an {{site.data.keyword.la_full_notm}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select an {{site.data.keyword.la_full_notm}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

  * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

5. Now that logging is enabled on the {{site.data.keyword.codeengineshort}} console, whenever you run a job, you can click **Launch logging** from the job details page to open the {{site.data.keyword.la_short}} page for all jobs that are run.
 
After logging is enabled, consider keeping the {{site.data.keyword.la_short}} window open to easily view your job log data. Keeping the {{site.data.keyword.la_short}} window open is useful when you use the Lite service plan as data is not retained with this plan. 
{: tip}

### Viewing job log data 
{: #batch-viewjoblogdata-ui}

You must [enable job logs](#batch-enablejoblog-ui) before you can view job log data from the console. 

* After you click **Submit Job** to run your job, from the job details page, click **Launch logging**.  This action opens the {{site.data.keyword.la_short}} page where you can view your job run log data. 

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the {{site.data.keyword.la_short}} page, you can modify and scope the preset filter to display log data at the job level or a more granular level of a specific job run. For example, the filter `_platform:{{site.data.keyword.codeengineshort}} app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:'Code Engine'``app:myjob` scopes the log data to the job level. 
{: tip}

## Next steps

For more information, see [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).

Looking for more code examples? Check out the [Samples for IBM Cloud Code Engine Github repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
