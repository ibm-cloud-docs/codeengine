---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-09"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Create a job from a public registry
{: #create-job}

When you create a job, you can specify workload configuration information that is used each time that the job is run. You can create a job from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Creating a job with the console
{: #create-job-ui}

Create a {{site.data.keyword.codeengineshort}} job by using the `icr.io/codeengine/firstjob` image. This job prints `Hi from a batch job! My index is:`. 

1. Open [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run a container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Specify a container image for your job, for example, `icr.io/codeengine/firstjob`. If you have your own source code that you want to turn into a container image for the job, see [building a container image](/docs/codeengine?topic=codeengine-build-image). For more information about the code that is used for this example, see [`firstjob`](https://github.com/IBM/CodeEngine/tree/main/job){: external}. 
7. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
8. Click **Create**.
9. From your job page, click **Submit job** to submit a job based on the current configuration. 
10. From the Submit job pane, accept all the default values, and click **Submit job** again to run your job. 

From the Submit job pane, you can review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. You can specify either **Number of instances** or **Array indices** for the number of parallel job instances to run. For **Number of instances**, provide the number of instances to run in parallel for this job. For **Array indices**, provide a comma-separated list for your custom set of indices. For example, to run this job with a custom set of `5` indices, specify `3,12-14,25`. After you submit this job, the system displays the status of the instances of your job on the Job details page. If you specify **Number of instances** instead of **Array indices** in the Submit job pane, from the `Configuration` section of the Job details page, this information is provided as **Array indices**.
{: note}

You can find details about your job run on the Job status page.

## Creating a job with the CLI
{: #create-job-cli}

To create a job configuration with the CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

The following **`job create`** command creates a job configuration that is named `myjob` and uses the container image `icr.io/codeengine/firstjob`. 

```txt
ibmcloud ce job create --name myjob  --image icr.io/codeengine/firstjob
```
{: pre}

**Example output**

```txt
Creating job 'myjob'...
OK
```
{: screen}

The following table summarizes the options that are used with the **`job create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.


| Option | Description |
| --- | --- |
| `--image` | The name of the image that is used for runs of the job. This value is required. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `TAG` is not specified, the default is `latest`. For images in [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`, as the default for `REGISTRY` is `docker.io`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. |
| `--name` | The name of the job. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain lowercase letters, numbers, and hyphens (-). |
{: caption="Table 1. Command options" caption-side="bottom"}

After you create your job, you can submit it. See [Run a job](/docs/codeengine?topic=codeengine-run-job).

## Next steps for jobs
{: #nextsteps-jobcreatepub}

After you create your job, you can submit it to [run the job](/docs/codeengine?topic=codeengine-run-job). For more information about jobs, see [Working with jobs](/docs/codeengine?topic=codeengine-job-plan).

Now that you have created your job, you can use event subscriptions to make your jobs event-driven, so that your jobs are triggered by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}



