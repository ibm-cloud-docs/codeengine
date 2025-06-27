---

copyright:
  years: 2023, 2025
lastupdated: "2025-06-27"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Function runtimes
{: #fun-runtime}

{{site.data.keyword.codeengineshort}} includes *managed runtimes* that you can use for your functions.
{: shortdesc}

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the pulling of container images and starting containers and processes. Your code is injected into an already running container.

Need to deploy a container image? See [Working with apps](/docs/codeengine?topic=codeengine-application-workloads) or [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). Not sure what type of {{site.data.keyword.codeengineshort}} workload to create? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}



## Supported managed runtimes for functions on {{site.data.keyword.codeengineshort}}
{: #fun-supported-managed}

The following runtimes are supported as managed runtimes.

- Node.js 20, Node.js 22
- Python 3.11, Python 3.13

## Supported CPU and memory combinations for functions
{: #fun-supported-combo}

See the following list for valid combinations of CPU and memory for functions.

- 0.25 vCPU and 1 GB memory
- 0.5 vCPU and 2 GB memory
- 1 vCPU and 4 GB memory (**Default**)

For memory and CPU information, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

## Runtime support lifecycle
{: #fun-runtimes-support-lifecycle}

The support lifecycle of managed runtimes for {{site.data.keyword.codeengineshort}} functions depends on the official support cycles of the programming language release on which they are based. If the runtime that your function uses reaches its end of life, your function stops working. Before end of life is a deprecation period (typically six months), when the runtime continues to receive security updates during user migration to the new runtime release. The following table lists the deprecation and end of life dates:

| Runtime | Deprecation | End of life |
| -------------- | -------------- | -------------- |
| Node.js 20  | 1 November 2025 | 30 April 2026 |
| Node.js 22 | 20 October 2026 | 30 April 2027 |
| Python 3.11 | 1 May 2027 | 30 September 2027 |
| Python 3.13 | 1 October 2026 | 30 April 2027 |
{: caption="Deprecation and end of life dates" caption-side="bottom"}

## Upgrading a function to a new runtime release
{: #fun-upgrade-to-new-runtime-release}

New runtime releases can contain breaking API changes and functions might require code changes, which must be tested. Use the {{site.data.keyword.codeengineshort}} `ibmcloud ce function update --runtime` CLI command to update your existing functions to use a new runtime version. Doing so Immediately causes the function to run with the new (selected) runtime release as the base (=in-place update). Therefore, do not use any in-place updates for production code. Create a test function during the migration phase.

Updating production code depends on whether it is acceptable that the function's URL is changed or if the URL must be kept:

* If function URL endpoint changes are acceptable:
    - create a new function based on the same source code (or code bundle) as the original function, by using the new runtime release.
    - make sure that the new function works as expected. If it does not, adapt the source code and rebuild the function.
    - use the new function URL and remove the previous version.

*  If the original function URL endpoint must be kept:
    - create a new function (as a test function) based on the same source code (or code bundle) as the original function, by using the new runtime release
    - make sure that the test function works as expected. If it does not, adapt the code and rebuild the test function.
    - update the original function to use the new runtime release and the adapted source code.
