---

copyright:
  years: 2023, 2023
lastupdated: "2023-11-03"

keywords: troubleshooting for code engine functions, allowlist, tips for functions and allowlists, proxy service, allowlist functions

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I add my {{site.data.keyword.codeengineshort}} function to an allowlist?
{: #ts-allowlist-function}
{: troubleshoot}

Your {{site.data.keyword.codeengineshort}} workload needs to access a protected resource. You need to create an allowlist for your {{site.data.keyword.codeengineshort}} workload. How can you find the IP addresses that your {{site.data.keyword.codeengineshort}} workload uses?

When you deploy your {{site.data.keyword.codeengineshort}} app, job, or function, the workload is deployed to a known list of possible network addresses, depending on the deployment region. You can add these IP addresses to an allowlist in your firewall; however, you must accept the drawbacks and risks that are involved in this action.
{: tsCauses}

- When {{site.data.keyword.codeengineshort}} runs an application, job, or function, it selects an arbitrary system from a large pool of systems for running the workload. Load conditions and system health influence the system selection. Systems are also dynamically added and removed from this pool without warning, making the list of potential network addresses large and dynamic. Your allowlist might not be stable and work reliably. 
- These network addresses are not exclusive to a single tenant and by granting access to these network addresses, you are also granting access for all other workloads, which might be owned by other tenants that are running on {{site.data.keyword.codeengineshort}}. 

Consider instead to send requests to a third-party proxy service. Proxy services provide static IP addresses that you can add to your allowlist. When you purchase a proxy service, you receive credentials for the proxy. Configure your workload to send all requests to the proxy by using the proxy credentials. The proxy service uses a unique, static IP address as the sender address when it forwards all requests to the target service. Because these IP addresses are static, they are stable to use in an allowlist.
{: tsResolve}

If this scenario does not work for you and you want to accept the risks previously stated, you can list all egress IP addresses, both public and private that are used by {{site.data.keyword.codeengineshort}} workloads in a specific project with the {{site.data.keyword.codeengineshort}} API. For more information, see [List egress IP addresses](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-egress-ips){: external}.

