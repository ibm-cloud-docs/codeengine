---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-28"

keywords: troubleshooting for code engine, troubleshooting functions in code engine, function in code engine, function

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging functions
{: #troubleshoot-function}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} functions.
{: shortdesc}

## Function limits to consider 
{: #ts-function-limits}

When you create functions, you must consider the [Function limits](/docs/codeengine?topic=codeengine-limits#limits_functions).

When you work with applications, functions, and batch jobs, these resources run within the context of a {{site.data.keyword.codeengineshort}} project. Resource quotas are defined on a per project basis, and limits apply for applications, functions, and batch jobs. 

For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).


## Getting logs for my function 
{: #ts-funcrtion-gettinglogs}

Logs can be helpful to troubleshoot problems when you run functions. You can view function logs from the console. 
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} function. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your functions. You can view function logs after you add logging capabilities. For more information, see [viewing function logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-funlogs-ui).

## Keep your runtime and CLI versions up to date
{: #ts-function-uptodate}

Verify that your runtime continues to be supported. See [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).  In addition, keep your CLI up to date. See [Updating the CLI](/docs/codeengine?topic=codeengine-install-cli#update-cli).
