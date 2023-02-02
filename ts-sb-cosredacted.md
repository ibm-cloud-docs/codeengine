---

copyright:
  years: 2023
lastupdated: "2023-02-02"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do the service credentials in my service binding to {{site.data.keyword.cos_full_notm}} show as `REDACTED`?
{: #ts-sb-cosredacted}
{: troubleshoot}

When you create a {{site.data.keyword.codeengineshort}} service binding with an {{site.data.keyword.cos_full_notm}} service instance, the service credentials show as `REDACTED`.

After you create a service binding to an {{site.data.keyword.cos_short}} instance and you use your own service credential, the service credentials for the binding to your {{site.data.keyword.codeengineshort}} app or job shows as `REDACTED` in the environment variables, instead of showing the service credential values.
{: tsSymptoms}

To retrieve existing service credentials, {{site.data.keyword.cos_short}} requires that the user (or service ID) that retrieves the service credential must have the additional IAM action of `resource-controller.credential.retrieve_all`. This IAM action is included in the `COS Reader` or the Platform `Administrator` access role.
{: tsCauses}

Try one of these solutions.
{: tsResolve}

1. Do not use custom service credentials when you create service bindings to {{site.data.keyword.cos_short}} with {{site.data.keyword.codeengineshort}}. Instead, use the default service binding access policies and let {{site.data.keyword.codeengineshort}} generate the credentials for you. See [Using the default service binding access policies](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-auto-servid).

2. If you want to use a custom service ID with {{site.data.keyword.codeengineshort}} service bindings, you must also add the `COS Reader` service access when you assign access for the service ID. See [Using a custom service ID for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-custom-servid).




