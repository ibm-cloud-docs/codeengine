---

copyright:
  years: 2020, 2026
lastupdated: "2026-01-27"

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

If your job run is created by a subscription, then event-triggered job runs are deleted after ten minutes. Manually triggered job runs are deleted after one week.
{: tsCauses}

To see whether jobs have run, ensure that your job implementation writes log statements (for example, when a job starts and finishes). You can then look for those statements in {{site.data.keyword.cloud}} Logs. For more information about viewing logs, see [Viewing logs](/docs/codeengine?topic=codeengine-logging&interface=ui).
{: tsResolve}

If you need an instance of your job run that was created by a subscription, trigger another event from your subscription event producer.

For example, if you are using an {{site.data.keyword.cos_full_notm}} subscription, you can update your {{site.data.keyword.cos_short}} bucket, considering the watched event types for your subscription. If you are using a Periodic timer (cron) subscription, you can either wait for the next scheduled event, or modify the schedule of the Periodic timer (cron) to meet your needs.

For more information about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-job-plan).
