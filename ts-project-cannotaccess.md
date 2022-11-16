---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-16"

keywords: troubleshooting for code engine projects, projects, tips for projects, accessing projects, tips for creating project

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I access a project?
{: #ts-access-project}
{: troubleshoot}

You cannot access a project that was created by someone else.
{: tsSymptoms}

Whenever you use an {{site.data.keyword.cloud_notm}} account to create or use a project that is not owned by you, you must be assigned proper system roles. 
{: tsCauses}

To perform operations with a project that is not owned by you, you must have `Viewer` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-iam).
{: tsResolve}



