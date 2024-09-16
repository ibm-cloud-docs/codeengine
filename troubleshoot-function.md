---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-16"

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

## Function return codes
{: #ts-function-return-codes}

Function invocations can return system or application errors. For example, system errors indicate that the function code did not execute successfully, while application errors indicate a problem in the function code itself. See the [{{site.data.keyword.codeengineshort}} functions HTTP return codes](/docs/codeengine?topic=codeengine-fun-work#functions-error) for details on error handling and debugging functions.

## Function limits to consider
{: #ts-function-limits}

When you create functions, you must consider the [Function limits](/docs/codeengine?topic=codeengine-limits#limits_functions).

When you work with applications, functions, and batch jobs, these resources run within the context of a {{site.data.keyword.codeengineshort}} project. Resource quotas are defined on a per project basis, and limits apply for applications, functions, and batch jobs. 

For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

With the CLI, you can use the [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to display information about limits and current usage. For example:

```txt
ibmcloud ce project create --name myproject
```
{: pre}

Example output

```txt
Getting project 'myproject'...
OK

Name:                                      myproject
ID:                         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:                                    active
Enabled:                                   true
Application Private Visibility Supported:  true
Selected:                                  true
Region:                                    us-south
Resource Group:             default
Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
Age:                        52d
Created:                                   Tue, 28 Sep 2021 05:12:16 -0500
Updated:                                   Tue, 28 Sep 2021 05:12:19 -0500

Quotas:
Category                                  Used  Limit
App revisions                             2    120
Apps                                      1     40
Build runs                                1     100
Builds                                    2     100
Configmaps                                2     100
CPU                                       0     128
Ephemeral storage                         0     512G
Functions                                 0     20
Instances (active)                        0     250
Instances (total)                         0     2500
Job runs                                 13     100
Jobs                                      2     100
Memory                                    0     512G
Secrets                                   6     100
Subscriptions (cron)                      0     100
Subscriptions (IBM Cloud Object Storage)  0     100
Subscriptions (Kafka)                     0     100
```
{: screen}


## Getting logs for my function
{: #ts-funcrtion-gettinglogs}

Logs can be helpful to troubleshoot problems when you run functions. You can view function logs from the console.
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} function. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your functions. You can view function logs after you add logging capabilities. For more information, see [viewing function logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-funlogs-ui).

## Keeping your runtime and CLI versions up to date
{: #ts-function-uptodate}

Verify that your runtime is supported. See [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).

## Verifying the code bundle reference for my function
{: #ts-function-verifyimage}

A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image.    ``

When you work with {{site.data.keyword.codeengineshort}} functions, you must specify a code bundle reference and a registry secret to access the image. For the function to work correctly, the code bundle reference and its access properties must remain valid for the life of the function.

Because code bundles and images are similar, you can verify your code bundle in the same ways that you verify an image. See [How can I verify my image reference](/docs/codeengine?topic=codeengine-ts-build-verify-image)?


## Additional topics
{: #ts-function-topics}

You can find more help in the following topics.

- [Troubleshooting overview](/docs/codeengine?topic=codeengine-troubleshooting_over).
- [Debugging builds](/docs/codeengine?topic=codeengine-troubleshoot-build).
