---

copyright:
  years: 2022
lastupdated: "2022-01-28"

keywords: applications in code engine, apps in code engine, job in code engine, memory and cpu combinations, memory in code engine, cpu in code engine, memory and CPU

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Supported memory and CPU combinations
{: #mem-cpu-combo}

{{site.data.keyword.codeenginefull}} applications and jobs consume CPU and memory. These amounts can vary, depending on if your app is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

For more information about memory or CPU limitations, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

See the following table for valid combinations of vCPU and memory.

| CPU-intensive  | Balanced | Memory-intensive |
|--------|--------|--------|
| 0.125 vCPU \n 0.25 GB | 0.125 vCPU \n 0.5 GB | 0.125 vCPU \n 1 GB |
| 0.25 vCPU \n 0.5 GB | 0.25 vCPU \n 1 GB | 0.25 vCPU \n 2 GB |
| 0.5 vCPU \n 1 GB | 0.5 vCPU \n 2 GB | 0.5 vCPU \n 4 GB |
|  \n 1 vCPU \n 2 GB | _**(default)**_  \n  1 vCPU \n 4 GB |  \n 1 vCPU \n 8 GB |
| 2 vCPU \n 4 GB | 2 vCPU \n 8 GB | 2 vCPU \n 16 GB |
| 4 vCPU \n 8 GB | 4 vCPU \n 16 GB | 4 vCPU \n 32 GB |
| 6 vCPU \n 12 GB | 6 vCPU \n 24 GB |  |
| 8 vCPU \n 16 GB | 8 vCPU \n 32 GB |  |
{: caption="Table 1. Valid vCPU and memory combinations" caption-side="top"}

Your existing apps and jobs might be using other memory and CPU combinations, and those will remain unaffected. However, these other combinations are not valid and only the valid combinations are supported. Therefore, any new apps or jobs as well as any changes to existing apps or jobs must comply with the list of valid choices. 
{: important}


