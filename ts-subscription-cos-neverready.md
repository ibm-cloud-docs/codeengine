---

copyright:
  years: 2024
lastupdated: "2024-10-15"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, ping, object storage

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my {{site.data.keyword.cos_short}} subscription never become ready?
{: #ts-cossub-notready}
{: troubleshoot}

A `cos` subscription was created, but it does not have a `ready` status.
{: tsSymptoms}

Check to see whether one of the following cases is true.
{: tsCauses}

1. The Notifications Manager role is not set for your account nor project. 
2. The {{site.data.keyword.cos_short}} bucket doesn't exist, is not set to `regional` resiliency, or exists in a different region as the project.
3. An application or job is missing.

Look at the subscription source to see whether any error messages returned by running the [**`ibmcloud ce sub cos get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command.
{: tsResolve}

1. If the error message includes `Verify you have assigned the Notifications Manager role to your project`,
    1. Go to [Manage access and users](https://cloud.ibm.com/iam/overview) and click **Authorizations**.
    2. Click **Create**.
    3. Select `Code Engine` as the Source Service and `Cloud Object Storage` as the Target Service. 
    4. Be sure to select the **Notifications Manager** service access checkbox.
    5. Click **Authorize**.

2. If the error message includes `Error accessing bucket in region`, check the region that your project is in by running [`ibmcloud ce project current`](/docs/codeengine?topic=codeengine-cli#cli-project-current). Find your bucket region by running [`ibmcloud cos bucket-location-get --bucket BUCKET_NAME`](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-find-bucket). Both the project and bucket must be in the same region. In addition, be sure that the resiliency is set to `regional`.

3. If the error message shows `NotFound : Sink not found`, then your destination app or job is not available. Run the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command or the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) command to make sure that your destination app or job exists. If the app or job doesn't exist, create the application with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or create the job with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

If these solutions do not solve your issue, retrieve the logs of the {{site.data.keyword.cos_short}} subscription for further debugging by using [{{site.data.keyword.logs_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration) for log management capabilities.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).
