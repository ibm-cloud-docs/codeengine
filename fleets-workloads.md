---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-29"

keywords: fleets in code engine, running fleets with code engine, creating fleets with code engine, images for fleets in code engine, fleets, serverless fleets, fleets workloads, fleet run, environment variables, fleet workloads

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Fleets workloads
{: #cefleets}

{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads, including fleet workloads. Learn about running fleets in {{site.data.keyword.codeengineshort}}.
{: shortdesc}


## What are fleets?
{: #fleet-workloads}

A fleet, also called a **serverless fleet**, is a Code Engine compute component that runs one or more instances of user code in parallel to complete a large queue of compute-intensive tasks. Fleets can connect to Virtual Private Clouds to securely interoperate with user data and services. Unlike batch jobs, fleets provide dynamic task queuing and single-tenant isolation, and are compatible with both vCPU and GPUs. 


## How do fleets work?
{: #fleet-how}

Fleets have three principal elements: tasks, instances, and worker nodes. A single task is completed by a single instance of user code, which runs on a worker node. Each worker node can run several tasks concurrently, allowing many tasks to be completed in parallel. When a task is complete, a new instance spins up on the worker node to complete the next available task in the queue. This process repeats on each worker node until all tasks are completed, at which point worker nodes are automatically deprovisioned.  
 

## How are fleets different from jobs?
{: #fleet-v-job}

Unlike batch jobs, which are primarily intended for small to medium sized tasks, fleets are designed to complete large, compute-intensive tasks. Review the table below for specific differences between jobs and fleets.

| Characteristic | Fleets | Jobs |
| -------------- | ---- | ----- |
| Isolation | Single-tenant | Multi-tenant |
| Task size | Large tasks | Small-to-medium sized tasks |
| Implementation | Dynamic queue | Static array  |
| Machine configuration |  Full control over machine profile | No control over machine profile |
| VPC connection | Natively connects to existing VPC | | Requires private path |
{: caption="Comparing {{site.data.keyword.codeengineshort}} Fleets and jobs " caption-side="bottom"}


## What are the key features of working with {{site.data.keyword.codeengineshort}} fleets?
{: #fleet-features}

Review the following topics to learn more about working with fleets in {{site.data.keyword.codeengineshort}}.

### Automatic scaling
{: #fleet-scaling}

With a fleet, you can take advantage of large scale parallelism to complete large, compute-intensive tasks. {{site.data.keyword.codeengineshort}} automatically scales the worker nodes in your fleet to meet resource requirements most efficiently. You can let {{site.data.keyword.codeengineshort}} determine the profiles of the workers that are deployed, or you can choose a specific profile, such as a GPU type. In either case, {{site.data.keyword.codeengineshort}} automatically scales the number of workers for the greatest level of efficiency. 

The number of workers deployed is based on the number of tasks to complete, the resources required for an instance of your code, and the maximum number of concurrent instances you want to run at a time. By adjusting these settings, you can scale your fleet to complete as few as 1 or as many as several million tasks. 

For example, imagine you have 4 tasks to complete. Each instance of code to complete a task requires `1 vCPU and 2 GB memory`, for a total requirement of `4 vCPU and 8GB memory`. If you set the maximum number of concurrent instances to 2, {{site.data.keyword.codeengineshort}} can deploy 1 worker node with `2 vCPU and 4 GB memory` to run 2 instances at one time. If you set the maximum number of concurrent instances to 4, {{site.data.keyword.codeengineshort}} can deploy 2 of the same worker nodes to run all 4 instances at the same time across both workers. In the second scenario, the fleet finishes more quickly but requires more workers to be deployed. Keep in mind that there is an infinite number of combinations for automatic worker node deployment, and that worker nodes of various profiles might be deployed. 

Automatic scaling is not available for GPUs. To deploy GPUs for a fleet, you must specify the type of GPU worker to deploy.
{: note}

### Task and instance specification
{: #fleet-taskspec}

When deploying a fleet, users can specify the number of tasks to complete, the number of instances to run at a time, the order in which tasks are completed. Fleets can work on many tasks in parallel by starting multiple instances concurrently. All instances are created with the same amount of vCPU and memory as per the fleet’s specification. Additionally users can create a task specification file to provide specific commands and arguments for each task or to create custom task indexes.


### Task storage in COS
{: #fleet-cos}

You can use a COS bucket to provide the tasks for your fleet by specifying a persistent data store and bucket subpath when you create the fleet. Each object in the COS bucket represents a single task. 

### Isolation
{: #fleet-isolation}

Unlike batch jobs, fleets provide single-tenant isolation. Your fleet workers are not shared with other users. 

### Retries
{: #fleet-retries}

Each fleet instance runs to completion. However, in the event of an error, {{site.data.keyword.codeengineshort}} restarts the instance. You can limit the maximum number of retries to avoid restarting failed instances.

### Status
{: #fleet-status}

A fleet is in the `Running` status when at least one worker node is provisioned. When the fleet has is no longer running, it is in the `Succeeded` status if all tasks completed successfully, or `Failed` if one or more tasks failed. You can also cancel a fleet.

For more information, see [Understanding the status of your fleet](/docs/codeengine?topic=codeengine-fleet-status).

## How can I get started with fleets?
{: #fleet-getstart}

To create and run a simple {{site.data.keyword.codeengineshort}} fleet with the `icr.io/codeengine/helloworld` sample image, see [Running your first {{site.data.keyword.codeengineshort}} fleet](/docs/codeengine?topic=codeengine-getting-started#first-fleet).
