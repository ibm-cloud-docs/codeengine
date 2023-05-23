---

copyright:
  years: 2023, 2023
lastupdated: "2023-05-23"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why did my app stop running?  
{: #ts-app-end}
{: troubleshoot}

After you deploy an app, the app runs for a while and then ends unexpectedly.
{: tsSymptoms}

Determine whether one of the following cases is true. 
{: tsCauses}


1. Your app code includes an exit when it completes its running cycle.
2. Your app code contains an error that is causing the app to end unexpectedly.
3. The image that your app is pulling from no longer exists because you deleted it or your [image retention policy](/docs/Registry?topic=Registry-registry_retention) in {{site.data.keyword.registrylong_notm}} caused it to be deleted. For example, your app is scaling up because of incoming requests. However, the scale-up fails because the image no longer exists in {{site.data.keyword.registryshort_notm}}. Another typical situation is if your app is on a worker node that is scheduled to receive the latest security fixes. If {{site.data.keyword.codeengineshort}} attempts to move your app to a different worker node and cannot find the image, the move fails and the app stops working.
4. The image that your app is pulling from no longer exists because while the image with the provided tag exists, it was overwritten after an application revision was created. The image that is associated with your specific application revision uses a unique container registry digest, and this digest is used for the life of your application revision. If you create a newer version of the image with the same tag as the original image, the original image is overwritten in the container registry. However, {{site.data.keyword.codeengineshort}} cannot find this newer image, because the newer image has a different digest than the digest for the application revision. No new instances of the application can be created, and this scenario results in a failure of the application.
  

Try the following solutions to resolve your problem.
{: tsResolve}


1. {{site.data.keyword.codeengineshort}} apps are designed to run without exiting. If your app code includes an exit, then consider [running your code as a job](/docs/codeengine?topic=codeengine-job-plan) instead.

2. Check for messages that might help you determine the cause. If you set up logging for {{site.data.keyword.codeengineshort}}, your log files might contain messages. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

  
3. Re-create the image in {{site.data.keyword.registryshort_notm}} and then deploy another instance of your app. Then, check your [image retention policy](/docs/Registry?topic=Registry-registry_retention) in {{site.data.keyword.registryshort_notm}} so that images that are used by active revisions are not deleted. If you are using toolchain templates for {{site.data.keyword.codeengineshort}}, you can also add logic to your pipeline definition to delete unused versions of your image only after a working version is deployed.

4. Create a new revision for your app by [updating your application](/docs/codeengine?topic=codeengine-update-app). If an image is pushed with same tag, then you must update your application to create a new revision that uses this updated image.
  


