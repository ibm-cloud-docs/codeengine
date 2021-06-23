---

copyright:
  years: 2021
lastupdated: "2021-06-23"

keywords: code engine security, security

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# {{site.data.keyword.codeengineshort}} and security
{: #secure}

The [{{site.data.keyword.codeenginefull}} architecture](/docs/codeengine?topic=codeengine-architecture) is built with a security-first mindset. {{site.data.keyword.codeengineshort}} components are [managed and owned by IBM](/docs/codeengine?topic=codeengine-responsibilities-ce). Customers and their workloads are isolated from each other by using projects, which are based on Kubernetes namespaces. Role-based access controls are performed on a resource level to allow only authorized users to perform certain operations on project resources. User access is controlled by {{site.data.keyword.iamshort}} (IAM). Deployed apps are exposed through `HTTPS` and {{site.data.keyword.codeengineshort}} creates and manages the underlying TLS certifications automatically for you.
{: shortdesc}

{{site.data.keyword.codeengineshort}} jobs cannot be accessed externally by definition. Jobs can still make external requests, though, and they can call {{site.data.keyword.codeengineshort}} applications internally. For more information and an example of a job calling an application internally, see the [Samples for {{site.data.keyword.codeengineshort}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: note}

You can use the following security features to enhance your security.

| Security feature | Description | 
|-----------|------------------|
| Authorize access with IAM | Grant access to other users for {{site.data.keyword.codeengineshort}} by using {{site.data.keyword.iamshort}} (IAM). {{site.data.keyword.cloud_notm}} IAM provides secure authentication with the {{site.data.keyword.cloud_notm}} platform, {{site.data.keyword.codeengineshort}}, and all the resources in your account. Setting up proper user roles and permissions is key to limit who can access your resources. See [Managing user access](/docs/codeengine?topic=codeengine-iam). | 
| Disable external endpoints | Deploy your application with a disabled external endpoint that is not exposed to external traffic by using the `--cluster-local` option. See [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-endpoint). |
| Store images in private image registries | Set up a private image registry, such as the one provided by {{site.data.keyword.registrylong_notm}}, to control access to the registry and the images that can be deployed in {{site.data.keyword.codeengineshort}}. Scan your images automatically with the [{{site.data.keyword.registrylong_notm}} Vulnerability Adviser](/docs/Registry?topic=va-va_index). You can also add access to your own custom private registry. See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). |
| Build code from a private repository | Store your source code in a private repository and then build to {{site.data.keyword.registrylong_notm}}. See [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). |
| Use secrets to store sensitive information | You can store information, such as passwords and SSH keys in a secret. For more information, see [Setting up and using secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret). |
{: caption="Table 1. Security features" caption-side="top"}

