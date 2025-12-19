---

copyright:
  years: 2025, 2025
lastupdated: "2025-12-19"

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
| VPC connection | Natively connects to existing VPC | Requires private path |
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
{: #fleet-status-summary}

A fleet is in the `Running` status when at least one worker node is provisioned. When the fleet is no longer running, it is in the `Succeeded` status if all tasks completed successfully, or `Failed` if one or more tasks failed. You can also cancel a fleet.

For more information, see [Understanding the status of your fleet](/docs/codeengine?topic=codeengine-fleet-status).

### Worker profile
{: #fleet-profile}

You can optionally choose the profile for your fleet worker. If you do not specify a profile, {{site.data.keyword.codeengineshort}} will pick a profile for you.

{{site.data.keyword.codeengineshort}} fleets support the following profile families:

| Instance profile |
|---------|
| bx2-2x8 |
| bx2-4x16 |
| bx2-8x32 |
| bx2-16x64 |
| bx2-32x128 |
| bx2-48x192 |
| bx2-64x256 |
| bx2-96x384 |
| bx2-128x512 |
| bx2a-2x8 |
| bx2a-4x16 |
| bx2a-8x32 |
| bx2a-16x64 |
| bx2a-32x128 |
| bx2a-48x192 |
| bx2a-64x256 |
| bx2a-96x384 |
| bx2a-128x512 |
| bx2a-228x912 |
| bx2d-2x8 |
| bx2d-8x32 |
| bx2d-16x64 |
| bx3d-2x10 |
| bx3d-4x20 |
| bx3d-8x40 |
| bx3d-16x80 |
| bx3d-24x120 |
| bx3d-32x160 |
| bx3d-48x240 |
| bx3d-64x320 |
{: caption="Balanced" caption-side="bottom"}
{: tab-title="Balanced"}
{: tab-group="profiles-tab-group"}
{: class="simple-tab-table"}
{: #balanced}

| Instance profile |
|---------|
| cx2-2x4 |
| cx2-4x8 |
| cx2-8x16 |
| cx2-16x32 |
| cx2-32x64 |
| cx2-48x96 |
| cx2-64x128 |
| cx2-96x192 |
| cx2-128x256 |
| cx3d-2x5 |
| cx3d-4x10 |
| cx3d-8x20 |
| cx3d-16x40 |
| cx3d-24x60 |
| cx3d-32x80 |
| cx3d-48x120 |
| cx3d-64x160 |
{: caption="Compute" caption-side="bottom"}
{: tab-title="Compute"}
{: tab-group="profiles-tab-group"}
{: class="simple-tab-table"}
{: #compute}

| Instance profile |
|---------|
| mx2-2x16 |
| mx2-4x32 |
| mx2-8x64 |
| mx2-16x128 |
| mx2-32x256 |
| mx2-48x384 |
| mx2-64x512 |
| mx2-96x768 |
| mx2-128x1024 |
| mx2d-16x128 |
| mx2d-64x512 |
| mx2d-96x768 |
| mx3d-2x20 |
| mx3d-4x40 |
| mx3d-8x16 |
| mx3d-16x160 |
| mx3d-24x240 |
| mx3d-32x320 |
| mx3d-48x480 |
| mx3d-64x640 |
{: caption="Memory" caption-side="bottom"}
{: tab-title="Memory"}
{: tab-group="profiles-tab-group"}
{: class="simple-tab-table"}
{: #memory}

| Instance profile |
|---------|
| gx3-16x80x1l4 |
| gx3-32x160x2l4 |
| gx3-64x320x4l4 |
| gx3-24x120x1l40s |
| gx3-48x240x2l40s |
| gx2-8x64x1v100 |
| gx2-16x128x1v100 |
| gx2-16x128x2v100 |
| gx2-32x256x2v100 |
| gx3d-24x120x1a100p |
| gx3d-48x240x2a100p |
| gx3d-160x1792x8h100 |
{: caption="GPU" caption-side="bottom"}
{: tab-title="GPU"}
{: tab-group="profiles-tab-group"}
{: class="simple-tab-table"}
{: #gpu}

| Instance profile |
|---------|
| nxf-2x1 |
| nxf-2x2 |
| bxf-2x8 |
| bxf-4x16 |
| bxf-8x32 |
| bxf-16x64 |
| bxf-24x96 |
| bxf-32x128 |
| bxf-48x192 |
| bxf-64x256 |
| cxf-2x4 |
| cxf-4x8 |
| cxf-8x16 |
| cxf-16x32 |
| cxf-24x48 |
| cxf-32x64 |
| cxf-48x96 |
| cxf-64x128 |
| mxf-2x16 |
| mxf-4x32 |
| mxf-8x64 |
| mxf-16x128 |
| mxf-24x192 |
| mxf-32x256 |
| mxf-48x384 |
| mxf-64x512 |
{: caption="Flex" caption-side="bottom"}
{: tab-title="Flex"}
{: tab-group="profiles-tab-group"}
{: class="simple-tab-table"}
{: #flex}

Some profiles may not be available in all VPC network zones. You can use the following CLI command to list the profiles in a region.

```txt
ibmcloud is instance-profiles
```
{: pre}

* If you want to know zonal availability and capacity of certain profiles, such as H100 and L40s, [open a support case](/docs/codeengine?topic=codeengine-get-support) and select "Virtual Private Cloud (VPC)" as the topic.
* If you need a certain VPC profile which is not supported by fleets today, [open a support case](/docs/codeengine?topic=codeengine-get-support) and select "Code Engine" as the topic.

## How can I get started with fleets?
{: #fleet-getstart}

To create and run a simple {{site.data.keyword.codeengineshort}} fleet with the `icr.io/codeengine/helloworld` sample image, see [Running your first {{site.data.keyword.codeengineshort}} fleet](/docs/codeengine?topic=codeengine-getting-started#first-fleet).
