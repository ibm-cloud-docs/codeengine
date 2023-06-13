---

copyright:
  years: 2020, 2023
lastupdated: "2023-06-13"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# I'm over my limit for jobs or job runs. How can I delete them?
{: #ts-jobrun-deleteforquota}
{: troubleshoot}


You receive a message that the limit for jobs or job runs is exceeded. 
{: tsSymptoms}

Check that the quota for your jobs and job runs is not exceeded. 
{: tsCauses}

{{site.data.keyword.codeengineshort}} has quotas for jobs and job runs within a project. You are limited to 100 jobs per project and 100 job runs per project before you need to clean up old ones. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Use one of the following ways to check that the quota limit for jobs and job runs is not exceeded.

* From the console, select your project and then go to the {{site.data.keyword.codeengineshort}} Overview page. You can view the number of jobs and job runs for the project in the Summary section. For more details, select Jobs or Job runs from the Summary section or select Jobs from the navigation menu.

* In the CLI, 
    * Run the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all your defined job runs. 
    * Run the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) command to list all your defined jobs. 

 
{: tsResolve}

If the number of jobs or job runs is near the quota limit, delete job runs and then jobs as needed. 

Use one of the following ways to delete job runs or jobs when the limit. 

When you  delete a job, all the submitted job runs that reference this job are also deleted.  
{: note}


* From the console, select your project and then go to the {{site.data.keyword.codeengineshort}} Overview page. You can view the number of jobs and job runs for the project in the Summary section. For more details, select Jobs or Job runs from the Summary section or select Jobs from the navigation menu. 
    * To delete a specific job run of a job, select the job from the **Jobs** page. From the specific job page, click the name of the job run from the **Latest job runs** section, and then select **Delete job run** in the drop-down menu. 
    * To delete a specific job and all of its job runs from the **Jobs** page, click the **Delete** icon ![Delete](../icons/delete.svg "Delete").


* In the CLI, 
    * Run the [**`ibmcloud ce jobrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-delete) command to delete the specified job run. 
    * Run the [**`ibmcloud ce job delete`**](/docs/codeengine?topic=codeengine-cli#cli-job-delete) command to delete your defined job and all the submitted job runs that reference this job. 



For more information, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan) and [Debugging jobs](/docs/codeengine?topic=codeengine-troubleshoot-job).






