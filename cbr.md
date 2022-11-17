---

copyright:
  years:  2022, 2022
lastupdated: "2022-11-17"

keywords: code engine, context-based restrictions, access, protect resources, cbr

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Protecting {{site.data.keyword.codeengineshort}} resources with context-based restrictions
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.codeenginefull}} resources can be controlled with context-based restrictions and identity and access management policies.
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Because both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

You must have the `Administrator` role on a service to create, update, or delete rules. Additionally, you must have either the `Editor` or `Administrator` role to create, update, or delete network zones.
{: note}

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated comes from the context-based restrictions service and not {{site.data.keyword.codeengineshort}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

To get started protecting your {{site.data.keyword.codeengineshort}} resources with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial).

Context-based restrictions for {{site.data.keyword.codeengineshort}} can be scoped to a location (region), project, or resource group. You can also limit which of your services can be accessed from {{site.data.keyword.codeengineshort}}.
{: note}


