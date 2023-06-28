---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-28"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Runtimes
{: #fun-runtime}

{{site.data.keyword.codeengineshort}} includes *Managed runtimes* that you can use for your Functions, but also supports *Custom runtimes* if the Function program logic has specific demands on its runtime environment.

Managed runtimes include Node.js and Python versions and specific CPU and memory combinations. These runtimes are optimized for fast startup. These runtimes are pre-warmed, which avoids the overhead of pulling container images and starting containers and processes. Your code is injected into an already running container. Use these managed runtimes when possible.

Custom runtimes are available for experienced users. You can build your own custom runtime that allows you to pre-package common libraries that are used across different Function implementations. This approach gives you more flexibility in the development process, but still allows for faster startup times, when compared to containerized applications. For more information about custom runtimes, see [Packaging dependencies for your Function](/docs/codeengine?topic=codeengine-fun-package).

## Supported managed runtimes for Functions on {{site.data.keyword.codeengineshort}}
{: #fun-supported-managed}
  
The following runtimes are supported as managed runtimes.
  
- Node.js 18
- Python 3.11
  
## Optimized CPU and memory combinations
{: #fun-cpu-mem}
  
The following table contains the supported CPU and memory combinations for Functions.
  
| Function footprint | Memory | CPU |
| --------- | ------ | ----- |
| Small  | `1G` | `0.25` |
| Medium | `2G` | `0.5` |
| Large  | `4G` | `1.0` |
{: caption="Table 1. Optimized CPU and memory combinations" caption-side="bottom"}

For other supported CPU and memory combinations, see [Supported CPU and memory combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
 
