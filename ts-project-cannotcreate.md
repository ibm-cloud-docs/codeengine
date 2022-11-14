---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-14"

keywords: troubleshooting for code engine projects, projects, tips for projects, accessing projects, tips for creating project

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I create a project?
{: #ts-create-project}
{: troubleshoot}

You cannot create a project in your resource group.
{: tsSymptoms}

If you cannot create a project in your resource group, determine whether one of the following cases is true. 
{: tsCauses}

1. Your project name must be unique in the region. 
2. You might not have the proper platform access to create a project. 
3. The number of projects exceeds the maximum number of projects that you can create per region. 


Try one of these solutions.
{: tsResolve}

1. If you receive a warning message about your project name not being unique, select a different name. 
2. To create a project, you must have `Administrator` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-iam).
3. The maximum number of {{site.data.keyword.codeengineshort}} projects that you can create per region is 20. The maximum number of projects includes projects that are active and any projects that are not permanently deleted, such as projects that are soft deleted. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas). Use the [**`project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command to display all your projects across all regions and the status of these projects. See [deleting a project](/docs/codeengine?topic=codeengine-manage-project#delete-project) for more information about projects that are hard deleted and soft deleted.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).



