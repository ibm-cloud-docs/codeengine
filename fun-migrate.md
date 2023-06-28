---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-28"

keywords: code engine, function, create function, code engine function, create code engine function, migrate function

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Migrating IBM Cloud Functions to {{site.data.keyword.codeengineshort}}
{: #fun-migrate}

[IBM Cloud Functions](https://cloud.ibm.com/docs/openwhisk){: external} has been IBM’s recommended Functions-as-a-Service solution, based on IBM’s public cloud. Available in six data centers around the world, IBM Cloud Functions has been serving the needs of customers since its inception. 
{: shortdesc}

However, the increased demands and additional requirements our valued customers have been articulating, lead us to constantly innovate, improve, and evolve the IBM Functions-as-a-Service technologies and offerings. As a result and to address these demands, IBM is adding Functions-as-a-Service technology to IBM Cloud Code Engine.

## Comparing Code Engine to Cloud Functions
{: #fun-migrate-compare}

The SOC2, ISO32k, BSI C5, and Financial Services Cloud-certified IBM Cloud Code Engine service is available in nine (9) regions. As a fully managed, serverless platform, it runs a broad variety of customer workloads as containers, batch jobs, applications, and functions. You can access [Code Engine in the IBM Public Cloud](https://cloud.ibm.com/codeengine){: external}. 

The new Functions-as-a-Service capabilities enable Code Engine customers to perform short running, run-to-completion type of workloads. Whether you are a Cloud Functions customer or you are new to Functions-as-a-Service, you can learn more about [running functions in IBM Cloud Code Engine](/docs/codeengine?topic=codeengine-fun-work). You can even [take a tutorial](/docs/codeengine?topic=codeengine-fun-tutorial).
  
Functions-as-a-Service in Code Engine offers an improved server-less value proposition in terms of user experience, usage patterns, security, and total cost of ownership. 
  
Function sin Code Engine simplifies your user experience, with the following options.

- Integrates fully with the Code Engine development flow and features.
- Includes common programming languages and provides optimized managed runtimes.
- Supports custom runtime images as optimized fit-to-purpose execution environments.
- Offers on-demand code execution with low cold-start latency and rapid scale-out.
- Offers a Web-URL based Function invocation mechanism with feature-rich support for web applications.
- Supported security capabilities such as access to private repositories and registries.


With IBM Cloud Code Engine Functions, you can use your favorite programming language to write lightweight code that runs snippets of business logic in a scalable way. You can run code in response to HTTP requests from applications or in response to IBM Cloud services and external events. 

## Key capabilities
{: #fun-migrate-key}

When you migrate your IBM Cloud Functions based workloads, consider the following capabilities and strategies.

- Supports an evolving list of managed runtimes. For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).
    - Node.js Release Version 18
    - Python Release Version 3.11
  
- Adds support for custom runtime images. You can use any custom container image as long as it fulfills an Openwhisk compliant runtime contract.
- Provides [optimized CPU and memory combinations](/docs/codeengine?topic=codeengine-fun-runtime#fun-cpu-mem). 

In addition, {{site.data.keyword.codeengineshort}} includes [Function limits](/docs/codeengine?topic=codeengine-limits#limits_functions), as well as [project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas). 


## How Functions compare to apps and jobs
{: #fun-migrate-compare-app-job}

{{site.data.keyword.codeengineshort}} apps serve long running, complex, compute tasks on a scalable compute infrastructure. {{site.data.keyword.codeengineshort}} jobs are used for low-parallelism, scheduled workloads that can require high resources. For more information, see [Common scenarios for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine#common-scenarios). 

Functions can perform lightweight, short running, data transformations as results of external events. They can also serve the content for dynamic, data elements on Web pages. In general, functions can perform scalable, short running parallel tasks that must be finished in a defined or short time.

{{site.data.keyword.codeengineshort}} Functions offers a straight-forward programming model that uses source code snippets of supported programming languages. These code snippets are used “inline” in a Function definition with no need to compile your code first.
 
| Characteristic | App | Job | Function |
| --------- | --------- | --------- | --------- |
| Execution time (duration) | Long-running 10min per request | Long-running up to 24hrs | Short-running (<=2mins) |
| Startup latency | Medium | Scheduled start | Low  | 
| Termination | Run-continuously | Run-to-completion | Run-to-completion |
| Invocation | On request or permanently running | Scheduled | On request, instant |
| Programming Model | Container based build and execution | Container based build and execution | Language specific source code files and dependency meta data |
| Parallelism | Parallel execution, flexible | Low to medium parallel execution | High parallel execution |
| Scale-out | Based on number of requests | Based on job workload definition | Based on events or direct invocations |
| Optimized for | Long running highly complex workload and on-demand scale-out | Scheduled/planned workloads with high resource demands | Startup time and rapid scale-out |
{: caption="Table 1. Comparing {{site.data.keyword.codeengineshort}} apps, jobs, and functions" caption-side="bottom"}

## Migrating IBM Cloud Functions Actions to Code Engine Functions FAQ
{: #fun-migrate-faqs}

### How can I process a bulk-load of computations?
{: #fun-migrate-faq1}
 
If you process a bulk-load of computations that require high CPU and memory resources and must be finished in less than n hours, you can migrate your program logic into a {{site.data.keyword.codeengineshort}} job and then schedule your jobs to run daily.  For more information, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).

### I used Cloud Function to include dynamic elements for my web application. Can I move to {{site.data.keyword.codeengineshort}} Functions?
{: #fun-migrate-faq2}
 
You can convert your action to a {{site.data.keyword.codeengineshort}} Function and then use the provided Function URL to invoke and return the required dynamic content. See [Working with Functions](/docs/codeengine?topic=codeengine-fun-work) to get started.

### Can I trigger my function code?
{: #fun-migrate-faq3}

While {{site.data.keyword.codeengineshort}} does not include an object called a “trigger”, it does support subscribing to event producers, including cron jobs (alarms), Object storage, and Event Streams (Kafka) data. For more information, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events).

### Can my function be accessed publically?
{: #fun-migrate-faq4}

A {{site.data.keyword.codeengineshort}} Function includes a public URL, that is provided for you when you create it.

### How can I secure my functions?
{: #fun-migrate-faq5}

While your code can be secured in a Git repository or container registry, because your function URL is public, authorization to invoke your function must be implemented by the Function code itself.

### Can I include dynamic elements?
{: #fun-migrate-faq6}
 
You can include dynamic elements that are supported by {{site.data.keyword.codeengineshort}}. For example, if you are using a Cloudant database and invoke Cloud Functions actions based on data changes, then you cannot migrate as {{site.data.keyword.codeengineshort}} does not support subscribing to a Cloudant database. You can, however, subscribe to {{site.data.keyword.cos_full_notm}}.
 
### Can I use sequences to chain my functions together?
{: #fun-migrate-faq7}
 
{{site.data.keyword.codeengineshort}} does not include support for sequences. However, because any Function can be invoked by calling its web URL, you can chain your Functions together with a series of REST calls. This logic must be added directly to your Function code.

### Can I use `whisk.system` actions?
{: #fun-migrate-faq8}

I use Cloud Functions system that are based on `whisk.system` actions. Can I use them in Code Engine Functions?

Export your `whisk.system` action with the `ibmcloud fn` CLI. The output contains the source code and references to required libraries. Then, [create a Code Engine Function](/docs/codeengine?topic=codeengine-fun-create-local), based on the exported source artifacts. While a certain level of artifact compatibility is retained, you cannot export the Action metadata directly into Code Engine Functions.

### Can I bind my function to service credentials?
{: #fun-migrate-faq9}

Yes, service binds are supported! See [Working with service bindings to integrate IBM Cloud services with Code Engine](/docs/codeengine?topic=codeengine-service-binding).                     

### Where can I find information about my in progress and finished Code Engine Function runs?
{: #fun-migrate-faq10}

If you created your Function from source code, you can [view build logs](/docs/codeengine?topic=codeengine-view-logs#view-build-cli).

Otherwise, you can use [set up {{site.data.keyword.la_full_notm}}](/docs/codeengine?topic=codeengine-view-logs#view-funlogs-ui) to view Platform logs, which contain information about your Function invocation (meta information) as well as log messages emitted by the Function code.

  
  
