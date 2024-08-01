---

copyright:
  years: 2023, 2024
lastupdated: "2024-08-01"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Function runtimes
{: #fun-runtime}

{{site.data.keyword.codeengineshort}} includes *Managed runtimes* that you can use for your functions.
{: shortdesc}

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the overhead of pulling container images and starting containers and processes. Your code is injected into an already running container.

Need to deploy a container image? See [Working with apps](/docs/codeengine?topic=codeengine-application-workloads) or [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). Not sure what type of {{site.data.keyword.codeengineshort}} workload to create? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}



## Supported managed runtimes for functions on {{site.data.keyword.codeengineshort}}
{: #fun-supported-managed}

The following runtimes are supported as managed runtimes.

- Node.js 18 and Node.js 20
- Python 3.11

## Supported CPU and memory combinations for functions
{: #fun-supported-combo}

See the following list for valid combinations of CPU and memory for functions.

- 0.25 vCPU and 1 GB memory 
- 0.5 vCPU and 2 GB memory (**Default**)
- 1 vCPU and 4 GB memory


For memory and CPU information, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
