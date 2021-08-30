---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-30"

keywords: job tutorial, jobs, images for code engine jobs, tutorial for code engine, job log

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

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


# Running jobs
{: #run-job-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, run a batch job by using the {{site.data.keyword.codeenginefull}} console.
{: shortdesc}

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.

**Before you begin**

To use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 

Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage.
{: note}

## Creating a job 
{: #batch-jobcreate}
{: step}

Create a {{site.data.keyword.codeengineshort}} job by using the [`ibmcom/firstjob`](https://hub.docker.com/r/ibmcom/firstjob){: external} image in Docker Hub. This job prints `Hi from a batch job! My index is:`. 
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
5. Enter a name for the job and specify `docker.io/ibmcom/firstjob` for the container image. Use a name for your job that is unique within the project. For this example, you do not need to modify the default values for environment variables or runtime settings.
6. Click **Create**.

## Running a job
{: #batch-jobrun-ui}
{: step}

After you create your job and specify your workload configuration information, you are ready to run your job. You can override some configuration information. Note that when you run your job, the most current version of your referenced container image is downloaded and deployed.
{: shortdesc}

1. Navigate to your job page. 
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
   * From the Jobs page, click the name of the job that you want to run. 

2. From your job page, in the Jobs pane, click **Submit job**. 
3. From the Submit job pane, accept all of the default values, and click **Submit job** again to run your job.

From the Submit job pane, you can review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. After you submit this job, the system displays the status of the instances of your job on the Job details page. If you specify **Number of instances** instead of **Array indices** in the Submit job pane, from the `Configuration` section of the Job details page, this information is provided as **Array indices**.
{: note} 

## Accessing job details
{: #batch-accessjobdetails-ui}
{: step}

Find details about your job.
{: shortdesc}

After you submit your job, the job results are available in the console from the Job details page. In the console, you can also view job details by clicking the name of your job in the Jobs pane on your job page. Job details include status of instances, configuration details, and environment variables of your job. 

If any of the instances of your job failed to run, you can take the following actions.

1. Click **Rerun failed indices** to run the job again for indices that failed.  From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

2. Click **Submit job** to submit the job for the failed indices.

You can view job logs after you add logging capabilities. For more information, see [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui). 
{: tip}

## Updating a job 
{: #batch-updatejob-ui}
{: step}

You can manage your job by fine tuning your job configuration, which includes updating the code container image, code arguments or commands, runtime instance resources, or environment variables.
{: shortdesc}

When the job is in ready state, you can update the job. Let's update the job that you created previously to change the container image from `ibmcom/firstjob` to `ibmcom/testjob` and then subsequently update an environment variable. When a request is sent to this [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob){: external} sample job, the job reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. 

1. Navigate to your job page. 
   * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
   * From the Jobs page, click the name of the job that you want to update. 

2. To update the image reference of your job, provide the name of your image or configure an image. Update the name of the image from `ibmcom/firstjob` to `ibmcom/testjob`. Click **Save**. 
3. Click **Submit job** .
4. From the Submit job pane, review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. Click **Submit job** again to run your job. The system displays the status of the instances of your job on the Job details page.  
3. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the job is `Hello World!`.
4. To update the job again and add an environment variable, navigate to your job page. 
5. Click **Environment variables** to open the tab and then click **Add**. Add a literal environment variable with the name of `TARGET` with a value of `Sunshine`. The `ibmcom/testjob` outputs the message, `Hello <value_of_TARGET>!>`.
6. Click **Add** to add your environment variable and then click **Save** to save the changes to your job. 
7. From the Submit job pane, review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. This time, specify **Number of instances** as `3`. Click **Submit job** again to run your job. The system displays the status of the instances of your job on the Job details page. From the `Configuration` section of the Job details page, the information about the number of instances is displayed as **Array indices**, which is `0 - 2` for this example. 
8. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the updated job is `Hello Sunshine!`.
  
## Next steps for jobs
{: #nextsteps-deployjobtut}

For more information, see [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
