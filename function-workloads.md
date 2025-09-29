---

copyright:
  years: 2023, 2025
lastupdated: "2025-09-29"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Function workloads
{: #cefunctions}

A function is a stateless code snippet that performs tasks as it is invoked by HTTP requests. With IBM Code Engine functions, you can run your business logic in a scalable and serverless way. IBM Code Engine functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your function code can be written in a managed runtime that includes specific [Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime) versions.
{: shortdesc}

A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image.

## Lifecycle of a function instance
{: #functions-lifecycle}

When a function is invoked (started), the corresponding Function instance is initialized with the configured Runtime container and Resource parameters. The process of the first initialization is referred to as *cold start*.

To reduce the cold start latency, {{site.data.keyword.codeengineshort}} optimizes the invocation by pre-warming certain runtimes with specific CPU and memory configurations. Pre-warmed combinations for functions include Node.js and Python runtimes as well as the default CPU and memory combination for Functions, which is 0.25 vCPU x 1 GB of memory. In addition, the system is designed to improve the reuse of Function instances that are already initialized. Therefore, a Function instance is kept alive after the invocation is finished to allow subsequent invocations by reusing the same instance and reusing the state of the instance when the last invocation completed. The reuse of a Function instance is not guaranteed.

## What are key features of working with functions?
{: #functions-work-ce}

Review the following topics to learn more about working with IBM Code Engine Functions.

- [Isolation](#cefun-isolation)
- [Logging](#functions-logging)
- [Runtimes](#functions-runtime)
- [Running functions](#cefun-runfun)
- [Security](#cefun-security)
- [Invocation concurrency and scaling of function instances](#functions-concur-ce)
- [Packaging your source code for a function](#functions-packaging)


### Isolation
{: #cefun-isolation}

{{site.data.keyword.codeengineshort}} is a multi-tenant, regional service where tenants share the same network and compute infrastructure. In particular, the network and compute infrastructure are shared resources and some management components are common to all tenants. However, tenants and their workloads are isolated from each other by using {{site.data.keyword.codeengineshort}} projects.  {{site.data.keyword.codeengineshort}} prevents communication between projects, providing isolation to your applications inside a multi-tenant environment, which can include applications, batch jobs, and functions. In addition, there are access controls that are performed on a resource level to allow only authorized users to perform certain operations on project resources, such as functions or other {{site.data.keyword.codeengineshort}} workloads.

For more information about workload isolation, see [{{site.data.keyword.codeengineshort}} workload isolation](/docs/codeengine?topic=codeengine-architecture#workload-isolation).

### Logging
{: #functions-logging}

Function code can write `stdout` and `stderr` logs that are captured and forwarded to an {{site.data.keyword.logs_full_notm}} instance. {{site.data.keyword.logs_full_notm}} is a Platform logging instances that you can set up to index your logs. For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-logging).


### Runtimes
{: #functions-runtime}

{{site.data.keyword.codeengineshort}} includes *Managed runtimes* that you can use for your Functions.

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the overhead of pulling container images and starting containers and processes. Your code is injected into an already running container.



For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).

### Running functions
{: #cefun-runfun}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you a streamlined way to run your code as an app.

You can create and invoke your function in {{site.data.keyword.codeengineshort}} in the following ways:

* Run from an existing code bundle.

* Run from existing source code. If you are starting with source code that is located in a Git repository or on your local workstation, you can point to the location of your source and {{site.data.keyword.codeengineshort}} takes care of building the image for you.

For more information about creating and invoking functions, see [Working with functions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-work).

### Security
{: #cefun-security}

{{site.data.keyword.codeengineshort}} provides immediate DDOS protection for your function. {{site.data.keyword.codeengineshort}}'s DDOS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you. DDoS protection covers System Interconnection (OSI) Layer 3 and Layer 4 (TCP/IP) protocol attacks, but not Layer 7 (HTTP) attacks. See [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos).

{{site.data.keyword.codeengineshort}} also provides a service mesh to use its networking layer, which enables mutual Transport Layer Security (TLS) traffic for functions, thus securing *service-to-service* and *user-to-service* communication.

For more information about security, see [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).


### Invocation concurrency and scaling of function instances
{: #functions-concur-ce}

When multiple functions are being invoked at the same time, {{site.data.keyword.codeengineshort}} initializes new function instances for each invocation, but at the same time, tries to maximize the reuse. Only one function invocation is handled by a function instance at a single point in time. For Node.js, the function can be configured with `concurrency > 0` to allow multiple invocations to be handled in a single function instance.

### Packaging your source code for a function
{: #functions-packaging}

Functions can be packaged in three different ways.

- as a single file
- as multiple files (with a folder structure and dependent modules)
- as a container image


## How can I get started with functions?
{: #cefun-getstart}

To deploy a simple {{site.data.keyword.codeengineshort}} application with a `hello-world` sample image, see [Running IBM Code Engine Functions](/docs/codeengine?topic=codeengine-fun-tutorial) tutorial.

To dive deeper into working with functions, see [Working with functions in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-work).
