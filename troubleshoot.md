---

copyright:
  years: 2020
lastupdated: "2020-07-09"

keywords: code engine, troubleshooting for code engine

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Troubleshooting tips
{: #kn-troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}}.
{: shortdesc}

## Why can't I access a project?
{: #ts-access-project}
{: troubleshoot}

{: tsSymptoms}
You cannot access a project that was created by someone else.

{: tsCauses}
Whenever you use an IBM Cloud account to create or use a project that is not owned by you, you must be assigned proper system roles. 

{: tsResolve}
To perform operations with a project that is not owned by you, you must have `Viewer` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-knative-iam).

## Why can't I create a project?
{: #ts-create-project}
{: troubleshoot}

{: tsSymptoms}
You cannot create a project in your resource group.

{: tsCauses}
There are several reasons why you might not be able to create a project in your resource group.

1. Your project name must be unique in the region. 
2. You might already have a project in the region. During the Experimental release, you are limited to creating a single project in a region.
3. You might not have the proper platform access to create a project. 
</br>

{: tsResolve}
Try one of these solutions.

1. If you receive a warning message about your project name not being unique, select a different name. 
2. You can create only one project per region. For more information, see [Experimental release limitations](/docs/codeengine?topic=codeengine-kn-limits#kn-limits_experimental).
3. In order to create a project, you must have `Administrator` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-knative-iam).

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).
