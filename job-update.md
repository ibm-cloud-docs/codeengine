---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-16"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Updating a job
{: #update-job}

You can make changes to a defined job and run the updated job from the console or with the CLI. Changes to your job might include updating the code container image, code arguments or commands, runtime instance resources, or environment variables.
{: shortdesc}

Each time your job runs, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run. 

Submitted batch jobs are run in parallel, if possible. If the number or size of the submitted jobs exceeds the configured quota limits, such as maximum number of running instances, then {{site.data.keyword.codeengineshort}} queues the jobs and delays running them until enough jobs finish. For more information about quotas and limits for jobs, including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

You can [update your job](/docs/codeengine?topic=codeengine-update-job) and its referenced code in *any* of the following ways, independent of how you created or previously updated your job.


- If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create (or update) your job. You can create (or update) your job from images in a [public registry](/docs/codeengine?topic=codeengine-create-job) or [private registry](/docs/codeengine?topic=codeengine-create-job-private) and then access the referenced image from your job run.


    If you created your job by using the **`job create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your job to point to a different container image, you must first remove the association of the build from your job. For example, run `ibmcloud ce job update -n JOB_NAME --build-clear`. After you remove the association of the build from your job, you can update the job to reference a different image. 
    {: important}

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating (or updating) the job with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.  

- If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating the job with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.

For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the job. Then, after the image is matured, you can update the job to reference the specific image that you want. You can repeat this process as needed.

When you run your updated job, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run. 




## Updating a job from the console
{: #update-job-ui}

When a job is in ready state, you can update the job. Let's update the `myjob` job that you created previously to change the container image from `icr.io/codeengine/firstjob` to `icr.io/codeengine/testjob` and then subsequently update an environment variable. When a request is sent to this `icr.io/codeengine/testjob` sample job, the job reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. For more information about the code that is used for this example, see [`testjob`](https://github.com/IBM/CodeEngine/tree/main/testjob){: external}.

1. Navigate to your job page. 
    * From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project. Click **Jobs** to open a listing of your jobs.   
    * From the Jobs page, click the name of the job that you want to update. 

2. To update the image reference of your job, provide the name of your image or configure an image. Update the name of the image for this job from `icr.io/codeengine/firstjob` to `icr.io/codeengine/testjob`. Click **Save**. 
3. Click **Submit job**.
4. From the Submit job pane, accept all the default values, and click **Submit job** again to run your job.  
5. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the job is `Hello World!`.
6. To update the job again and add an environment variable, navigate to your job page. 
7. Click **Environment variables** to open the tab and then click **Add environment variable**. Add a literal environment variable with the name of `TARGET` with a value of `Sunshine`. The `icr.io/codeengine/testjob` outputs the message, `Hello <value_of_TARGET>!>`.
8. Click **Done**.
9. Click **Save** to save the update to the job. 
10. Click **Submit job** to submit the updated job.
11. From the Submit job pane, this time change the CPU value to one of the valid CPU choices for the specified memory. Notice that you must use [valid memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). Click **Submit job** again to run this job. The system displays the status of your job on the Job details page. Notice the updated CPU value in the `Configuration` section of the job details.
12. By [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui) for this job, the output of the updated job is `Hello Sunshine!`.

## Updating a job with the CLI
{: #update-job-cli}

With the CLI, you can update an existing job configuration or specify your changes on a new job run. 

### Updating a job configuration with the CLI
{: #update-jobconfig-cli}

You can update an existing job configuration with the [**`ibmcloud ce job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command. 

1. Use the **`job update`** command to update the `myjob` job to reference a different image. 

    ```txt
    ibmcloud ce job update --name myjob --image icr.io/codeengine/testjob 
    ```
    {: pre}

    Run the `ibmcloud ce job get -n myjob` command to display details of the updated job.

    Example output

    ```txt
    Name:          myjob
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           3m6s
    Created:       2021-06-04T11:56:22-04:00

    Last Job Run:
        Name:     myjob-jobrun-abcde
        Age:      32d
        Created:  2021-08-06T13:50:02-04:00

    Image:                icr.io/codeengine/testjob
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

    ```txt
    ibmcloud ce jobrun submit --name myjobrun1 --job myjob
    ```
    {: pre}

3. Run **`ibmcloud ce jobrun get -n myjobrun1`** to view details of this job run. Note that the referenced image is `icr.io/codeengine/testjob`, which is based on the updated job configuration.

    Example output

    ```txt
    Getting jobrun 'myjobrun1'...
    Getting instances of jobrun 'myjobrun1'...
    Getting events of jobrun 'myjobrun1'...
    [...]

    Name:          myjobrun1
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           3m6s
    Created:       2021-06-15T11:56:22-04:00

    Job Ref:              myjob
    Image:                icr.io/codeengine/testjob
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

### Updating a job run with the CLI  
{: #update-jobrun-cli}

You can specify changes for a job run with the [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command. The **`jobrun submit`** command resubmits a job run that references a previous job run. 

1. Use the **`jobrun resubmit`** command to resubmit the `myjobrun1` job run and change the array indices from `0` to `1-4`. While the `--name` option is not required for the **`jobrun resubmit`** command, the following example command specifies the `--name` option to provide a name for this job run. 

    ```txt
    ibmcloud ce jobrun resubmit -jobrun myjobrun1 --array-indices "1-4" --name myjobrunresubmit
    ```
    {: pre}

2. Run the `ibmcloud ce jobrun get -n myjobrunresubmit` command to display details of the updated job run. Note that the value of array indices is updated for this job run.

    Example output

    ```txt
    Getting jobrun 'myjobrunresubmit'...
    Getting instances of jobrun 'myjobrunresubmit'...
    Getting events of jobrun 'myjobrunresubmit'...
    [...]

    Name:          myjobrunresubmit2 
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           3m6s
    Created:       2021-06-04T11:56:22-04:00

    Job Ref:              myjob
    Image:                icr.io/codeengine/testjob
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

