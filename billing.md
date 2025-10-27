---

copyright:
  years: 2025
lastupdated: "2025-10-27"

keywords: billing, pricing, costs for code engine, billing for code engine, job pricing, app pricing, build pricing

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for {{site.data.keyword.codeengineshort}}
{: #pricing}

{{site.data.keyword.codeenginefull}} is different from traditional cloud computing technologies, you pay for only the resources that you use. You are billed for the memory and vCPU that your workloads consume, as well as any incoming HTTP calls. If your app scales to zero or your job or build isn't running, you are not consuming resources and so you are not charged.
{: shortdesc}

{{site.data.keyword.codeengineshort}} includes a free tier so that you can experiment with {{site.data.keyword.codeengineshort}} before you commit.

You are billed for the following entities,

- [Applications](#app-pricing)
- [Job runs](#job-pricing)
- [Functions](#functions-pricing)
- [Fleet](#fleet-pricing)
- [Build runs](#build-pricing)

Entities such as [projects](/docs/codeengine?topic=codeengine-manage-project) do not incur charges, but instead serve as a folder for your entities. Entities such as secrets, bindings, or subscriptions do not incur charges, but do contribute to the overall limits of your project. For more information, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

The costs that are provided in this topic are guidelines and do not represent actual costs. They represent a starting point for estimates of costs that are incurred in environments with a similar configuration. Actual costs can vary by geography. For the most up-to-date prices, see [{{site.data.keyword.codeengineshort}} pricing](https://cloud.ibm.com/codeengine/overview#pricing){: external}. 
{: important}

## Application pricing
{: #app-pricing}

When you deploy an application, charges apply for HTTP requests and for the CPU and memory resources that are consumed by running instances of the application. Incoming HTTP calls are billed by the number of HTTP calls that are received by your application. For example, if your app serves 100 calls, you are then billed for 100 HTTP calls. Internal HTTP traffic within a project between your workloads is excluded from the billable HTTP call total.

For example, 

- If you create a {{site.data.keyword.codeengineshort}} app with `2` GB (gigabyte) memory and `1` virtual CPU, with a minimum and maximum instance scale of `1`, after an hour, you are charged for `1` vCPU hour and `2` GB hours. 
- If you then set your maximum instance scale to `2` and your application receives enough requests to scale up to 2, then you are billed for the (`number of instances`) x (`number of virtual CPUs`) = `2` vCPU and `4` GB per hour.

For valid CPU and memory combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

Note that the time that it takes to pull your image or to build it from source code is included in the billable time.

## Job pricing
{: #job-pricing}

When you run a job, charges apply for the CPU and memory resources that are consumed by the job when it runs. You are not charged for your job configuration.

For example, 

- If you create a job to process information from {{site.data.keyword.cos_full_notm}} with one job instance and that runs for an hour and uses `4` GB of memory, you are billed for `1` CPU hour and `4` GB hours.
- If you scale the same job to `4` instances and then it completes in 15 minutes, you are charged for `4` vCPU and `16` GB for `.25` hours.

For valid CPU and memory combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

Note that the time that it takes to pull your image or to build it from source code is included in the billable time.

## Function pricing
{: #functions-pricing}

When you deploy a function, charges apply for HTTP requests, and for the CPU and memory resources that are consumed by running instances of the function. Incoming HTTP calls are billed by the number of HTTP calls that are received by your function. For example,
* If your function serves 100 calls, you are then billed for 100 HTTP calls. Internal HTTP traffic within a {{site.data.keyword.codeengineshort}} project between your workloads is excluded from the billable HTTP call total. 
* If you create a {{site.data.keyword.codeengineshort}} function with 2 GB memory and 0.5 virtual CPU, after 600 invocations (assuming each requires 6 seconds to complete the result), you are charged for 0.5 vCPU hour and 2 GB hours. 
  
For valid CPU and memory combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

The time that it takes to pull your code bundle or to build it from source code is included in the billable time. 
{: note}

## Fleet pricing
{: #fleet-pricing}

When you run a fleet, charges apply only for the CPU, memory resources, and potentially GPU resources, that are consumed while the fleet runs.

For each fleet you run, you can choose to allow Code Engine to deploy worker nodes to meet the fleet resource requirements, or you can choose to deploy a specific worker node profile that you specify.  Review the cost considerations for both options below. 

### If you let CE automatically provision worker nodes
{: #fleet-pricing-auto}

When you run your fleet, you specify the amount of resources required to run an instance of your code to complete a task, and the maximum number of instances to run concurrently. Code Engine deploys worker nodes of potentially various profiles to meet these resource requirements most efficiently. In this scenario, the cost is based on the worker nodes deployed, but can be approximated using the instance resource requirements you specify, the number of tasks, and the average instance runtime. The formula to approximate the cost of a fleet based on these values is:

`[ (total cost of vCPU seconds) + (total cost of GB seconds) ] x (# of tasks) x (average runtime of each task in seconds)`  

For example, if an instance of your code requires 2 vCPU and 4 GB, you run 100 tasks, and the average runtime of each task is 0.5 seconds, the formula to approximate the total cost is:

`[ 2 x (cost of 1 vCPU second) + 4 x (cost of 1 GB second) ] x (100) x (0.5)`  

The total cost to run the fleet is the accumulation of costs for each worker node utilized during the runtime of the fleet.  Additionally, unsuccessful instances can have their runtimes increased by retries, which can add to the fleet cost. You can configure retry settings when you create the fleet. 

Code Engine does not automatically deploy GPUs for fleets. To deploy GPUs for your fleet, you must choose to deploy a specific worker profile or GPU family. 
{: note}

 
### If you choose a specific worker profile
{: #fleet-pricing-spec}


If you choose to deploy a specific worker node profile or family for your fleet, then only that type of worker node is deployed for your fleet. The total cost to run the fleet is the accumulated cost to run each worker node that is deployed. You can also choose worker profiles with GPUs.

This option is currently available in the CLI only.
{: note}

Keep in mind that this may not be the most efficient way to run your fleet and might result in a higher cost if worker resources deployed exceed resources required.

#### Non-GPU worker profiles
{: #fleet-pricing-non-gpu}

If you do not use GPUs, then the cost to run a worker can be approximated with the following formula:

`[ (total cost of worker VPU seconds) + (total cost of worker GB seconds)  ] x  (average worker runtime in seconds)` 

For example, if you choose a worker profile of 16 vCPU and 64 GB, and your fleet runs for 10 seconds, the formula to approximate the total cost is:

`[ 16 x (cost of 1 vCPU second) + 64 x (cost of 1 GB second) ] x (10)`

The total cost to run the fleet is the accumulated cost of running each worker node that deploys. For example, if `2` worker nodes are deployed, you would multiple the above formulas by `2` to approximate the total cost. Keep in mind that the number of worker nodes depends on the required instances resources and the maximum number of concurrent instances.

#### GPU worker profiles
{: #fleet-pricing-gpu}

Each GPU worker incurs an additional charge for GPU seconds. You can approximate the cost of running a GPU worker with the following formula:

`[ (total cost of  GPU-seconds) + (Total cost of vCPU seconds) + (total cost of 1 GB second) ] x (average worker runtime in seconds)`

For example, consider the worker node profile `gx3-24x120x2l40s`. You can use the values in the worker node profile to approximate the cost of using the worker. The profile is composed of these parts:
- The first value `gx3` is the worker node category.
- The second value, `24` is the vCPU 
- The third value `120` is the GB of memory
- The fourth value `2 L40s`, represents the number of L40s GPU cores.

The approximate cost per second to use a worker node with this profile is:

`[ 24 x (cost of 1 vCPU second) + 120 x (cost of 1 GB second) + 2 x (cost of 1 L40 GPU-second) ] x (average worker runtime in seconds)` 

The total cost to run the fleet is the accumulated cost of running each worker node that deploys. For example, if `2` GPU workers are deployed, you would multiple the above formulas by `2` to approximate the total cost. Keep in mind that the number of worker nodes depends on the required instance resources and the maximum number of concurrent instances.

## Build pricing
{: #build-pricing}

When you build an image from source code to deploy as an app or run as a job, you are billed for the memory and vCPU usage time that the build consumes. However, this charge is separate from the charges that you might incur when you use the resulting image in an application or job run. You are not charged for your build configuration.

Builds are classified as `small`, `medium`, `large`, `xlarge`, and `xxlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build when it runs. A smaller build is less expensive, but typically also slower due to the lower number of CPU cores. In addition, the memory and disk requirements of your build might cause the build to fail if you choose too small a size. For more information about build size, see [Determine the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size).

Note that the time that it takes to pull source code and push your built image is included in the billable time.
