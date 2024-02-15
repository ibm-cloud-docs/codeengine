---

copyright:
  years: 2024
lastupdated: "2024-02-15"

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



## Build pricing
{: #build-pricing}

When you build an image from source code to deploy as an app or run as a job, you are billed for the memory and vCPU usage time that the build consumes. However, this charge is separate from the charges that you might incur when you use the resulting image in an application or job run. You are not charged for your build configuration.

Builds are classified as `small`, `medium`, `large`, `xlarge`, and `xxlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build when it runs. A smaller build is less expensive, but typically also slower due to the lower number of CPU cores. In addition, the memory and disk requirements of your build might cause the build to fail if you choose too small a size. For more information about build size, see [Determine the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size).

Note that the time that it takes to pull source code and push your built image is included in the billable time.



