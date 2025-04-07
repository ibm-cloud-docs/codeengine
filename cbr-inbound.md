---

copyright:
  years: 2025
lastupdated: "2025-04-07"

keywords: connectivity, inbound connections, inbound connectivity, private, private inbound connectivity

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Restricting inbound traffic to {{site.data.keyword.codeengineshort}} applications and functions with context-based restrictions
{: #cbr-inbound}

 This feature is a beta feature and is available for evaluation and testing purposes only.
 {: beta}

 You can restritct inbound traffic to your {{site.data.keyword.codeenginefull}} applications and functions by using {{site.data.keyword.cloud_notm}} context-based rules to restrict access to your {{site.data.keyword.codeengineshort}} applications or functions. This feature is not supported for {{site.data.keyword.codeengineshort}} jobs. Instead of assigning access, context-based restrictions check that an access request comes from an allowed context that you configure. You can limit inbound traffic to your applications and functions within your {{site.data.keyword.codeengineshort}} projects to [safeguard your projects from unwanted inbound traffic](/docs/codeengine?topic=codeengine-cbr).
{: shortdesc}

When you secure {{site.data.keyword.codeengineshort}} resources with context-based restrictions with private endpoints, in addition to restricting the inbound traffic that connects to your application or functions with context-based rules, you can [restrict who can manage your {{site.data.keyword.codeengineshort}} resources](/docs/codeengine?topic=codeengine-cbr), such as deploying or updating applications and secrets.
{: tip}

Context-based restrictions for {{site.data.keyword.codeengineshort}} can be scoped to a single project, an entire resource group, or a location (region). You can also limit which of your services can be accessed from {{site.data.keyword.codeengineshort}}. For more information about {{site.data.keyword.cloud_notm}} context-based restrictions, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

When a context-based restriction rule covers a resource group or a location, the restrictions apply to existing projects. If you create a new project in the same location or resource group, you must update the rule (without making any changes) to apply the restrictions to the new project. Note that you do not have to change the rule; simply click **Edit** and then **Apply** to ensure the new project is associated with the restrictions.
{: Important}

## Creating a context-based restriction for your {{site.data.keyword.codeengineshort}} resources
{: #add-cbr-ui}

To create a context-based restriction, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create). The following steps are specific to creating one for {{site.data.keyword.codeengineshort}} resources.

1. Go to the Context-based restrictions [Rules page](https://cloud.ibm.com/context-based-restrictions/rules).

2. Click **Create** to create a new rule for the context-based restriction, starting with the service.

3. Select **Code Engine** for **Services** and click **Next** to select the service APIs to protect.

4. Restrict access to protect your {{site.data.keyword.codeengineshort}} application or function workloads by selecting the **Data plane** option for **Service APIs**.

    You define workload restrictions at the data plane level, so select at least the data plane service. You can also select other service or platform APIs.

    Click **Next** to scope the restriction for your resources.

5. Apply the restriction to a single project, the entire resource group, or a location (region) where you have multiple projects. Apply this scope in the **Resources** section and click **Review** to proceed.

6. Click **Continue** to add context to your rule.

7. {{site.data.keyword.codeengineshort}}'s data plane API provides restrictions for private workloads, not public ones. By default, all public workloads remain accessible. For your context-based restriction to restrict private inbound connections, and also keep all public endpoints accessible, you must create an empty public context. Without this empty public endpoint, you encounter rule setup errors. To create an empty public context:
    1. Set **Endpoints** to on.
    2. Select **Public**.
    3. Leave **Network zones** empty. Make sure that no network zones are enabled in this section so that all public endpoints are accessible.

    You can restrict private endpoints, if wanted:
    * To deny all access to private endpoints within your project, make sure that only the empty public context exists and no private contexts are set.
    * To restrict private workloads within your project, select the list of network zones that you want to allow (for example, you can allow a VPC to access private networks in your {{site.data.keyword.codeengineshort}} project).
    * IPv6 restrictions are not supported for {{site.data.keyword.codeengineshort}}.

8. Click **Continue** to provide rule details.

9. Provide a name or description for your rule.

10. Select **Enabled** for **Enforcement**.

11. Review the summary and click **Create**.

## Testing your context-based restriction rule for private inbound connectivity
{: #test-cbr}

After you create the context-based restriction rule, you can test it using your private application or function. Access is only granted to allowlisted IP addresses. If a request comes from an IP address that is not allowlisted, you see an `RBAC Access Denied` error message. For example, if you allowed only `9.9.9.9/32`, then your application or function is accessible only from that IP range. Anything outside of that range encounters the error message.

If you selected a network zone that points to a VPC (virtual private cloud), you must also create a VPE (virtual private endpoint) gateway to allow the VPC to access private workloads. After you create the gateway, you can experience a temporary delay due to PDNS resolution. You can see `RBAC Access Denied` error messages initially, but you will be granted access after a bit of time.
{: tip}
