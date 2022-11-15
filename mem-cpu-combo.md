---

copyright:
  years: 2022
lastupdated: "2022-11-15"

keywords: applications in code engine, apps in code engine, job in code engine, memory and cpu combinations, memory in code engine, cpu in code engine, memory and CPU

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Supported memory and CPU combinations
{: #mem-cpu-combo}

{{site.data.keyword.codeenginefull}} applications and jobs consume CPU and memory. These amounts can vary, depending on if your app is compute-intensive, memory-intensive, or balanced.
{: shortdesc}



The use of ephemeral storage is now bounded by memory. The ephemeral storage in {{site.data.keyword.codeengineshort}} cannot exceed the default value of 0.4 GB (400 MB) or the configured value for memory. If you need more than the default for ephemeral storage, you must increase your memory according to the valid combinations of vCPU and memory.
{: important}


Consider the following examples of setting valid values for ephemeral storage:

* If memory is set to 0.25 GB, you can set ephemeral storage up to the default value of 0.4 GB.
* If ephemeral storage is set to 0.4 GB and memory is set to 2 GB, and you want to reduce the memory to 0.25 GB, this operation is valid because the ephemeral storage is set to its default value.
* If ephemeral storage is set to 0.5 GB and memory is set to 2 GB, and you want to reduce the memory to 0.25 GB, this operation is not valid because the ephemeral storage is now greater than the memory and its default of 0.4 GB. The ephemeral storage cannot exceed the default value of 0.4 GB or the configured value for memory.
* If ephemeral storage is set to 1 GB and memory is set to 4 GB, and you want to increase the ephemeral storage to 4 GB, this operation is valid because the ephemeral storage is less than or equal to the memory.
* If ephemeral storage is set to 1 GB and memory is set to 4 GB, and you want to reduce the memory to 2 GB, this operation is valid because the ephemeral storage is less than or equal to the memory.


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
| 6 vCPU \n 12 GB | 6 vCPU \n 24 GB | 6 vCPU \n 48 GB  |
| 8 vCPU \n 16 GB | 8 vCPU \n 32 GB |  |
| 10 vCPU \n 20 GB | 10 vCPU \n 40 GB |  |
| 12 vCPU \n 24 GB | 12 vCPU \n 48 GB |  |
{: caption="Table 1. Valid vCPU and memory combinations" caption-side="top"}

Your existing apps and jobs might be using other memory and CPU combinations, and those will remain unaffected. However, these other combinations are not valid and only the valid combinations are supported. Therefore, any new apps or jobs as well as any changes to existing apps or jobs must comply with the list of valid choices. 
{: important}


