---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-16"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating a job from repository source code
{: #run-job-source-code}

You can create your job directly from source code that is located in a Git repository with the {{site.data.keyword.codeenginefull}} console and CLI. Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
{: shortdesc}


## Creating your job from repository source code from the console
{: #run-job-source-code-ui}

You can create your job directly from source code with the console. 
{: shortdesc}

Before you begin, [plan for your build](/docs/codeengine?topic=codeengine-plan-build). You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile). Each time that you run the job, the most current version of the dependent build artifacts, including the buildpacks and container image, are used during the build process and are included in the resulting container image.

{{site.data.keyword.codeengineshort}} can automatically push (upload) images to {{site.data.keyword.registrylong}} namespaces in your account and even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private Docker Hub account, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start from source code**.
3. Select **Job**.
4. Enter a name for the job. Use a name for your job that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select a source repository, for example, `https://github.com/IBM/CodeEngine`. Because we are using sample source that does not require credentials, select `None` for the Code repo access. You can optionally provide a branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. Click **Next**. 
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Provide registry information about where to store the image of your build output. Select a container registry location, such as `IBM Registry, Dallas`. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Select an existing **Registry access secret** or create a new one. If you are building your image to an {{site.data.keyword.registrylong_notm}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you.
12. Select a namespace, name, and a tag for your image. If you are building your image to an {{site.data.keyword.registrylong_notm}} instance that is in your account, you can select an existing namespace or let {{site.data.keyword.codeengineshort}} create and manage the namespace for you.
13. Click **Done**.
14. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
15. Click **Create**.
16. After your build run is submitted, the built container image is sent to {{site.data.keyword.registryshort}} and then your job can reference the built image. When the job is ready, click **Submit job** to run the job based on the current configuration.  

Build runs that complete are ultimately automatically deleted. When your build run is based on build configuration, this build run is deleted after 3 hours if the build run is successful. If the build run is not successful, this build run is deleted after 48 hours.  
{: note}

Now that you have created your job and [run your job](/docs/codeengine?topic=codeengine-run-job), you can view details about your job configuration and job runs from your job page.  


Need help? Check out [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Creating your job from repository source code with the CLI
{: #run-job-source-code-cli}

You can create your job directly from repository source code with the CLI. Use the **`job create`** command to both build an image from your Git repository source, and define the configuration for your job.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your Git repository source, automatically uploads the image to your container registry, and then creates your job configuration to reference this built image with the **`job create`** command. You need to provide only a name for the job and the URL to the Git repository if the image is to be located in an {{site.data.keyword.registrylong_notm}} account. In this case, {{site.data.keyword.codeengineshort}} manages the namespace for you. However, if you want to use a different container registry, then you must specify the image and a registry access secret for that container registry. Use the **`ibmcloud ce jobrun submit`** command to run your job that references the built image. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) and [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) commands. 

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

1. Use the **`job create`** command to create the `myjob-repo` job to reference an image that is built from the `https://github.com/IBM/CodeEngine` build source. This command automatically builds the image and uploads the image to an {{site.data.keyword.registrylong}} namespace in your account and job runs for this job reference this built image. By specifying the `--build-context-dir` option, the build uses the source in the `helloworld` directory. This example command uses the default `dockerfile` strategy, and the default `medium` build size. Because the branch name of the repository is not specified with the `--build-commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. By adding the `--wait` option, this specifies for the job create to wait for the image build to complete.  

    ```txt
    ibmcloud ce job create --name myjob-repo --build-source https://github.com/IBM/CodeEngine --build-context-dir helloworld --wait
    ```
    {: pre}

    Example output

    ```txt
    Creating job 'myjob-repo'...
    Submitting build run 'myjob-repo-run-220420-15590196'...
    Creating image 'private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-repo'...
    Waiting for build run to complete...
    Build run status: 'Running'
    Build run completed successfully.
    Run 'ibmcloud ce buildrun get -n myjob-repo-run-220420-15590196' to check the build run status.
    OK
    ```
    {: screen}

    Because we specified the `--wait` option, the output of  the **`job create`** command provides information on the progression of the build run before the job is created.
    {: tip}

    In this example, the built image is uploaded to the `ce--abcde-glxo4kabcde` namespace in {{site.data.keyword.registrylong_notm}}. 

    The following table summarizes the options that are used with the **`job create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `--name` | The name of the job. Use a name that is unique within the project. This value is required. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). | 
    | `--build-source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`. |
    | `--build-context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. |
    | `--wait` | Specifies to wait for the image build to complete before creating the job. |
    {: caption="Table 1. Command description" caption-side="bottom"}

2. (optional) Use the **`job get`** command to display information about your job, including information about the build.

    ```txt
    ibmcloud ce job get --name myjob-repo
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myjob-repo
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
    Age:           2d15h
    Created:       2022-04-14T16:10:11-04:00
    
    Image:                private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-repo

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
      Build Run Name:     myjob-repo-run-220420-15590196
      Build Type:         git
      Build Strategy:     dockerfile-medium
      Timeout:            600
      Source:             https://github.com/IBM/CodeEngine
      Context Directory:  helloworld
      Dockerfile:         Dockerfile

      Build Run Summary:  Succeeded
      Build Run Status:   Succeeded
      Build Run Reason:   All Steps have completed executing
      Run 'ibmcloud ce buildrun get -n myjob-repo-run-220420-15590196' for details.
      ```
    {: screen}


3. Now that your job is created and your image is built, run your job that references the built image. This example command runs the `myjobrun-repo` job run based on the `myjob-repo` job configuration.  

    ```txt
    ibmcloud ce jobrun submit --name myjobrun-repo --job myjob-repo
    ```
    {: pre}

4. (optional) View the details of your job run. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun-repo 
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
    
    Job Ref:              myjob-repo
    Image:                private.us.icr.io/ce--abcde-glxo4kabcde/job-myjob-repo
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
      Completed:          90s
      Instance Statuses:
        Succeeded:  1
      Conditions:
        Type      Status  Last Probe  Last Transition
        Pending   True    101s        101s
        Running   True    91s         91s
        Complete  True    90s         90s

    Events:
      Type    Reason     Age                 Source                Messages
      Normal  Updated    91s (x4 over 102s)  batch-job-controller  Updated JobRun "myjobrun-repo"
      Normal  Completed  91s                 batch-job-controller  JobRun completed successfully

    Instances:
      Name               Running  Status     Restarts  Age
      myjobrun-repo-0-0  0/1      Succeeded  0         102s
    ```
    {: screen}

Now that your job is created and run from from repository source code, you can update the job to meet your needs by using the [**`ibmcloud ce job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command. For more information about updating jobs, see [Updating a job](/docs/codeengine?topic=codeengine-update-job). If you want to update your source to use with your job, you must provide the `--build-source` option on the **`job update`** command.

When your job is created from repository source code or from [local source](/docs/codeengine?topic=codeengine-job-local-source-code) with the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted.  Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.
{: note}

## Next steps
{: #nextsteps-jobcreatesource}

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

