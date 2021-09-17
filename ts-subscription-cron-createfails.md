---

copyright:
  years: 2021
lastupdated: "2021-09-17"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, cron, cron event, ping event, ping, object storage

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my `subscription cron create` command failing?
{: #ts-cronsub-create}
{: troubleshoot}

You cannot create a cron subscription through the CLI by using the [**`ibmcloud ce subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command and you receive an error that mentions `failed` in the message.
{: tsSymptoms}

If you cannot create a cron subscription, determine whether one of the following cases is true.
{: tsCauses}

1. The name of your subscription is not unique within the project. 
2. The application or job reference doesn't exist. An error with text similar to the following message appears: `Failed to retrieve the application. View available applications by running ibmcloud ce app list`.

Try one of these solutions.
{: tsResolve}

1. Run the [**`ibmcloud ce sub cron list`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-list) command to list all defined cron subscriptions and check whether a subscription with the same name exists. If a subscription with the same name exists, use the [**`ibmcloud ce sub cron delete --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-delete) command to delete the old subscription. The name of the subscription must be unique within your project.

2. Run [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) or [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) to make sure that your destination app or job exists. If the app or job doesn't exist, create the application with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or create the job with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).



