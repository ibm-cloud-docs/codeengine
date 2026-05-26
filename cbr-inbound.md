---

copyright:
  years: 2026
lastupdated: "2026-05-26"

keywords: connectivity, inbound connections, inbound connectivity, private, public, context-based restrictions, cbr, network restrictions

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Restricting inbound traffic to applications and functions using context-based restrictions
{: #cbr-inbound}

You can use {{site.data.keyword.cloud}} context-based restrictions (CBR) to control inbound network traffic to your {{site.data.keyword.codeenginefull}} applications and functions. With CBR, you can restrict access through private endpoints, public endpoints, or both, providing flexible network-level security for your workloads. Instead of assigning access based on identity, context-based restrictions verify that an access request comes from an allowed context that you configure. You can limit inbound traffic to your applications and functions within your {{site.data.keyword.codeengineshort}} projects to [safeguard your projects from unwanted inbound traffic](/docs/iam?topic=iam-context-restrictions-create). These context-based restrictions apply at either account, project, resource group, or location (region) level and apply for all applications and functions within the scope of the restriction.
{: shortdesc}

Context-based restrictions for {{site.data.keyword.codeengineshort}} applications and functions support the following use-cases:

- **Block public inbound entirely**: Restrict your applications and functions to be accessible only through their private endpoint via CBR. This approach eliminates the need to configure [application endpoint visibility](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility) settings, as public access is blocked at the network level. Your workloads remain accessible from private networks (such as VPCs) and from other {{site.data.keyword.codeengineshort}} components within the same project.

- **Block public and restrict private by IP**: Achieve maximum control over inbound traffic by blocking all public internet access and restricting private endpoint access to specific IP addresses or network zones. This combines the capability of IP-based restrictions for private endpoints with the ability to block public endpoints entirely at the network level.

- **Isolate workloads entirely**: Block both private and public endpoints to completely isolate your applications and functions at the network level. This use case is ideal for scenarios such as batch processing workloads that only need to make outbound connections, internal microservices that communicate exclusively through message queues or event subscriptions, or workloads undergoing maintenance where you want to prevent all inbound traffic temporarily while keeping the application deployed.

Context-based restrictions apply only to applications and functions because these workloads expose network endpoints. Context-based restrictions do not apply to jobs and fleets since they are not exposing any network endpoints.
{: note}

When you secure {{site.data.keyword.codeengineshort}} resources with context-based restrictions, in addition to restricting the inbound traffic that connects to your applications or functions with context-based rules, you can [restrict the contexts (network paths) from which your {{site.data.keyword.codeengineshort}} resources](/docs/codeengine?topic=codeengine-cbr) can be managed, such as deploying or updating applications and secrets.
{: tip}

Context-based restrictions for {{site.data.keyword.codeengineshort}} can be scoped to a single project, an entire resource group, or a location (region). For more information about {{site.data.keyword.cloud_notm}} context-based restrictions, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

When a context-based restriction rule covers a resource group or a location (region), the restrictions apply to existing projects. If you create a new project in the same location or resource group, the restrictions are automatically applied to the new project. It can take a few minutes for the new project to be associated with the restrictions. To observe the CBR rules are applied, check the project status connectivity section in the UI, CLI, or API.
{: Important}

## Creating a context-based restriction for your {{site.data.keyword.codeengineshort}} resources
{: #create-cbr}

You can create context-based restrictions for your {{site.data.keyword.codeengineshort}} resources by using the {{site.data.keyword.cloud_notm}} console, CLI, API, SDKs, or Terraform. For more information about creating context-based restrictions, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create). The following sections provide specific guidance for creating restrictions for {{site.data.keyword.codeengineshort}} applications and functions.

IPv6 restrictions are not supported for {{site.data.keyword.codeengineshort}}.
{: note}

### Adding a context-based restriction using the UI
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

7. Configure contexts to define which endpoints are restricted. Choose one of the following scenarios based on your security requirements:

    - **Use-case A: Block public inbound entirely**

      Use this use-case to make your applications and functions accessible only through their private endpoint, eliminating public internet access at the network level.

      1. Set **Endpoints** to on.
      2. Select **Private** (allow traffic).
      3. Leave **Public** deselected (block traffic).
      4. Leave **Network zones** empty. Make sure that no network zones are enabled in this section so that all private endpoints remain accessible.
      5. Click **Add** to create a new context.

    - **Use-case B: Block public and restrict private by IP**

      Use this use-case to achieve maximum control by blocking all public internet access and restricting private endpoint access to specific IP addresses or network zones.

      1. Set **Endpoints** to on.
      2. Select **Private** (allow traffic).
      3. Leave **Public** deselected (block traffic).
      4. Select the network zones you want to allow for private access (for example, specific VPCs or IP ranges).
      5. Click **Add** to create a new context.

    - **Use-case C: Isolate workloads entirely**

      Use this use-case to completely isolate your applications and functions at the network level by blocking both private and public endpoints. This is useful for batch processing workloads that only make outbound connections, internal microservices that communicate exclusively through message queues or events, or workloads undergoing maintenance.

      1. Set **Endpoints** to on.
      2. Leave **Private** deselected (block traffic).
      3. Leave **Public** deselected (block traffic).
      4. Leave **Network zones** empty. An empty public context with no network zones blocks all public access.
      5. Click **Add** to create a new context.

8. Click **Continue** to provide rule details.

9. Provide a description for your rule.

10. Select **Enabled** for **Enforcement**.

11. Review the summary and click **Create**.

### Adding a context-based restriction using the CLI
{: #add-cbr-cli}

You can use the IBM Cloud CLI to create context-based restrictions for your {{site.data.keyword.codeengineshort}} resources. Before you begin, make sure you have the [IBM Cloud CLI installed](/docs/cli?topic=cli-install-ibmcloud-cli) and the context-based restrictions plug-in installed by running `ibmcloud plugin install cbr`.

- **Use-case A: Block public inbound entirely**

  Use this use-case to make your applications and functions accessible only through their private endpoint, eliminating public internet access at the network level.

  Create a rule that allows private access and blocks public access:

  ```txt
  ibmcloud cbr rule-create --description "Block public inbound entirely" \
  	--service-name codeengine \
  	--api-types crn:v1:bluemix:public:context-based-restrictions::::api-type:data-plane \
  	--context-attributes endpointType=private
  ```
  {: pre}

- **Use-case B: Block public and restrict private by IP**

  Use this use-case to achieve maximum control by blocking all public internet access and restricting private endpoint access to specific IP addresses or network zones. Check `ibmcloud cbr zones` for available zone IDs.

  Create a rule that restricts private access to specific zones and blocks public access:

  ```txt
  ibmcloud cbr rule-create --description "Block public and restrict private by IP" \
  	--service-name codeengine \
  	--api-types crn:v1:bluemix:public:context-based-restrictions::::api-type:data-plane \
  	--context-attributes endpointType=private \
  	--zone-id <zone-id>
  ```
  {: pre}

- **Use-case C: Isolate workloads entirely**

  Use this use-case to completely isolate your applications and functions at the network level by blocking both private and public endpoints. This is useful for batch processing workloads that only make outbound connections, internal microservices that communicate exclusively through message queues or events, or workloads undergoing maintenance.

  To block all inbound traffic, create a rule with no contexts (an empty rule blocks all access):

  ```txt
  ibmcloud cbr rule-create --description "Isolate workloads entirely" \
  	--service-name codeengine \
  	--api-types crn:v1:bluemix:public:context-based-restrictions::::api-type:data-plane
  ```
  {: pre}

Context-based restriction rule cover the entire account, project, resource group, or location (region). Use `--resource-attributes` to specify the level at which the rule applies, e.g. `--resource-attributes "projectId=<your-project-id>"` to apply at project level.
{: note}

## Testing your context-based restriction rule for private inbound connectivity
{: #test-cbr}

After you create the context-based restriction rule, you can test it using your application or function:

- **If you blocked public endpoints**: Attempts to access your application or function through its public URL result in an `RBAC Access Denied` error message. Your workload remains accessible through private endpoints (from VPCs or other {{site.data.keyword.codeengineshort}} components in the same project).

- **If you restricted private endpoints by IP**: Access through private endpoints is only granted to allowlisted network zones or IP addresses. If a request comes from a source that is not allowlisted, you see an `RBAC Access Denied` error message. For example, if you allowed only `9.9.9.9/32`, then your application or function is accessible only from that IP range through the private endpoint. Anything outside of that range encounters the error message.

If you selected a network zone that points to a VPC (virtual private cloud), you must also create a VPE (virtual private endpoint) gateway to allow the VPC to access private workloads. After you create the gateway, you can experience a temporary delay due to PDNS resolution. You can see `RBAC Access Denied` error messages initially, but you will be granted access after a bit of time.
{: tip}
