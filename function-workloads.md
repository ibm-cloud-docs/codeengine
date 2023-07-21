---

copyright:
  years: 2023, 2023
lastupdated: "2023-07-21"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Function workloads
{: #cefunctions}

A Function is a stateless code snippet that performs tasks in response to an HTTP request. With IBM Code Engine Functions, you can run your business logic in a scalable and serverless way. IBM Code Engine Functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your Function code can be written in a managed runtime that includes specific [Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime) versions.
{: shortdesc}

## Lifecycle of a Function instance
{: #functions-lifecycle}

When a Function is invoked, the corresponding Function instance is initialized with the configured Runtime container and Resource parameters. The process of the first initialization is referred to as *cold start*.

To reduce the cold start latency, {{site.data.keyword.codeengineshort}} optimizes the invocation by pre-warming certain runtimes with specific CPU and memory configurations. In addition, the system is designed to improve the reuse of Function instances that are already initialized. Therefore, a Function instance is kept alive after the invocation is finished to allow subsequent invocations by reusing the same instance and reusing the state of the instance when the last invocation completed. How long it is kept alive can be configured by the `scale-down-delay` option. The reuse of a Function instance is not guaranteed.

## How do Functions compare to apps and jobs?
{: #functions-work-compare}

| Characteristic | App | Job | Function |
| --------- | --------- | --------- | --------- |
| Execution time (duration) | Long-running (10 minutes per request) | Long-running (up to 24 hours) | Short-running (2 minutes or less) |
| Startup latency | Medium | Scheduled start | Low  | 
| Termination | Run-continuously | Run-to-completion | Run-to-completion |
| Invocation | On request or permanently running | Scheduled | On request, instant |
| Programming Model | Container-based build and execution | Container-based build and execution | Language-specific source code files and dependency metadata |
| Parallelism | Parallel execution, flexible | Low to medium parallel execution | High parallel execution |
| Scale-out | Based on number of requests | Based on job workload definition | Based on events or direct invocations |
| Optimized for | Long running, highly complex workload and on-demand scale-out | Scheduled or planned workloads with high resource demands | Startup time and rapid scale-out |
{: caption="Table 1. Comparing {{site.data.keyword.codeengineshort}} apps, jobs, and functions" caption-side="bottom"}

## What are key features of working with Functions?
{: #functions-work-ce}

Review the following topics to learn more about working with IBM Code Engine Functions.

- [Isolation](#cefun-isolation)
- [Logging](#functions-logging)
- [Runtimes](#functions-runtime)
- [Running Functions](#cefun-runfun)
- [Security](#cefun-security)
- [Invocation concurrency and scaling of Function instances](#functions-concur-ce)
- [Packaging your source code for a Function](#functions-packaging)


### Isolation
{: #cefun-isolation}

{{site.data.keyword.codeengineshort}} is a multi-tenant, regional service where tenants share the same network and compute infrastructure. In particular, the network and compute infrastructure are shared resources and some management components are common to all tenants. However, tenants and their workloads are isolated from each other by using {{site.data.keyword.codeengineshort}} projects.  {{site.data.keyword.codeengineshort}} prevents communication between projects, providing isolation to your applications inside a multi-tenant environment, which can include applications, batch jobs, and functions. in In addition, there are access controls that are performed on a resource level to allow only authorized users to perform certain operations on project resources, such as Functions or other {{site.data.keyword.codeengineshort}} workloads.

For more information about workload isolation, see [{{site.data.keyword.codeengineshort}} workload isolation](/docs/codeengine?topic=codeengine-architecture#workload-isolation).

### Logging
{: #functions-logging}

Function code can write `stdout` and `stderr` logs that are captured and forwarded to an {{site.data.keyword.loganalysisfull_notm}} instance. {{site.data.keyword.loganalysisfull_notm}} is a Platform logging instances that you can set up to index your logs. For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).


### Runtimes
{: #functions-runtime}

{{site.data.keyword.codeengineshort}} includes *Managed runtimes* that you can use for your Functions.

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the overhead of pulling container images and starting containers and processes. Your code is injected into an already running container. Use these managed runtimes when possible.



For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).

### Running Functions
{: #cefun-runfun}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you a streamlined way to run your code as an app.

You can create and invoke your Function in {{site.data.keyword.codeengineshort}} in the following ways:

* Run from an existing code bundle. 

* Run from existing source code. If you are starting with source code that is located in a Git repository or on your local workstation, you can point to the location of your source and {{site.data.keyword.codeengineshort}} takes care of building the image for you. 

For more information about creating and invoking Functions, see [Working with Functions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-work).
	
### Security 
{: #cefun-security}

{{site.data.keyword.codeengineshort}} provides immediate DDOS protection for your Function. {{site.data.keyword.codeengineshort}}'s DDOS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you. DDoS protection covers System Interconnection (OSI) Layer 3 and Layer 4 (TCP/IP) protocol attacks, but not Layer 7 (HTTP) attacks. See [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos). 

{{site.data.keyword.codeengineshort}} also provides a service mesh to use its networking layer, which enables mutual Transport Layer Security (TLS) traffic for Functions, thus securing *service-to-service* and *user-to-service* communication.

For more information about security, see [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).


### Invocation concurrency and scaling of Function instances
{: #functions-concur-ce}

When multiple Functions are being invoked at the same time, {{site.data.keyword.codeengineshort}} initializes new Function instances for each invocation, but at the same time, tries to maximize the reuse. Only one Function invocation is handled by a Function instance at a single point in time. For Node.js, the Function can be configured with `concurrency > 0` to allow multiple invocations to be handled in a single Function instance. 

### Packaging your source code for a Function
{: #functions-packaging}

Functions can be packaged in three different ways.

- as a single file
- as multiple files (with a folder structure and dependent modules)
- as a container image


## How can I get started with Functions?
{: #cefun-getstart}
  
To deploy a simple {{site.data.keyword.codeengineshort}} application with a `hello-world` sample image, see [Running IBM Code Engine Functions](/docs/codeengine?topic=codeengine-fun-tutorial) tutorial.

To dive deeper into working with Functions, see [Working with Functions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-work).


