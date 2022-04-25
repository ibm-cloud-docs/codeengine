---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-25"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating your job from local source code with the CLI
{: #job-local-source-code}

You can create your job directly from source code on your local workstation with the {{site.data.keyword.codeenginefull}} CLI. Use the **`job create`** command to both build an image from your local source, and define the configuration for your job to reference this built image. 
{: shortdesc}

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and {{site.data.keyword.codeengineshort}} automatically uploads the image to an {{site.data.keyword.registrylong}} namespace in your account, and then creates your job to reference this built image. Note that you can only target {{site.data.keyword.registrylong_notm}} for your local builds. For this scenario, you only need to provide a name for the job and the path to the local source. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command. 

You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. The source image is created in the same namespace as your build image.

The {{site.data.keyword.registrylong}} is required for this scenario.
{: important}

Before you begin, your source must be in an accessible location on your local machine. 

This example uses the `https://github.com/IBM/CodeEngine` samples; in particular, the `helloworld` sample. 

1. Download the `https://github.com/IBM/CodeEngine` sample source to your local workstation with the following command.

    ```txt
    git clone https://github.com/IBM/CodeEngine
    ```
    {: pre}

2. Change to the `CodeEngine\helloworld` directory. 

3. From the `CodeEngine\helloworld` directory, create the `myjob-local` job, which uses an image that is built from the `CodeEngine\helloworld` source on your local workstation. This command automatically builds and pushes the image to a {{site.data.keyword.registrylong_notm}} namespace in your account. If you do not have an existing {{site.data.keyword.registryshort}} namespace, {{site.data.keyword.codeengineshort}} automatically creates one for you. By adding the `--wait` option, this specifies for the job create to wait for the image build to complete. 

    ```txt
    ibmcloud ce job create --name myjob-local --build-source . --wait
    ```
    {: pre}

    The `.` indicates the build source is located in your current working directory. 
    {: note}


    Example output

    ```txt
    Creating job 'myjob-local'...
    Creating build 'myjob-local-build-220420-150457582'...
    Packaging files to upload from source path '.'...
    Submitting build run 'myjob-local-run-220420-150457582'...
    Creating image 'private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-local'...
    Waiting for build run to complete...
    Build run status: 'Running'
    Build run completed successfully.
    Run 'ibmcloud ce buildrun get -n myjob-local-run-220420-150457582' to check the build run status.
    OK
    ```
    {: screen}

    Because we specified the `--wait` option, the output of the **`job create`** command provides information on the progression of the build and build run before the job is created.
    {: tip}

    In this example, the built image is uploaded to the `ce--abcde-glxo4kabcde` namespace in {{site.data.keyword.registryshort}}. 

    The following table summarizes the options that are used with the **`job create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `--name` | The name of the job. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). | 
    | `--build-source` | The path to the local source. |
    | `--wait` | Specifies to wait for the image build to complete before creating the job. |
    {: caption="Table 1. Command description" caption-side="bottom"}

4. (optional) Use the **`job get`** command to display information about your job, including information about the build.

    ```txt
    ibmcloud ce job get --name myjob-local
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myjob-local
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-04-14T16:10:11-04:00
    
    Image:                private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-local
    Resource Allocation:
      CPU:     1
      Memory:  4G
    Registry Secrets:
      ce-auto-icr-private-us-south

    Runtime:
      Array Indices:       0
      Max Execution Time:  7200
      Retry Limit:         3

    Build Information:
      Build Name:         myjob-local-build-220420-150457582
      Build Run Name:     myjob-local-run-220420-150457582
      Build Type:         local
      Build Strategy:     dockerfile-medium
      Timeout:            600
      Source:             .
      Dockerfile:         Dockerfile

      Build Status:       Succeeded
      Build Reason:       all validations succeeded
      Run 'ibmcloud ce build get -n myjob-local-build-220420-150457582' for details.

      Build Run Summary:  Succeeded
      Build Run Status:   Succeeded
      Build Run Reason:   All Steps have completed executing
      Run 'ibmcloud ce buildrun get -n myjob-local-run-220420-150457582' for details..
    [...]
    ```
    {: screen}

    Instead of building your image from local source and creating your job with a single command, you can choose to build from local source first *before* you create your job. See [Creating a build configuration that pulls source from a local workstation](/docs/codeengine?topic=codeengine-build-image#build-config-local-cli), [Running a build for source from a local workstation](/docs/codeengine?topic=codeengine-build-image#build-run-cli), and [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). 

5. Now that your job is created and your image is built, run your job that references the built image. This example command runs the `myjobrun-local` job run based on the `myjob-local` job configuration. 

    ```txt
    ibmcloud ce jobrun submit --name myjobrun-local --job myjob-local
    ```
    {: pre}

6. (optional) View the details of your job run. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun-local 
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun-local'...
    Getting instances of jobrun 'myjobrun-local'...
    Getting events of jobrun 'myjobrun-local'...
    Run 'ibmcloud ce jobrun events -n myjobrun-local' to get the system events of the job run instances.
    Run 'ibmcloud ce jobrun logs -f -n myjobrun-local' to follow the logs of the job run instances.
    OK

    Name:          myjobrun-local
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-04-14T16:10:11-04:00
    
    Job Ref:              myjob-local
    Image:                private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-local
    Resource Allocation:
      CPU:                1
      Ephemeral Storage:  400M
      Memory:             4G
    Registry Secrets:
      ce-auto-icr-private-us-south

    Runtime:
      Array Indices:       0
      Max Execution Time:  7200
      Retry Limit:         3

    Status:
      Completed:          2m40s
      Instance Statuses:
        Succeeded:  1
      Conditions:
        Type      Status  Last Probe  Last Transition
        Pending   True    2m44s       2m44s
        Running   True    2m40s       2m40s
        Complete  True    2m40s       2m40s

    Events:
      Type    Reason     Age                    Source                Messages
      Normal  Updated    2m41s (x3 over 2m45s)  batch-job-controller  Updated JobRun "myjobrun-local"
      Normal  Completed  2m41s                  batch-job-controller  JobRun completed successfully

    Instances:
      Name                Running  Status     Restarts  Age
      myjobrun-local-0-0  0/1      Succeeded  0         2m45s
    ```
    {: screen}


## Next steps
{: #nextsteps-job-localdeploysource}

1. After you create your job, submit the job to run it. See [Run a job](/docs/codeengine?topic=codeengine-run-job). You can run your job multiple times. 

2. After you [run your job](/docs/codeengine?topic=codeengine-run-job), to view details of your job and job runs, see [access job details](/docs/codeengine?topic=codeengine-access-job-details).

3. You can [update your job](/docs/codeengine?topic=codeengine-update-job) to meet your needs.

4. Now that you have created your job, consider making your jobs event-driven. By using event subscriptions, you can trigger your jobs by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or set your job to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).




Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}



