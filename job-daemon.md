---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-09"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating and running a job that runs indefinitely
{: #job-daemon}

Learn how to create and run a {{site.data.keyword.codeengineshort}} job that can run indefinitely and does not time out.
{: shortdesc}

Typically, jobs are designed to run one time and exit with a maximum execution time.

However, suppose that you want to constantly poll a third-party data store. You can choose to create an application; however, the app port must remain open to handle HTTP requests. Instead, if you don't want to service HTTP requests, you can choose to create a job that runs without a maximum execution time and does not time out.

With {{site.data.keyword.codeengineshort}}, you can choose the mode of your job. Use the default `task` mode for jobs where a maximum execution time applies. For these jobs, failed instances are restarted per the job retries limit.

If you want to create a job that can run indefinitely and does not time out, use `daemon` mode for your jobs. With this mode, runs of the job do not time out and any failed instances are automatically restarted indefinitely.

When you use `daemon` mode to run jobs, if you want {{site.data.keyword.codeengineshort}} to automatically restart the job if there's a failure, make sure that your code stops with a nonzero exit code. If the container image that is associated with your daemon job ends with a `0` exit code, then {{site.data.keyword.codeengineshort}} assumes that the job was stopped intentionally, and the job is not restarted. However, if the job fails for an unexpected reason, and the container image that is associated with your daemon job exits with a nonzero exit code, then {{site.data.keyword.codeengineshort}} automatically restarts the daemon job. See [Why does my daemon job not automatically restart](/docs/codeengine?topic=codeengine-ts-jobrun-daemon)?

With {{site.data.keyword.codeengineshort}}, you pay for only the resources that you use. When your job runs in `daemon` mode, be aware that the job is always running until you delete the job.
{: important}

## Creating and running a job that runs indefinitely from the console
{: #job-daemon-ui}


This example uses the [{{site.data.keyword.codeenginefull_notm}} samples](https://github.com/IBM/CodeEngine){: external}; in particular, the `helloworld` sample. When you create a job that references the `icr.io/codeengine/helloworld` sample, and you also specify the mode as `daemon`, this job runs without a maximum execution time and failed instances are restarted indefinitely. If mode is not specified, by default, the job runs in `task` mode.
{: note}

1. Create your job
    1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
    2. Select **Let's go**.
    3. Select **Job**.
    4. Enter a name for the job; for example, `myjob`.
    5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
    6. Choose the code to run. You can create your job from an image in a [public registry](/docs/codeengine?topic=codeengine-create-job), [private registry](/docs/codeengine?topic=codeengine-create-job-private), or in [{{site.data.keyword.registrylong_notm}}](/docs/codeengine?topic=codeengine-create-job-crimage). You can also create your job from [repository](/docs/codeengine?topic=codeengine-run-job-source-code) or [local](/docs/codeengine?topic=codeengine-job-local-source-code) source code. For this example, use the {{site.data.keyword.codeengineshort}} sample image, `icr.io/codeengine/helloworld`.
    7. In the **Resources & scaling** section, specify `daemon` for the mode in the **Resiliency settings**. When you specify `daemon` mode, job runs for this job can run indefinitely, and they do not time out. There is no retry limit for these job runs. Any job runs for these jobs are automatically restarted without limit.
    8. Click **Create** to create the job.

2. From the **Jobs** page, click the **Jobs** tab to view a list of defined jobs. Click the name of your job to open the configuration.

3. Run the job.
    1. Click **Submit job** to open the Submit job dialog. Review and optionally change default configuration values such as instances, CPU, memory, number of job retries, and job timeout. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
    2. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. If any of the instances of your job failed to run, these instances are automatically retried indefinitely.

4. (optional) View logs of the job run. From the console, you can [view job logs](/docs/codeengine?topic=codeengine-logging#view-joblogs-ui) for your job runs. Notice in the log output for the `helloworld` sample, that the `JOB_MODE` environment variable displays the mode of the job.



## Creating and running a job that runs indefinitely with the CLI
{: #job-daemon-cli}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

This example uses the [{{site.data.keyword.codeenginefull_notm}} samples](https://github.com/IBM/CodeEngine){: external}; in particular, the `helloworld` sample. When you create a job that references the `icr.io/codeengine/helloworld` sample, and you also specify `--mode daemon`, this job runs without a maximum execution time and failed instances are restarted indefinitely. If mode is not specified, by default, the job runs in `task` mode.
{: note}


1. Create the `myjob-daemon` job, which uses the sample image `icr.io/codeengine/helloworld`. To run this sample image as a job in `daemon` mode, specify `--mode daemon`.

    ```txt
    ibmcloud ce job create --name myjob-daemon --image icr.io/codeengine/helloworld --mode daemon
    ```
    {: pre}


    Example output

    ```txt
    Creating job 'myjob-daemon'...
    ```
    {: screen}


    The following table summarizes the options that are used with the **`job create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `--name` | The name of the job. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). |
    | `--image` | The name of the image that is used for runs of the job.  |
    | `--mode` | The mode for runs of the job. Valid values are `task` (default) and `daemon`. In `daemon` mode, there is no timeout value and failed instances are restarted indefinitely. |
    {: caption="Command description" caption-side="bottom"}

2. (optional) Use the **`job get`** command to display information about your job.

    ```txt
    ibmcloud ce job get --name myjob-daemon
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myjob-daemon
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           2d15h
    Created:       2022-04-14T16:10:11-04:00

    Image:                icr.io/codeengine/helloworld
    Resource Allocation:
      CPU:     1
      Memory:  4G

    Runtime:
        Mode:                  daemon
        Array Indices:         0
        Array Size:            1
        Max Execution Time:    7200
        Retry Limit:           3
    [...]
    ```
    {: screen}

3. Run your job. This example command runs the `myjobrun-daemon` job run that is based on the `myjob-daemon` job configuration.

    ```txt
    ibmcloud ce jobrun submit --name myjobrun-daemon --job myjob-daemon
    ```
    {: pre}

4. (optional) View the details of your job run.

    ```txt
    ibmcloud ce jobrun get --name myjobrun-daemon
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun-daemon'...
    Getting instances of jobrun 'myjobrun-daemon'...
    Getting events of jobrun 'myjobrun-daemon'...
    For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-job.
    Run 'ibmcloud ce jobrun events -n myjobrun-daemon' to get the system events of the job run instances.
    Run 'ibmcloud ce jobrun logs -f -n myjobrun-daemon' to follow the logs of the job run instances.
    OK

    Name:          myjobrun-daemon
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           2d15h
    Created:       2022-04-14T16:10:11-04:00

    Job Ref:              myjob-daemon
    Image:                icr.io/codeengine/helloworld
    Resource Allocation:
      CPU:                1
      Ephemeral Storage:  400M
      Memory:             4G

    Runtime:
        Mode:                  daemon
        Array Indices:         0
        Array Size:            1
        JOP_ARRAY_SIZE Value:  1
        Max Execution Time:    7200
        Retry Limit:           3

    Status:
      Instance Statuses:
        Running:  1
      Conditions:
        Type     Status  Last Probe  Last Transition
        Pending  True    27s         27s
        Running  True    4s          4s

    Events:
      Type    Reason   Age               Source                Messages
      Normal  Updated  4s (x3 over 26s)  batch-job-controller  Updated JobRun "myjobrun-daemon"

    Instances:
      Name                 Running  Status   Restarts  Age
      myjobrun-daemon-0-0  1/1      Running  0         26s
    ```
    {: screen}

5. (optional) View logs for the job run. With the CLI, you can [view job logs](/docs/codeengine?topic=codeengine-logging#view-joblog-cli) for all instances of a job run or for a particular job run instance. The following example displays job logs for all instances of the `myjobrun-daemon` job run.

    ```txt
    ibmcloud ce jobrun logs --name myjobrun-daemon
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of job run 'myjobrun-daemon'...
    Getting jobrun 'myjobrun-daemon'...
    Getting instances of jobrun 'myjobrun-daemon'...
    OK

    myjobrun-daemon-0-0/myjob-daemon:
    Hello from helloworld! I'm a batch job! Index: 0

    Hello World from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    CE_DOMAIN=us-south.codeengine.appdomain.cloud
    CE_JOB=myjob-daemon
    CE_JOBRUN=myjobrun-daemon
    CE_SUBDOMAIN=glxo4k7nj7d
    HOME=/root
    HOSTNAME=myjobrun-daemon-0-0
    JOB_INDEX=0
    JOB_MODE=daemon
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    z=Set env var 'SHOW' to see all variables
    ```
    {: screen}

Now that your job is created in `daemon` mode, the job runs indefinitely. Because there is no timeout and failed instances are restarted indefinitely, the `--maxexecutiontime` and `--retrylimit` options are not allowed when you run a job in `daemon` mode.

Notice that the `JOB_MODE` environment variable displays the mode of the runs of the job.


## Stopping a job that runs indefinitely
{: #job-daemon-stop}

When you run a job in `daemon` mode, it can run indefinitely, since it runs without a maximum execution time and any failed instances are automatically retried indefinitely. To stop a job that is in `daemon` mode, delete the specific job run or delete the job.


### Stopping a job that runs indefinitely from the console
{: #job-daemon-stop-ui}

* To delete a specific job run, go to the job page for your specific job. Go to the **Job runs** tab. Delete the job run that you want to remove.

* To delete a job, go to the Jobs page, click the name of the job that you want to remove. Deleting a job deletes the job, its configuration, and any job runs associated with the job.

### Stopping a job that runs indefinitely with the CLI
{: #job-daemon-stop-cli}

* To delete a specific job run with the CLI, use the [**`jobrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-delete) command. You can optionally use the `-f` option to force the delete of a job run without confirmation.

    ```txt
    ibmcloud ce jobrun delete --name myjobrun-daemon -f
    ```
    {: pre}

    Example output

    ```txt
    Deleting job run 'myjobrun-daemon'...
    OK
    ```
    {: screen}


* To delete a job with the CLI, use the [**`job delete`**](/docs/codeengine?topic=codeengine-cli#cli-job-delete) command. You can optionally use the `-f` option to force the delete of a job without confirmation. When you delete a job, any job runs for this job are also deleted.  The following example deletes the `myjob-daemon` job,

    ```txt
    ibmcloud ce job delete --name myjob-daemon -f
    ```
    {: pre}


    Example output

    ```txt
    Deleting job 'myjob-daemon'...
    OK
    ```
    {: screen}
