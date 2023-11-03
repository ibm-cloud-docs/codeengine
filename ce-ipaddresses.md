---

copyright:
  years: 2023, 2023
lastupdated: "2023-11-03"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.codeengineshort}} public and private IP addresses
{: #network-addresses}

When you deploy your {{site.data.keyword.codeengineshort}} app, job, or function, the workload is deployed to a known list of possible network addresses, depending on the deployment region. You can add these IP addresses to an allowlist in your firewall; however, you must accept the drawbacks and risks that are involved in this action.
{: shortdesc}

- When {{site.data.keyword.codeengineshort}} runs an application or job, it selects an arbitrary system from a large pool of systems for running the workload. Load conditions and system health influence the system selection. Systems are also dynamically added and removed from this pool without warning, making the list of potential network addresses large and dynamic. Your allowlist might not be stable and work reliably. 
- These network addresses are not exclusive to a single tenant and by granting access to these network addresses, you are also granting access for all other workloads, which might be owned by other tenants that are running on {{site.data.keyword.codeengineshort}}. 

Because of these reasons, this approach is not recommended. However, if you accept these risks, then follow these steps to find the network addresses that are used by your {{site.data.keyword.codeengineshort}} workload.

Depending on your scenario, you can send requests to a third-party proxy service. Proxy services provide static IP addresses that you can add to your allowlist. For more information, see [How can I add my {{site.data.keyword.codeengineshort}} application to an allowlist](/docs/codeengine?topic=codeengine-ts-allowlist-app)?
{: tip}
  
You can list all egress IP addresses, both public and private that are used by {{site.data.keyword.codeengineshort}} workloads in a specific project with the {{site.data.keyword.codeengineshort}} API. For more information, see [List egress IP addresses](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-egress-ips).

