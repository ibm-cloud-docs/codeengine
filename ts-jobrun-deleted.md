---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-14"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Where is my job run?  
{: #ts-jobrun-deleted}
{: troubleshoot}

When I display my job runs, some of my job runs are deleted after a period of time.
{: tsSymptoms}

If your job run is created by a subscription, then your job run is deleted after 10 minutes. 
{: tsCauses}

If you need an instance of your job run that was created by a subscription, trigger another event from your subscription event producer.
{: tsResolve}

For example, if you are using an {{site.data.keyword.cos_full_notm}} subscription, you can update your {{site.data.keyword.cos_short}} bucket, considering the watched event types for your subscription. If you are using a Periodic timer (cron) subscription, you can either wait for the next scheduled event, or modify the schedule of the Periodic timer (cron) to meet your needs.

For more information about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-job-plan).



