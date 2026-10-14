---

copyright:
  years: 2026
lastupdated: "2026-10-13"

keywords: jobs in code engine, batch jobs in code engine, copy create job in code engine, job workloads in code engine, deploying workloads in code engine, job, copy, duplicate, clone

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Copying a {{site.data.keyword.codeengineshort}} job to create a new job
{: #job-copycreate}

With {{site.data.keyword.codeenginefull}}, you can create a new job by copying the configuration of an existing job. The *copy create* feature duplicates all configuration settings of a source job — including the container image reference, resource allocation, environment variables, and runtime settings — into a new job that you can then customize independently.
{: shortdesc}

The new job is created as a separate, independent workload. Changes to the original job after copying do not affect the new job, and vice versa.

Before you begin, make sure that an existing job is already created in your project.

## What is copied when you use copy create?
{: #job-copycreate-what-is-copied}

When you copy a job to create a new job, the following configuration is copied from the source job to the new job.

| Configuration | Description |
| --- | --- |
| Container image | The image reference, including the registry, namespace, repository, and tag. |
| Registry secret | The registry secret that is used to pull the container image, if specified. |
| Resource allocation | The CPU and memory that are assigned to the job. See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). |
| Environment variables | All literal environment variables and references to secrets and configmaps. See [Working with environment variables](/docs/codeengine?topic=codeengine-envvar). |
| Runtime settings | The number of job instances, array indices, maximum execution time, and retry limit. See [Running a job](/docs/codeengine?topic=codeengine-run-job). |
| Commands and arguments | Any commands and arguments that override the container image entrypoint. See [Defining commands and arguments for your {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-cmd-args). |
{: caption="Configuration that is copied when you use copy create" caption-side="bottom"}

The new job is assigned the name that you specify. It is not run automatically after it is created.

Build source configuration (repository or local source builds) is **not** copied to the new job.
{: note}

## Copying a job from the console
{: #job-copycreate-console}

You can create a new job by copying the configuration of an existing job with the {{site.data.keyword.codeengineshort}} console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. Click **Jobs**, then click the **Jobs** tab to open a list of your jobs.
3. Select one of the following ways to click **Create copy**:
    * Click the name of the job that you want to copy to open its job page. Then click the **dropdown chevron** in the upper right corner of the page and select **Create copy**.
    * In the jobs list, click the row actions icon (⋮) of the job that you want to copy and select **Create copy**.
4. On the Create job page, the configuration of the source job is pre-populated. Enter a unique name for the new job. Use a name that is unique within the project.
5. Review and optionally modify any configuration settings for the new job, such as the container image, resource allocation, or environment variables.
6. Click **Create** to create the new job.

The new job behaves as an independent workload. The source job is not affected by any changes to the new job, and vice versa.

## Running a copied job
{: #job-copycreate-run}

After the new job is created, you can submit it as a job run in the same ways as any other {{site.data.keyword.codeengineshort}} job.

For more information about running a job, see [Running a job](/docs/codeengine?topic=codeengine-run-job).

## Updating a copied job
{: #job-copycreate-update}

After the new job is created, you can update it in the same ways as any other {{site.data.keyword.codeengineshort}} job.

For more information about updating a job, see [Updating a job](/docs/codeengine?topic=codeengine-update-job).
