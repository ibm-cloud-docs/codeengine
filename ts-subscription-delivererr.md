---

copyright:
  years: 2022
lastupdated: "2022-11-15"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, cron, ping, object storage, 

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my subscription show errors when it delivers events?
{: #ts-subscription-deliveryerrors}
{: troubleshoot}

Subscription events were created, but errors are received when events are delivered to your {{site.data.keyword.codeengineshort}} application or job.
{: tsSymptoms} 

Check to see whether one of the following cases is true.
{: tsCauses}

1. Does the subscription destination application or job exist? 
2. Is the destination app or job prepared and looking for HTTP POST messages?

Look at the subscription source to see whether any error messages are returned. For {{site.data.keyword.cos_full_notm}} subscriptions, use the [**`ibmcloud ce sub cos get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command. For cron subscriptions, use [**`ibmcloud ce sub cron get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-get) command.
{: tsResolve}

1. Confirm that your subscription destination exists. 

    * If your subscription destination is an application, use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to confirm that your application exists and that it wasn't deleted. Check that the status of your application is `Ready`. You can also use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display the status of the application. 
    * If your subscription destination is a job, use the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to confirm that your job exists. You can also use the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to display the status of the job. 

    For more information about {{site.data.keyword.cos_short}} subscriptions, see [Working with the {{site.data.keyword.cos_short}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer). For more information about cron subscriptions, see [Working with the cron event producer](/docs/codeengine?topic=codeengine-subscribe-cron).

2. The error message that your subscription source receives might include a `404 Not Found` error or a `5xx HTTP` error. If you receive either of these errors, then confirm that your destination application is expecting to receive event information as POST HTTP requests. Event information is received as POST HTTP requests for applications and as environment variables for jobs.

If these solutions do not solve your issue, retrieve the logs of your subscription destination application or job. For apps, use the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command. For jobs, use the  [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command to obtain the logs for your specific jobrun. 

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).


