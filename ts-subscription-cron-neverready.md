---

copyright:
  years: 2022
lastupdated: "2022-11-17"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, cron, cron event, ping event, ping, object storage

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my cron subscription never become ready?
{: #ts-cronsub-notready}
{: troubleshoot}

A cron subscription was created, but it does not have a `ready` status.
{: tsSymptoms}

The destination app or job does not exist.
{: tsCauses}


Check the cron subscription to see whether any error messages are returned by using the [**`ibmcloud ce sub cron get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-get) command. 
{: tsResolve}

If the error message shows `NotFound : Sink not found`, then your destination app or job is not available. Use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) or the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) command to verify that your destination app exists. If the app or job doesn't exist, create the application with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or create the job with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).


