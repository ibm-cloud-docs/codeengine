---

copyright:
  years: 2023, 2023
lastupdated: "2023-10-09"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Runtimes
{: #fun-runtime}

{{site.data.keyword.codeengineshort}} includes *Managed runtimes* that you can use for your Functions.
{: shortdesc}

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the overhead of pulling container images and starting containers and processes. Your code is injected into an already running container.

Need to deploy a container image? See [Working with apps](/docs/codeengine?topic=codeengine-application-workloads) or [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). Not sure what type of {{site.data.keyword.codeengineshort}} workload to create? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}



## Supported managed runtimes for Functions on {{site.data.keyword.codeengineshort}}
{: #fun-supported-managed}
  
The following runtimes are supported as managed runtimes.
  
- Node.js 18
- Python 3.11

For memory and CPU information, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).


 
