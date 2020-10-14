---

copyright:
  years: 2020
lastupdated: "2020-10-14"

keywords: code engine, troubleshooting for code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Troubleshooting tips for jobs
{: #troubleshoot-job}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} jobs.
{: shortdesc}

## Why can't I submit a job run with the CLI?  
{: #ts-jobrun-submit-fails-cli}
{: troubleshoot}

{: tsSymptoms}
You cannot submit a job run with the CLI. When you run the `ibmcloud ce jobrun submit` command, you receive the following error message: 

```
Submitting job run 'JOB_NAME'...
FAILED
Failed to create job run
```
{: screen}

{: tsCauses}
There are several reasons why you might not be able to submit a job run.  

1. The name of your job run is not unique within the project.  
2. If you reference a job and the job doesn't exist, the job run is not submitted and an error occurs.  
3. When you submit a job run with the `jobrun submit` command and you reference a job and you also specify an image on this command that is different from the image that is specified in the job, the job run is not submitted and an error occurs.  

{: tsResolve}
Try one of these solutions.

1. Use the `ibmcloud ce jobrun list` command to list all defined job runs and check whether a job run with the same name exists. If a job run with the same name exists, use the `ibmcloud ce jobrun delete --name JOBRUN_NAME` to delete the old job run. The name of the job run must be unique within your project. You cannot submit a job run with the same job run name again. 
2. Use the `ibmcloud ce job list` command to list all defined jobs and confirm that you are referencing a defined job. 
3. The image that is defined in your job cannot be overwritten by specifying a different image value when submitting a job run that refers to your job. If you want to use another image for your job run, create a new job that refers to the image that you want to use, or you can submit a job run that does not refer to the job. 

For more about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-job-deploy).

## Why is my job run not completing? (CLI) 
{: #ts-jobrun-doesnotcomplete-cli}
{: troubleshoot}

{: tsSymptoms}
After you submit a job run, when you run the `ibmcloud ce jobrun get` command in the CLI to display the details of the job run, the job run status result does not include the following output: 

```
Status:                True
Type:                  Complete
```
{: screen}

{: tsCauses}
There are several reasons why the job run did not complete.   

1. The job run requires more time to complete. 
2. The image that is used by your job run does not exist. 
3. The environment variable parameters that are required by the job run are not specified.
4. The commands or arguments that are passed to the job run are not valid. 

{: tsResolve}
Try one of these solutions.

1. Check that the `--maxexecutiontime MAX_TIME` option is set properly and enough time is specified for the job run to complete.
2. Check that the image that is used by your job run exists and is referred to correctly. Use the `ibmcloud ce jobrun get` command to display details of your job run, which includes the name of the image.  Confirm that you are using an image that exists. 
3. Display the details of the job run by using the `ibmcloud ce jobrun get` command and review the results for the following items:
  * Check to see whether any environment variables that are set by using the `--env KEY=VALUE`, `--env-from-secret SECRET_NAME`, and `--env-from-configmap CONFIGMAP_NAME` options are correct in the job run details.
  * Use the `ibmcloud ce secret get --name SECRET_NAME` and `ibmcloud ce configmap get --name CONFIGMAP_NAME` commands to check that any environment variable that is stored in the secret and configmap does exist. 

4. Verify that the commands and arguments are valid for the job run by using the `ibmcloud ce jobrun get` command. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, retrieve the logs of the job run for further debugging by using the `ibmcloud ce jobrun logs --instance JOBRUN_INSTANCE` command. For more information, see [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-job-deploy#view-joblog-cli).

## Why is my running job not completing? (console) 
{: #ts-jobrun-doesnotcomplete-ui}
{: troubleshoot}

{: tsSymptoms}
After you submit a job, from the job details page in the console, instances of the job seem to be stuck in `pending` or `running` status, or are in a `failed` status.

{: tsCauses}
There are several reasons why the job did not complete.   

1. The submit of your job requires more time to complete. 
2. The image that is used by your job does not exist. 
3. The environment variable parameters that are required by the job are not specified. 
4. The commands or arguments that are passed to the job are not valid.

{: tsResolve}
Try one of these solutions.

1. From your job page, click **Submit Job** to run a job that is based on the selected job and its defined properties. Check that the **Job timeout** value is set properly and specifies enough time for the job run to complete.
2. From your job page, check that the image that is specified for **Image reference** is correct and confirm that this image exists in the container registry.  
3. View details of your submitted job in the console by clicking the name of your job run in the Jobs pane on your job page. From the submitted job details page, you can review any environment variables that are set and check that the environment variables are correct. 
4. Verify that the commands and arguments are valid for the job. View details of the submitted job in the console by clicking the name of your job run in the Jobs pane on your job page. The submitted job details page lists any commands or arguments that are defined for the submitted job. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, retrieve the logs of the job for further debugging by using {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run on the console from your job details page. For more information, see [Viewing job logs from the console](/docs/codeengine?topic=codeengine-job-deploy#view-joblogs-ui).

