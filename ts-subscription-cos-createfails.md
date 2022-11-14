---

copyright:
  years: 2022
lastupdated: "2022-11-14"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, ping, object storage

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my `subscription cos create` command failing?
{: #ts-cossub-create}
{: troubleshoot}

You cannot create an {{site.data.keyword.cos_full_notm}} subscription through the CLI by using the 
[**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command and you receive an error that mentions `failed` in the message.
{: tsSymptoms}

If you cannot create an {{site.data.keyword.cos_short}} subscription, determine whether one of the following cases is true,
{: tsCauses}

1. The name of your subscription is not unique within the project. 

2. The application or job reference doesn't exist. An error with text similar to the following message appears: `Failed to retrieve the application. View available applications by running ibmcloud ce app list`.

3. A timeout occurs. Error message mentions `Getting COS event subscription status timed out`

Try one of these solutions.
{: tsResolve}

1. Run the [`ibmcloud ce sub cos list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-list) command to list all defined {{site.data.keyword.cos_short}} subscriptions and check whether a subscription with the same name exists. If a subscription with the same name exists, run the [`ibmcloud ce sub cos delete --name SUB_NAME`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) to delete the old subscription. The name of the subscription must be unique within your project.

2. Run [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) or [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) to make sure that your destination app or job exists. If the app or job doesn't exist, create the application with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or create the job with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

3. Try the solutions in [Why does my {{site.data.keyword.cos_short}} subscription never become ready?](/docs/codeengine?topic=codeengine-ts-cossub-notready)



