---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-13"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I submit a job run with the CLI?  
{: #ts-jobrun-submit-fails-cli}
{: troubleshoot}

You cannot submit a job run with the CLI.
{: tsSymptoms} 

When you run the **`ibmcloud ce jobrun submit`** command, you receive the following error message: 

```txt
Submitting job run 'JOB_NAME'...
FAILED
Failed to create job run
```
{: screen}

If you cannot submit a job run, determine whether one of the following cases is true.
{: tsCauses}

1. The name of your job run is not unique within the project.  
2. If you reference a job and the job doesn't exist, the job run is not submitted and an error occurs.  
3. When you submit a job run with the **`jobrun submit`** command and you reference a job and you also specify an image on this command that is different from the image that is specified in the job, the job run is not submitted and an error occurs.
4. The job run resource size exceeds the maximum size, which is 10 KiB. 

Try one of these solutions.
{: tsResolve}

1. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all defined job runs and check whether a job run with the same name exists. If a job run with the same name exists, use the `ibmcloud ce jobrun delete --name JOBRUN_NAME` command to delete the old job run. The name of the job run must be unique within your project. You cannot submit a job run with the same job run name again. 
2. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all defined jobs and confirm that you are referencing a defined job. 
3. The image that is defined in your job cannot be overwritten by specifying a different image value when you submit a job run that refers to your job. If you want to use another image for your job run, create a new job that refers to the image that you want to use, or you can submit a job run that does not refer to the job. 
4. The maximum size for jobs and job runs is 10 KiB. When you create or update jobs and job runs with the console, CLI, or API, {{site.data.keyword.codeengineshort}} checks the size of the job or job run. If the operation exceeds the limit, you receive a size limit exceeded error. If you receive this error, try reducing the size of your job or your job run in one of the following ways:
    * If you are using commands and arguments, reduce the use of these options, make them shorter, or move them into the container image that is used by your job or job run.
    * If you are using environment variables, use fewer environment variables or make them shorter. You can use secrets or configmaps to define environment variables and import them into the job by using the `--env-from-secret` or `--env-from-configmap` options with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`ibmcloud ce job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), and [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

For more information about job size limits, see [Job size limit](/docs/codeengine?topic=codeengine-limits#job_size_limit). For more information about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-run-job).



