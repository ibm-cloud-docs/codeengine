---

copyright:
  years: 2023
lastupdated: "2023-02-01"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials, secrets

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging service bindings
{: #troubleshoot-servicebindings}
{: troubleshoot}

Use the tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} service bindings.
{: shortdesc}

## Limits to consider 
{: #ts-sb-limits}

When you create service bindings with {{site.data.keyword.codeengineshort}}, secrets are created. Every new service binding that does not reuse a service credential creates a secret. The maximum number of secrets per project is 100 secrets.

For more information about limits for secrets, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Be sure to also consider limits for the specific service instance that you are binding to.
{: important}

For more information about service bindings, see [Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding).



