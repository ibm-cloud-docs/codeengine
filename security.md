---

copyright:
  years: 2023
lastupdated: "2023-03-17"

keywords: code engine security, security, security features for code engine, code engine security features, code engine iam

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.codeengineshort}} and security
{: #secure}

The [{{site.data.keyword.codeenginefull}} architecture](/docs/codeengine?topic=codeengine-architecture) is built with a security-first mindset. {{site.data.keyword.codeengineshort}} components are [managed and owned by IBM](/docs/codeengine?topic=codeengine-responsibilities-ce). Customers and their workloads are isolated from each other by using projects, which are based on Kubernetes namespaces. Role-based access controls are performed on a resource level to allow only authorized users to perform certain operations on project resources. User access is controlled by {{site.data.keyword.iamshort}} (IAM). Deployed apps are exposed through `HTTPS` and {{site.data.keyword.codeengineshort}} creates and manages the underlying TLS certifications automatically for you. {{site.data.keyword.codeengineshort}} provides out-of-the-box DDOS protection for your application. {{site.data.keyword.codeengineshort}}'s DDOS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you.
{: shortdesc}

{{site.data.keyword.codeengineshort}} jobs cannot be accessed externally by definition. Jobs can still make external requests, though, and they can call {{site.data.keyword.codeengineshort}} applications internally. For an example of a job that calls an application internally, see the [Samples for {{site.data.keyword.codeengineshort}} GitHub repository](https://github.com/IBM/CodeEngine){: external}.
{: note}

You can use the following security features to enhance your security.

| Security feature | Description | 
|-----------|------------------|
| Authorize access with IAM | Grant access to other users for {{site.data.keyword.codeengineshort}} by using {{site.data.keyword.iamshort}} (IAM). {{site.data.keyword.cloud_notm}} IAM provides secure authentication with the {{site.data.keyword.cloud_notm}} platform, {{site.data.keyword.codeengineshort}}, and all the resources in your account. Setting up proper user roles and permissions is key to limit who can access your resources. See [Managing user access](/docs/codeengine?topic=codeengine-iam). | 
| Disable external endpoints | Deploy your application with a disabled external endpoint that is not exposed to external traffic by using the `--visibility=private` or `visibility=project` option. See [Options for visibility for a Code Engine application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility). |
| Store images in private image registries | Set up a private image registry, such as the one provided by {{site.data.keyword.registrylong_notm}}, to control access to the registry and the images that can be deployed in {{site.data.keyword.codeengineshort}}. Scan your images automatically with the [{{site.data.keyword.registrylong_notm}} Vulnerability Advisor](/docs/Registry?topic=Registry-va_index). You can also add access to your own custom private registry. See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). |
| Build code from a private repository | Store your source code in a private repository and then build to {{site.data.keyword.registrylong_notm}}. See [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). |
| Use secrets to store sensitive information | You can store information, such as passwords and SSH keys in a secret. For more information, see [Working with secrets](/docs/codeengine?topic=codeengine-secret).  |
{: caption="Table 1. Security features" caption-side="bottom"}

## Supported TLS versions and cipher suites
{: #secure-tls}

The {{site.data.keyword.codeengineshort}} API and application endpoints support transport layer security (TLS) 1.2 (or higher) and the following cipher suites.

### TLS cipher suites 
{: #secure-cipher-suites}

- `ECDHE-ECDSA-AES128-GCM-SHA256`
- `ECDHE-ECDSA-AES256-GCM-SHA384`
- `ECDHE-RSA-AES128-GCM-SHA256`
- `ECDHE-RSA-AES256-GCM-SHA384`
- `ECDHE-ECDSA-CHACHA20-POLY1305`
- `ECDHE-RSA-CHACHA20-POLY1305`


