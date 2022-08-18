---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-16"

keywords: job tutorial, jobs, images for code engine jobs, tutorial for code engine, job log

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Running and updating jobs 
{: #run-job-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, run a batch job by using the {{site.data.keyword.codeenginefull}} console.
{: shortdesc}

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.

Before you begin

To use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Creating a job 
{: #batch-jobcreate}
{: step}

Create a {{site.data.keyword.codeengineshort}} job by using the `icr.io/codeengine/firstjob` image. This job prints `Hi from a batch job! My index is:`. 
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} Overview page.
2. Select **Start creating** from **Run a container image**.
3. Select **Job**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
5. Enter a name for the job and specify `icr.io/codeengine/firstjob` for the container image. Use a name for your job that is unique within the project. For this example, you do not need to modify the default values for environment variables or runtime settings. For more information about the code that is used for this example, see [`firstjob`](https://github.com/IBM/CodeEngine/tree/main/job){: external}. 
6. Click **Create**.

## Running a job
{: #batch-jobrun-ui}
{: step}

After you create your job and specify your workload configuration information, you are ready to run your job. You can override some configuration information. 
{: shortdesc}

Note that when you run your job, the latest version of your referenced container image is downloaded and deployed, unless you specified a tag for the image. If a tag is specified for the image, then the tagged image is used for the job. 

1. Navigate to your job page. 
    * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
    * From the Jobs page, click the name of the job that you want to run. 

2. From your job page, click **Submit job** to submit a job that is based on the current configuration. 
3. From the Submit job pane, accept all the default values, and click **Submit job** again to run your job.

From the Submit job pane, you can review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. After you submit this job, the system displays the status of the instances of your job on the Job details page. If you specify **Number of instances** instead of **Array indices** in the Submit job pane, from the `Configuration` section of the Job details page, this information is provided as **Array indices**.
{: note} 

## Accessing job details
{: #batch-accessjobdetails-ui}
{: step}

Find details about your job.
{: shortdesc}

After you submit your job, the job results are available in the console from the Job details page. In the console, you can also view job details by clicking the name of your job run from the **Job runs** section of your job. Job details include status of instances, configuration details, and environment variables of your job. 

If any of the instances of your job failed to run, you can take the following actions.

1. Click **Rerun failed indices** to run the job again for indices that failed. From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

2. Click **Submit job** to submit the job for the failed indices.

You can view job logs after you add logging capabilities. For more information, see [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui). 
{: tip}

## Updating a job 
{: #batch-updatejob-ui}
{: step}

You can manage your job by fine tuning your job configuration, which includes updating the code container image, code arguments or commands, runtime instance resources, or environment variables.
{: shortdesc}

When the job is in ready state, you can update the job. Let's update the job that you created previously to change the container image from `icr.io/codeengine/firstjob` to `icr.io/codeengine/testjob` and then subsequently update an environment variable. When a request is sent to this `icr.io/codeengine/testjob` sample job, the job reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. For more information about the code that is used for this example, see [`testjob`](https://github.com/IBM/CodeEngine/tree/main/testjob){: external}.

1. Navigate to your job page. 
    * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
    * From the Jobs page, click the name of the job that you want to update. 

2. To update the image reference of your job, provide the name of your image or configure an image. Update the name of the image from `icr.io/codeengine/firstjob` to `icr.io/codeengine/testjob`. Click **Save**. 
3. Click **Submit job**.
4. From the Submit job pane, review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. Click **Submit job** again to run your job. The system displays the status of the instances of your job on the Job details page.  
5. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the job is `Hello World!`.
6. To update the job again and add an environment variable, navigate to your job page. 
7. Click **Environment variables** to open the tab and then click **Add environment variable**. Add a literal environment variable with the name of `TARGET` with a value of `Sunshine`. The `icr.io/codeengine/testjob` outputs the message, `Hello <value_of_TARGET>!>`.
8. Click **Done** to add your environment variable and then click **Save** to save the changes to your job. 
9. Click **Submit job** to submit the updated job.
10. From the Submit job pane, review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. This time, specify **Number of instances** as `3`. Click **Submit job** again to run your job. The system displays the status of the instances of your job on the Job details page. From the `Configuration` section of the Job details page, the information about the number of instances is displayed as **Array indices**, which is `0 - 2` for this example. 
11. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the updated job is `Hello Sunshine!`.

## Next steps
{: #nextsteps-deployjobtut}

* After you create your job, submit the job to run it. See [Run a job](/docs/codeengine?topic=codeengine-run-job). You can run your job multiple times. 

* After you [run your job](/docs/codeengine?topic=codeengine-run-job), to view details of your job and job runs, see [access job details](/docs/codeengine?topic=codeengine-access-job-details).

* Now that your job is created, consider making your jobs event-driven. By using event subscriptions, you can trigger your jobs by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or set your job to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).

* You can [update your job](/docs/codeengine?topic=codeengine-update-job) and its referenced code in *any* of the following ways, independent of how you created or previously updated your job.

    - If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create (or update) your job. You can create (or update) your job from images in a [public registry](/docs/codeengine?topic=codeengine-create-job) or [private registry](/docs/codeengine?topic=codeengine-create-job-private) and then access the referenced image from your job run.

        If you created your job by using the **`job create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your job to point to a different container image, you must first remove the association of the build from your job. For example, run `ibmcloud ce job update -n JOB_NAME --build-clear`. After you remove the association of the build from your job, you can update the job to reference a different image. 
        {: important}


    - If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating (or updating) the job with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.  

    - If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating the job with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.

    For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the job. Then, after the image is matured, you can update the job to reference the specific image that you want. You can repeat this process as needed.

    When you run your updated job, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run. 





Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

