---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-17"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with jobs and job runs
{: #job-plan}

Learn how to run jobs in {{site.data.keyword.codeenginefull}}. A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.
{: shortdesc}

Before you begin

* If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
* If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} job component.

{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Batch CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-batch).

## How do I make my code run as a {{site.data.keyword.codeengineshort}} job component?
{: #job-containerimage}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides a streamlined way for you to run your code as a job.

- If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create your job. You can create your job from images in a [public registry](/docs/codeengine?topic=codeengine-create-job) or [private registry](/docs/codeengine?topic=codeengine-create-job-private) and then access the referenced image from your job run.

- If you are starting with source code that is located in a Git repository, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the image from your source and creating the job with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create your job and run the job.  

- If you are starting with source code on a local workstation, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the image from your source and creating the job with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create your job and run the job.

After you create and run your job, you can also [update your job](/docs/codeengine?topic=codeengine-update-job) by using *any* of the preceding ways, independent of how you created or previously updated your job.

When you work with jobs, keep in mind the following key things.

* Unlike application images, job images do not have an HTTP Server.
* The executable program in the image must exit with a code of zero to be considered successful.
* Your image can be downloaded from either a public or private image registry. For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

When you run your job, the latest version of your referenced container image is used for the job run, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the job run.


## Considerations for HTTP handling
{: #considerationshttphandlingjob}

When you are working with jobs (or apps), it is helpful to be aware of basic HTTP handling in {{site.data.keyword.codeengineshort}}. See [Considerations for HTTP handling](/docs/codeengine?topic=codeengine-application-workloads#considerationshttphandlingapp)

## Options for creating and running a job
{: #job-options}

Learn about the options that you can specify when you create or run your job. Note that options can vary between the console and the CLI.
{: shortdesc}

### Memory and CPU for jobs
{: #job-options-combo}

When you deploy your job, you can specify the amount of memory, and CPU that your job can consume. These amounts can vary, depending on if your job is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

By default, your job is assigned 4 G of memory and 1 vCPU. For more information about selecting memory and CPU, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

### Creating and running a job with commands and arguments
{: #job-cmd-args}

You can define commands and arguments for your job to use at run time when you create or run your job. 
{: shortdesc}

You can add commands and arguments to your job by using the CLI or the console.

To add commands and arguments through the console, use the `Command` and `Arguments` fields.

To add commands and arguments by using the CLI, add the `--cmd` and `--args` options to your [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) or your [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command.

For more information about defining commands and arguments, see [Defining commands and arguments for your Code Engine workloads](/docs/codeengine?topic=codeengine-cmd-args).

### Creating and running a job with environment variables 
{: #job-option-envvar}

You can define and set environment variables as key-value pairs that can be used by your job at run time. 
{: shortdesc}

You can define environment variables when you create your job, or when you update an existing job from the console or with the CLI. You can create environment variables for your jobs that fully reference a configmap (or secret) or reference individual keys in a configmap (or secret). 

For more information about defining environment variables, see [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

### Creating and running a job with secrets and configmaps 
{: #job-option-secconfigmap}

In {{site.data.keyword.codeengineshort}}, secrets and configmaps can be used by your job by using environment variables. 
{: shortdesc}

Both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

Your job can use environment variables to fully reference a configmap (or secret) or reference individual keys in a configmap (or secret).

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#configmap-ref).


## What if I want my job to run indefinitely?
{: #job-indefinite}

Typically, jobs are designed to run one time and exit with a maximum execution time.

However, suppose that you want to constantly poll a third-party data store. You can choose to create an application; however, the app port must remain open to handle HTTP requests. Instead, if you don't want to service HTTP requests, you can choose to create a job that runs without a maximum execution time and does not time out.

With {{site.data.keyword.codeengineshort}}, you can choose the `mode` of your job. For jobs where a maximum execution time applies, use `task` mode for your jobs. Failed instances are restarted per the job retries limit. This mode is the default behavior for jobs.

If you want to create a job that can run indefinitely and does not time out, use `daemon` mode for your jobs. Failed instances are automatically restarted indefinitely.

With {{site.data.keyword.codeengineshort}}, you pay for only the resources that you use. When your job runs in `daemon` mode, be aware that the job is always running until you delete the job. 
{: important}

For more information, see [Creating and running a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon) commands.




