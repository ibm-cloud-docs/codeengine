---

copyright:
  years: 2022
lastupdated: "2022-03-25"

keywords: limits for code engine, limitations for code engine, quotas for code engine, project quotas in code engine, app limits in code engine, job limits in code engine, limits, limitations, quotas

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Limits and quotas for {{site.data.keyword.codeengineshort}}
{: #limits}

The following sections provide technical details about the {{site.data.keyword.codeenginefull}} limitation and quota settings.
{: shortdesc}

**How does my resource allocation affect my project quotas and billing?**

From the console, you can view information about your current {{site.data.keyword.codeengineshort}} resource allocation from your project overview page. If you want to display information about the allocated memory and vCPU values based on what you have configured for each specific application or job, then view the listing of your applications or jobs in your project. With the CLI, you can also get information about your current resource allocation usage for the project with the [**`project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command. 

With {{site.data.keyword.codeengineshort}}, you pay for only the resources that you use based on the configured memory and vCPU that your workloads consume, as well as any incoming HTTP calls. If your app scales to zero or your job or build isn't running, you are not consuming resources and so you are not charged. To host all your applications and jobs, {{site.data.keyword.codeengineshort}} deploys and manages the necessary infrastructure for you. However, while you are not billed for this infrastructure, it does count toward the project quotas. See the following tables for more information on project quotas.

## Project quotas
{: #project_quotas}

The maximum number of projects that you can create per region is 20. 

The maximum number of projects includes projects that are active and any projects that are not permanently deleted. When you delete a project, the project is soft deleted and can be restored within 7 days before it is permanently deleted. Use the console or the CLI to display soft-deleted projects. For more information, see [deleting a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).
{: important}

The following table lists the quotas for projects.

| Category  |   Description      | 
| --------- | -----------        | 
| Apps | You are limited to 20 apps per project. |
| App revisions | You are limited to a total of 60 revisions for all apps per project. |
| Builds | You are limited to 100 build configurations per project. |
| Build runs | You are limited to 100 build runs per project before you need to remove or clean up old ones. |
| Configmaps | You are limited to 100 configmaps per project. |
| CPU | The total combination for all the apps and jobs cannot exceed 64 vCPUs. |
| Ephemeral storage | The total combination for all the apps and jobs cannot exceed 256 G of ephemeral storage. |
| Instances (active) | The number of app instances, running job instances, and running build instances cannot exceed 250. |
| Instances (total)  | The number of active instances and the number of completed job and build instances cannot exceed 2500. |
| Jobs | You are limited to 100 jobs per project. |
| Job runs | You are limited to 100 job runs per project before you need to remove or clean up old ones. |
| Memory | The total combination for all the apps and jobs cannot exceed 256 G of memory. |
| Secrets | You are limited to 100 secrets per project. |
| Subscriptions ({{site.data.keyword.cos_full_notm}}) | You are limited to 100 ({{site.data.keyword.cos_short}}) subscriptions per project. |
| Subscriptions (Periodic timer (cron)) | You are limited to 100 periodic timer (cron) subscriptions per project. |
{: caption="Project quotas"}




## Application limits and defaults
{: #limits_application}

The following table lists the limits for applications.

| Category                    |         Minimum         |         Maximum           |        Default         |
| --------------------------- | ----------------------- | ------------------------- | ---------------------- |
| CPU                         |                   0.125 |                       8.0 |                    1.0 |
| Ephemeral storage           |                       40 M |                      32 G |                  400 M |
| Max scale                   |                       0 |                       250 |                     10 |
| Memory                      |                   0.25 G|                      32 G |                    4 G |
| Min scale                   |                       0 |                       250 |                      0 |
| Concurrency                 |                       1 |                      1000 |                    100 |
| Timeout                     |                       0 |                600 seconds|            300 seconds |
{: caption="Application limits"}

{{site.data.keyword.codeengineshort}} does not support overcommitment for application resources. Therefore, if you create an application by using the API or with `kubectl apply -f <yaml>`, the values for `Resource.Requests` and `Resource.Limits` for `CPU`, `Memory`, and `Ephemeral Storage` must be specified and must be the same. 

For more information about supported CPU and memory combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).


## Job limits and defaults
{: #limits_job}

Job definitions, as templates for jobs, reflect the same limits as jobs. 

The following table lists the limits for jobs. 

| Category                    |    Minimum    |         Maximum           |        Default         |
| --------------------------- | ------------- | ------------------------- | ---------------------- |
| Array - Array indices        |             0 |                   9999999 |                      0 |
| Array - Number of instances  |             1 |                      1000 |                      1 |
| CPU                         |         0.125 |                       8.0 |                    1.0 |
| Ephemeral storage           |             40 M |                      32 G |                  400 M |
| Memory                      |        0.25 G |                      32 G |                    4 G |
| Retries                     |             0 |                         5 |                      3 |
| Timeout                     |      1 second |  43200 seconds (12 hours) | 7200 seconds (2 hours) |
{: caption="Job limits"}

*Array indices* are comma-separated lists or hyphen-separated range of indices, which specifies the job instances to run; for example, `1,3,6,9` or `1-5,7-8,10`. 

*Number of instances* is the number of job instances to run in parallel. 

For more information about supported CPU and memory combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

### Job size limit
{: #job_size_limit}

{{site.data.keyword.codeengineshort}} limits the size of jobs and job runs with a maximum of 10 KiB. When you create or update jobs and job runs with the console, CLI, or API, {{site.data.keyword.codeengineshort}} checks the size of the job or job run. If the operation exceeds the limit, a size limit exceeded error is given. If you receive this error, try reducing the size of your job or job run in one of the following ways:

* If you use commands and arguments, try reducing the use of these options, make them shorter, or move them into the container image that is used by your job or job run. 

* If you use environment variables, try to use fewer environment variables or make them shorter. You can use secrets or configmaps to define environment variables and import them into the job by using the `--env-from-secret` or `--env-from-configmap` options with the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), and [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

For more information about troubleshooting jobs, see [Troubleshooting - Why can't I submit a job run?](/docs/codeengine?topic=codeengine-ts-jobrun-submit-fails-cli)

## Periodic timer (cron) subscription limits
{: #subscription-cron-limit}

{{site.data.keyword.codeengineshort}} limits the size of data for Periodic timer (cron) events with a maximum of 4096 bytes. When you create or update periodic timer (cron) events, {{site.data.keyword.codeengineshort}} checks the size of the cron event data. If the Periodic timer (cron) event data exceeds the limit, a size limit exceeded error is given. If you receive this error, try reducing the cron event data size to less than 4096 bytes. 

For more information about troubleshooting subscriptions, see [Debugging subscriptions](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions).

## Increasing limits
{: #increase-limits}

Limit values are fixed, but can be increased by [contacting IBM support and creating a support case](/docs/codeengine?topic=codeengine-get-support).


