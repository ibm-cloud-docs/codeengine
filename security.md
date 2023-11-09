---

copyright:
  years: 2023
lastupdated: "2023-11-09"

keywords: code engine security, security, security features for code engine, code engine security features, code engine iam

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.codeengineshort}} and security
{: #secure}

The [{{site.data.keyword.codeenginefull}} architecture](/docs/codeengine?topic=codeengine-architecture) is built with a security-first mindset. {{site.data.keyword.codeengineshort}} components are [managed and owned by IBM](/docs/codeengine?topic=codeengine-responsibilities-ce). Customers and their workloads are isolated from each other by using projects, which are based on Kubernetes namespaces. Role-based access controls are performed on a resource level to allow only authorized users to perform certain operations on project resources. User access is controlled by {{site.data.keyword.iamshort}} (IAM). Deployed apps are exposed through `HTTPS` and {{site.data.keyword.codeengineshort}} creates and manages the underlying TLS certifications automatically for you. {{site.data.keyword.codeengineshort}} provides immediate DDoS protection for your application. {{site.data.keyword.codeengineshort}}'s [DDoS protection](#secure-ddos) is provided by {{site.data.keyword.cis_short}} at no additional cost to you.
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
| Use secrets to store sensitive information | You can store information, such as passwords and SSH keys in a secret. For more information, see [Working with secrets](/docs/codeengine?topic=codeengine-secret). |
| Add authentication and authorization capabilities | If you are exposing your application or function in {{site.data.keyword.codeengineshort}} on a public API or website, you might want to restrict access to certain users or locations (IP address ranges). While {{site.data.keyword.codeengineshort}} provides capabilities to restrict access for APIs that you can use to manage {{site.data.keyword.codeengineshort}} projects and its entities, it is the responsibility of the owner of the code source to add proper authentication and authorization capabilities to protect the code that runs when reaching the endpoints. For example, you can use [{{site.data.keyword.appid_full_notm}}](/docs/appid) to add authentication and authorization capabilities for your code. |
| Rotate TLS certificates regularly | If you are using custom domain mappings to expose your applications or functions, you must ensure that your TLS certificates have an expiry date; for example 90 days. You must periodically rotate your certificate with an updated certificate (that has its own expiry date). Ideally, use automation to rotate the certificates. For example, you can use a {{site.data.keyword.codeengineshort}} job that is triggered by a cron subscription to rotate the certificate. If you store secrets in {{site.data.keyword.secrets-manager_full_notm}}, consider using {{site.data.keyword.en_full_notm}} so that your {{site.data.keyword.codeengineshort}} project is aware of certificate rotations. You can find a [sample app that uses event notifications](https://github.com/IBM/CodeEngine/tree/main/app-n-event-notification){: external} by visiting our {{site.data.keyword.codeengineshort}} samples repository on GitHub. |
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

## DDoS protection 
{: #secure-ddos}

{{site.data.keyword.codeengineshort}} provides immediate DDoS protection for your application. {{site.data.keyword.codeengineshort}}'s DDoS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you.

DDoS protection covers System Interconnection (OSI) Layer 3 and Layer 4 (TCP/IP) protocol attacks, but not Layer 7 (HTTP) attacks. 

To address Layer 7 attacks, you can take the following steps so that your traffic runs through a secure route using your custom domain and is no longer available to the public internet through the {{site.data.keyword.codeengineshort}} provided domain.

1. Obtain your custom domain.
2. In {{site.data.keyword.codeengineshort}}, [create a custom domain mapping](/docs/codeengine?topic=codeengine-domain-mappings) for your app.
3. Set up an instance of [{{site.data.keyword.cis_short}}](https://cloud.ibm.com/catalog/services/internet-services){: external} to manage your custom domain.
4. [Add the custom domain to the {{site.data.keyword.cis_short_notm}} instance](/docs/cis?topic=cis-multi-domain-support).
5. [Configure a global load balancer](/docs/cis?topic=cis-configure-glb) in {{site.data.keyword.cis_short_notm}}.
6. [Enable the HTTP proxy mode for the load balancer](/docs/cis?topic=cis-proxy-modes) in {{site.data.keyword.cis_short_notm}}. This activates DDoS protection on Layer 7 and other {{site.data.keyword.cis_short_notm}} security features.
7. In {{site.data.keyword.codeengineshort}}, turn off the public system provided domain mappings of your application. Go to your application, from the **Domain mapping** tab for your app, select **No external system domain mapping**.
8. Click **Create** to save the application revision. 

For more information about DDoS in {{site.data.keyword.cis_short_notm}}, see [Dealing with Distributed Denial of Service attacks in {{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-distributed-denial-of-service-ddos-attack-concepts). For more ways to address Layer 7 attacks, see [Mitigating Layer 7 attacks in {{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis#cis-mitigate-layer7-attacks). 



