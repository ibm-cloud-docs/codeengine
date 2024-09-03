---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-03"

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

## Runtimes support lifecycle
{: #fun-runtimes-support-lifecycle}

The support lifecycle of Code Engine functions' managed runtimes depends on the official support cycles of the language upon they are based. With end of life of the underlying runtime, Functions will stop working. With the begin of the deprecation, the successor release becomes the default runtime. The following table lists the deprecation and end of life dates. 

Runtime     | Deprecation | End of life
------------+-------------+------------
Node.js 18  | 1/Oct/2024  | 1/May/2025
Node.js 20  | 1/Nov/2025  | 1/May/2026
Python 3.11 | 1/May/2027  | 1/Nov/2027

## How to upgrade a Function to a new runtime release
{: #fun-upgrade-to-new-runtime-release}

Each function has a managed runtime release associated with it, even if the (generic) runtime family was specified during the function creation. Managed runtimes expire after a deprecation period, and in line with the official support period of the runtime provider. After the end of the deprecation period (end of life of the runtime), a function using this runtime will stop working.

Therefore, existing functions must be migrated to the currently supported (new) runtime release. As new runtime releases may contain breaking API changes, the update of a function to a new runtime release comprises of migration (code changes) and testing steps. Customers may use the IBM Code Engine CLI's "ibmcloud ce function update --runtime ..." command to update existing functions with a new runtime version. Doing so will immediately cause the function to run untested with the new (selected) runtime release as base (in-place update). Therefore, in-place update is not recommended for production code.

The recommended way to update production code depends on whether it is acceptable that the function's URL is changed or if the URL must be kept:

1. Function URL endpoint changes are acceptable
- create a new function based on the same source code (or code bundle) like the original function, using the new runtime release
- ensure the new function works as expected. if not, adapt the source code and rebuild the function
- use the new function URL and remove the previous version

2. Original function URL endpoint must be kept
- create a new function (=test function) based on the same source code (or code bundle) like the original function, using the new runtime release
- ensure the test function works as expected. if not, adapt the code and rebuild the test function
- update the original function to use a) the new runtime release and b) the adapted source code
