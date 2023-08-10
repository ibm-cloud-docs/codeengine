---

copyright:
  years: 2023, 2023
lastupdated: "2023-08-10"

keywords: troubleshooting for code engine, troubleshooting applications in code engine, tips for applications in code engine, debugging applications in code engine, custom domain mapping and code engine

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why did my app restart? 
{: #ts-app-restart}
{: troubleshoot}

My app is running, but I see that app instances are restarted. 
{: tsSymptoms}

When an application restart occurs, {{site.data.keyword.codeengineshort}} automatically starts a new instance of the app. When your new app instance is marked as `Ready`, {{site.data.keyword.codeengineshort}} routes traffic to it.

If your app is restarted, determine whether one of the following cases is true. 
{: tsCauses}


1. An exception occurred and it is not handled in your application source code.

2. Your {{site.data.keyword.codeengineshort}} system memory configuration is constrained for resources. For example, the memory setting per instance is set too low, so the instance experiences restarts due to out of memory errors.

3. Because {{site.data.keyword.codeengineshort}} is a fully managed {{site.data.keyword.cloud_notm}} environment, applications, and other {{site.data.keyword.codeengineshort}} workloads might get relocated to another physical location; for example, to apply security fixes. Given the managed nature of the environment, these types of changes can occur at any time. When you are working with deployed applications, actions of this type can cause your application to restart.


Try one of these solutions.
{: tsResolve}


1. If an exception occurred, take the following actions.
    * Check for messages that might help you determine what is happening. If you set up logging for {{site.data.keyword.codeengineshort}}, your log files might contain messages. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).
    * After you update your application source code and build an updated container image, create a new revision for your app by [updating your application](/docs/codeengine?topic=codeengine-update-app).
    * Use the detailed views of your application instances to help you in troubleshooting your apps. Use the {{site.data.keyword.codeengineshort}} console to view details of your app instances. See [Getting details about app instances](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-instancedetails).


2. If your application is constrained for memory resources, take the following actions.
    * Be aware of {{site.data.keyword.codeengineshort}} limits. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). If needed, [update your application](/docs/codeengine?topic=codeengine-update-app) to change the memory settings for your app.
    * Check the resource settings for your app and modify as needed. See [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
    * Use the detailed views of your application instances to help you in troubleshooting your apps. Use the {{site.data.keyword.codeengineshort}} console to view details of your app instances. See [Getting details about app instances](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-instancedetails).

3. In general, you cannot rely on specific application instances to run without interruption in the managed {{site.data.keyword.codeengineshort}} environment. You can make sure that your app follows the [12-factor app methodology](https://12factor.net/){: external} to avoid downtime with your app during these types of system upgrades. See [Why did my app stop running](/docs/codeengine?topic=codeengine-ts-app-end)?






