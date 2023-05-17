---

copyright:
  years: 2020, 2023
lastupdated: "2023-05-17"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my job run not starting?
{: #ts-jobrun-notstart}
{: troubleshoot}


A trigger to start a job run fails to start the job run.
{: tsSymptoms}


If your job run did not start, check that the quota for your jobs and job runs is not exceeded. 
{: tsCauses}



{{site.data.keyword.codeengineshort}} has quotas for jobs and job runs within a project.
{: tsResolve}

Check that you have not exceeded the quota limit for jobs and job runs for your project. You are limited to 100 jobs per project and 100 job runs per project before you need to clean up old ones. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Use one of the following ways to check that you haven't exceeded the quota limit for jobs and job runs.

* In the CLI, run the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all your defined job runs. Run the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) command to list all your defined jobs. 

* From the console, select your project and then go to the {{site.data.keyword.codeengineshort}} Overview page. You can view the number of jobs and job runs for the project in the Summary section. For more details, select Jobs or Job runs from the Summary section or select Jobs from the navigation menu.

If the number of jobs or job runs is near the quota limit, delete job runs and then jobs as needed. 

For more information, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan) and [Debugging jobs](/docs/codeengine?topic=codeengine-troubleshoot-job).



