---

copyright:
  years: 2020, 2024
lastupdated: "2024-12-16"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, batch jobs, batch job workloads, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Batch job workloads
{: #cebatchjobs}


{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads, including batch job or application workloads. Learn about running batch jobs in {{site.data.keyword.codeengineshort}}.
{: shortdesc}


## What are batch job workloads?
{: #batchjob-workloads}

A job in {{site.data.keyword.codeengineshort}} runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit, such that the resources to run the job workload are freed up.

You can scale batch jobs by defining multiple instances. Workloads can be split into parallel tasks to reduce compute time. You can set the job to run with automatic retry to address failing workloads within a job instance. You can trigger batch jobs manually, programmatically, and by events, such as {{site.data.keyword.cos_short}} events.

When you create a job, you can specify the workload configuration information that is used each time that the job is run.

Typical batch job workloads include:

- Machine model training
- Analyzing files, such as voice analysis or image recognition
- Compressing or decompressing files
- Archiving information

When you create a job, you can specify workload configuration information that is used each time that the job is run.

### What is the lifecycle of a batch job?
{: #batchjob-lifecycle}

When you submit a batch job, it runs to completion. Typically, batch jobs retrieve input data, do computational work, and store the results in persistent data stores. When the batch job is completed, resources that are used to run the job are removed and no cost is incurred for any stand-by resources.



## How do jobs compare to applications and functions?
{: #batchjob-compare}

| Characteristic | Application | Job | Function |
| --------- | --------- | --------- | --------- |
| Execution time (duration) | Long-running (10 minutes per request) | Long-running (up to 24 hours) | Short-running (2 minutes or less) |
| Startup latency | Medium | Scheduled start | Low  |
| Termination | Run-continuously | Run-to-completion | Run-to-completion |
| Invocation | On request or permanently running | Scheduled | On request, instant |
| Programming Model | Container-based build and execution | Container-based build and execution | Language-specific source code files and dependency metadata |
| Parallelism | Parallel execution, flexible | Low to medium parallel execution | High parallel execution |
| Scale-out | Based on number of requests | Based on job workload definition | Based on events or direct invocations |
| Optimized for | Long running, highly complex workload and on-demand scale-out | Scheduled or planned workloads with high resource demands | Startup time and rapid scale-out |
{: caption="Comparing {{site.data.keyword.codeengineshort}} applications, jobs, and functions" caption-side="bottom"}

For more information, see [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

## What are the key features of working with {{site.data.keyword.codeengineshort}} batch jobs?
{: #batchjob-features}

Review the following topics to learn more about working with batch jobs in {{site.data.keyword.codeengineshort}}.

* [Isolation](#batchjob-isolation)
* [Logging](#batchjob-logs)
* [Queuing](#batchjob-queue)
* [Retries](#batchjob-retries)
* [Running batch jobs](#batchjob-run)
* [Scaling](#batchjob-scaling)
* [Status](#batchjob-status)
* [Submitting similar batch jobs](#batchjob-reuse)
* [Triggering batch jobs with events](#batchjob-eventing)


### Isolation
{: #batchjob-isolation}

{{site.data.keyword.codeengineshort}} is a multi-tenant, regional service where tenants share the same network and compute infrastructure. In particular, the network and compute infrastructure are shared resources and some management components are common to all tenants. However, tenants and their workloads are isolated from each other by using {{site.data.keyword.codeengineshort}} projects.  {{site.data.keyword.codeengineshort}} prevents communication between projects, providing isolation to your applications inside a multi-tenant environment. In addition, there are access controls that are performed on a resource level to allow only authorized users to perform certain operations on project resources, such as applications or other {{site.data.keyword.codeengineshort}} workloads.

For more information about workload isolation, see [{{site.data.keyword.codeengineshort}} workload isolation](/docs/codeengine?topic=codeengine-architecture#workload-isolation).

### Logging
{: #batchjob-logs}

When you work with {{site.data.keyword.codeengineshort}} jobs in the console with logging enabled, logs are forwarded to an {{site.data.keyword.logs_full_notm}} service instance that is associated with your {{site.data.keyword.codeengineshort}} project. In the {{site.data.keyword.logs_full_notm}} service instance, the logs are indexed, enabling full-text search through all generated messages and convenient querying based on specific fields. See [Getting logs for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-gettinglogs).

System event information can also be helpful to troubleshoot problems when you run jobs. You can view system event information with the CLI. See [Getting system event information for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent).

For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-logging).

### Queuing
{: #batchjob-queue}

Submitted batch jobs are automatically queued and are in a pending state until dispatched. Batch jobs are run based on the available compute resources as defined by your {{site.data.keyword.codeengineshort}} project. Batch jobs that are in a `pending` status can be removed from the queue. You can monitor batch jobs that are pending, running, or completed by using the {{site.data.keyword.codeengineshort}} console or command-line interface.

### Retries
{: #batchjob-retries}

Each job instance runs to completion. However, the workload code might encounter an error during the job run. When a job instance completes with a nonzero return code, {{site.data.keyword.codeengineshort}} restarts the job instance. With {{site.data.keyword.codeengineshort}}, you can specify to limit the number of retries to avoid restarting failed job instances.

### Running batch jobs
{: #batchjob-run}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides a streamlined way for you to run your code as a job.

You can create and run batch jobs in {{site.data.keyword.codeengineshort}} in the following ways:

* Run an existing container image. Create a job and provide a reference to your image to use when you submit the job. For an example, see [Create and run a job](/docs/codeengine?topic=codeengine-getting-started#first-job).
* Start with source code. If you are starting with source code that is located in a Git repository or on your local workstation, you can point to the location of your source and {{site.data.keyword.codeengineshort}} takes care of building the image for you. See [Create a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code) and [Create a job from local source code](/docs/codeengine?topic=codeengine-job-local-source-code).

For more information, see [Working with jobs](/docs/codeengine?topic=codeengine-job-plan).


### Scaling
{: #batchjob-scaling}

A job in {{site.data.keyword.codeengineshort}} (batch job) consists of one or more job instances. While job instances run independent of each other, they run the same code. Suppose you have a database with 100 records to analyze. You can run your job such that each job instance analyzes 10 records each. For example, the first job instance analyzes records 0 - 9, the second job instance can analyze records 10 - 19, and so on. In this example, each job instance receives the system provided job input parameter `JOB_INDEX` as an environment variable that you can use to calculate the range of database records to analyze by each job instance. The number of job instances is specified when the batch job is submitted.


When you run a batch job, during the startup time, job instances might linger in a pending state as the instances are being started. Pending times for job instances can vary due to the system and network infrastructure, as the system adjusts to fulfill the resource demands related to this run of the job. If the system infrastructure is responding to a high usage demand, the result might be a multi-minute delay of the startup for jobs because job instances are provisioned just-in-time.
{: note}



### Status
{: #batchjob-status}

A batch job is in the `Succeeded` status when all job run instances are completed.

A batch job is in `Failed` status after one or more job run instances reaches the retry limit. Also, if a job takes too long to complete, the job is in `Failed` status whenever the maximum execution time is reached. For more information, see [job status](/docs/codeengine?topic=codeengine-access-job-details#job-status).



### Submitting similar batch jobs
{: #batchjob-reuse}

When you create a job, you can specify workload configuration information that is used each time that the job is run. When you use a common set of configuration information for batch jobs, with {{site.data.keyword.codeengineshort}}, you can specify additional parameters with the job submission to overwrite the batch job parameters for this specific job submission.


### Triggering batch jobs with events
{: #batchjob-eventing}

Batch jobs can be submitted automatically based on events, such as periodic timers, {{site.data.keyword.cos_short}} events, or Kafka topics.

Suppose you want to trigger your batch job automatically based on a subscription to an {{site.data.keyword.cos_full_notm}} bucket that generates events whenever a file changes or is added to the {{site.data.keyword.cos_short}} bucket. Review the [{{site.data.keyword.codeengineshort}} `cos-event-job` sample](https://github.com/IBM/CodeEngine/tree/main/cos-event-job){: external} for information about how to create {{site.data.keyword.cos_short}} events and use the events to trigger batch jobs.

For more information about using eventing with {{site.data.keyword.codeengineshort}} jobs, see the following topics: [Working with the Periodic timer (cron) event producer](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job), [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job), and [Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-job).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## How can I get started with batch jobs?
{: #batchjob-getstart}

To create and run a simple {{site.data.keyword.codeengineshort}} batch job application with the `icr.io/codeengine/firstjob` sample image, see [Running your first {{site.data.keyword.codeengineshort}} job](/docs/codeengine?topic=codeengine-getting-started#first-job).

Also, you can try a batch job tutorial, see [Running and updating jobs](/docs/codeengine?topic=codeengine-run-job-tutorial).

To dive deeper into working with batch jobs, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).
