---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-19"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# Running a job
{: #run-job}

After you create your job, you can run a job based on its definition, or you can run the job with overriding properties. Run your job from the console or with the CLI.
{: shortdesc}

Each time your job runs, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run. 

Submitted batch jobs are run in parallel, if possible. If the number or size of the submitted jobs exceeds the configured quota limits, such as maximum number of running instances, then {{site.data.keyword.codeengineshort}} queues the jobs and delays running them until enough jobs finish. For more information about quotas and limits for jobs, including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Job runs that are created by subscriptions are deleted after 10 minutes. For more information about subscriptions, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events).
{: note}

## Running a job from the console
{: #run-job-ui}

When you create a job, you can run it immediately. However, you can submit and resubmit a job at any time. You can also submit or resubmit a job that you previously created.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select Projects from the navigation menu.
3. Select a project as the current context. 
4. From the Overview page, select Jobs from the Summary section or select Jobs from the navigation menu.
5. Click the name of your job to open the configuration.
6. Click **Submit job** to open the Submit job dialog. Review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
7. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
8. If any of the instances of your job failed to run, click **Rerun failed indices** to run the job again for indices that failed. From the Submit job pane, review and optionally change the configuration values. The **Array indices** field automatically lists the indices of the failed job run instances. After you review and optionally change configuration values, click **Submit job** to run your job.

You can view job logs after you add logging capabilities. For more information, see [viewing logs](/docs/codeengine?topic=codeengine-view-logs).
{: tip}

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [I see configmaps that I didn't create. Can I delete them?](/docs/codeengine?topic=codeengine-configmap#inside-configmaps).
{: note}

## Running a job with the CLI
{: #run-job-cli}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a job](/docs/codeengine?topic=codeengine-create-job#create-job-cli).

To run a job with the CLI, use the **`jobrun submit`** command. For a complete listing of options, see the [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command. 

With the CLI, you can [run a job based on a job configuration](#run-job-cli-withjobconfig) or you can [run a job without first creating a job configuration](#run-job-cli-withoutjobconfig). 

### Running a job with the CLI based on a job configuration 
{: #run-job-cli-withjobconfig}

By creating a job configuration, you can more easily run your job multiple times.

For example, the following **`jobrun submit`** command creates five new instances to run the container image that is specified in the defined `myjob` job configuration. To reference a defined job configuration, use the `--job` option. While the `--name` option is not required if the `--job` option is specified, the following example command specifies the `--name` option to provide a name for this job run. For jobs, the default value for `cpu` is `1` and the default value for `memory` is `4G`. The resource limits and requests are applied per instance, so each instance gets 4 G memory and 1 vCPU. This job allocates 5 \* 4 G = 20 G memory and 5 \* 1 vCPU = 5 vCPUs.

```txt
ibmcloud ce jobrun submit --name testjobrun --job myjob --array-indices "1 - 5"  
```
{: pre}

The following table summarizes the options that are used with the **`jobrun submit`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

| Option | Description |
| --- | --- |
| `--name` | The name of this job run. The `--name` and the `--image` values are required, if you do not specify the `--job` value. Use a name that is unique within the project. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). |
| `--job` | The name of the job to be run. This value is required if you do not specify the `--name`  and `--image` values. |
| `--array-indices` | Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is `0`. |
{: caption="Table 1. Command options" caption-side="bottom"}

The `JOB_INDEX` environment variable is automatically injected into each instance of your job whenever the job is run. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [I see configmaps that I didn't create. Can I delete them?](/docs/codeengine?topic=codeengine-configmap#inside-configmaps).
{: note} 

### Running a job with the CLI without first creating a job configuration 
{: #run-job-cli-withoutjobconfig}

With the CLI, you can submit a job run without first creating a job configuration. You can specify the same configuration options on the `jobrun submit` and `jobrun resubmit` commands that are available with the `job create` command.

For example, the following [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command submits a job run to reference the `us.icr.io/mynamespace/myhello_bld` image by using the `myregistry` access information. Because this job run is not referencing a defined job configuration, you must specify values for the `--name` and `image` options. Use `--name` to specify the name of this job run and use `--image` to provide the name of the image that is used for this job run. The `--array-indices` option creates five new instances to run the container image. For job runs, the default value for `cpu` is `1` and the default value for `memory` is `4G`. The resource limits and requests are applied per instance, so each instance gets 4 G memory and 1 vCPU. This job run allocates 5 \* 4 G = 20 G memory and 5 \* 1 vCPU = 5 vCPUs.

```txt
ibmcloud ce jobrun submit --name myhellojob-jobruna --image us.icr.io/mynamespace/myhello_bld --registry-secret myregistry   --array-indices "1 - 5"  
```
{: pre}

Run the `jobrun get -n myhellojob-jobruna` command to check the job run status. 

Example output

```txt
[...]

Name:          myhellojob-jobruna
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m6s
Created:       2021-06-04T11:56:22-04:00


Image:                us.icr.io/mynamespace/myhello_bld
Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G
Registry Secrets:
    myregistry

Runtime:
    Array Indices:       1 - 5
    Max Execution Time:  7200
    Retry Limit:         3

Status:
    Completed:          9s
    Instance Statuses:
        Succeeded:  5
    Conditions:
        Type      Status  Last Probe  Last Transition
    Pending   True    16s         16s
    Running   True    13s         13s
    Complete  True    9s          9s

Events:
    Type    Reason     Age                Source                Messages
    Normal  Updated    11s (x8 over 18s)  batch-job-controller  Updated JobRun "myhellojob-jobruna"
    Normal  Completed  11s                batch-job-controller  JobRun completed successfully

Instances:
    Name                    Running  Status     Restarts  Age
    myhellojob-jobruna-1-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-2-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-3-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-4-0  0/1      Succeeded  0         18s
    myhellojob-jobruna-5-0  0/1      Succeeded  0         18s
```
{: screen}


Job runs that are submitted (or resubmitted) with the CLI that do not reference a defined job configuration are not viewable from the console. 
{: note}

## Resubmitting your job with the CLI
{: #resubmit-job-cli}

If you want to resubmit a job run based the configuration of a previous job run, use the **`jobrun resubmit`** command. This command requires the name of the previous job run and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command. 
{: shortdesc}

For example, the following **`jobrun resubmit`** command resubmits the `testjobrun` job run. 

```txt
ibmcloud ce jobrun resubmit --jobrun testjobrun 
```
{: pre}

Example output

```txt
Getting job run 'testjobrun'...
Getting job 'myjob'...
Rerunning job run 'myjob-jobrun-fji48'...
Run 'ibmcloud ce jobrun get -n myjob-jobrun-fji48' to check the job run status.
```
{: screen}

For example, the following **`jobrun resubmit`** command resubmits the `myhellojob-jobruna` job run, which was run without first creating the job configuration. Because the referenced job run does not have a related job configuration, you must specify the `--name` option to specify a name this job run. 

```txt
ibmcloud ce jobrun resubmit --jobrun myhellojob-jobruna --name myhellojob-jobrunb
```
{: pre}

Run the `jobrun get -n myhellojob-jobrunb` command to check the job run status. 

Example output

```txt 
Getting jobrun 'myhellojob-jobrunb'...
[...]

Name:          myhellojob-jobrunb
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           3m6s
Created:       2021-06-04T11:56:22-04:00

Image:                us.icr.io/mynamespace/myhello_bld
Resource Allocation:
    CPU:                1
Ephemeral Storage:  400M
Memory:             4G
Registry Secrets:
    myregistry

Runtime:
    Array Indices:       1 - 5
Max Execution Time:  7200
Retry Limit:         3

Status:
    Completed:          91s
Instance Statuses:
    Succeeded:  5
Conditions:
    Type      Status  Last Probe  Last Transition
    Pending   True    96s         96s
    Running   True    92s         92s
    Complete  True    91s         91s

Events:
    Type    Reason     Age                Source                Messages
Normal  Updated    93s (x7 over 97s)  batch-job-controller  Updated JobRun "myhellojob-jobrunb"
Normal  Completed  93s                batch-job-controller  JobRun completed successfully

Instances:
    Name                    Running  Status     Restarts  Age
myhellojob-jobrunb-1-0  0/1      Succeeded  0         97s
myhellojob-jobrunb-2-0  0/1      Succeeded  0         97s
myhellojob-jobrunb-3-0  0/1      Succeeded  0         97s
myhellojob-jobrunb-4-0  0/1      Succeeded  0         97s
myhellojob-jobrunb-5-0  0/1      Succeeded  0         97s
```
{: screen}


Job runs that are submitted (or resubmitted) with the CLI that do not reference a defined job configuration are not viewable from the console. 
{: note}

## Next steps
{: #nextsteps-run-job}

* After you [run your job](/docs/codeengine?topic=codeengine-run-job), to view details of your job and job runs, see [access job details](/docs/codeengine?topic=codeengine-access-job-details).

* Now that your job is created, consider making your jobs event-driven. By using event subscriptions, you can trigger your jobs by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or set your job to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).

* You can [update your job](/docs/codeengine?topic=codeengine-update-job) and its referenced code in *any* of the following ways, independent of how you created or previously updated your job.

    - If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create (or update) your job. You can create (or update) your job from images in a [public registry](/docs/codeengine?topic=codeengine-create-job) or [private registry](/docs/codeengine?topic=codeengine-create-job-private) and then access the referenced image from your job run.

        If you created your job by using the **`job create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your job to point to a different container image, you must first remove the association of the build from your job. For example, run `ibmcloud ce job update -n JOB_NAME --build-clear`. After you remove the association of the build from your job, you can update the job to reference a different image. 
        {: important}


    - If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating (or updating) the job with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-plan-build) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.  

    - If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and creating the job with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-plan-build)) with {{site.data.keyword.codeengineshort}} before you create (or update) your job and run the job.

    For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the job. Then, after the image is matured, you can update the job to reference the specific image that you want. You can repeat this process as needed.

    When you run your updated job, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run. 





Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}




