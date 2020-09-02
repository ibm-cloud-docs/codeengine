---

copyright:
  years: 2020
lastupdated: "2020-09-02"

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
{: #kn-troubleshoot-job}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} jobs.
{: shortdesc}

## Why can't I create a job with the CLI?
{: #ts-create-job-cli-fails}
{: troubleshoot}

{: tsSymptoms}
You cannot create a running instance of a job with the CLI. When running the `ibmcloud ce job run` (or its alias `ibmcloud ce job create` command), you receive the following error message:

```
Creating job 'JOB_NAME'...
FAILED
Failed to create job
```
{: screen}

{: tsCauses}
There are several reasons why you might not be able to create a running instance of a job. 

1. Your job name is not unique within the project.  
2. If you reference a job definition and the job definition doesn't exist, the job will not create a running instance and an error occurs.  
3. If you reference a job definition and you specify an image that is different from the image in the job definition, the job will not create a running instance and an error occurs.  

{: tsResolve}
Try one of these solutions.

1. Use the `ibmcloud ce job list` command to list all defined jobs and check if a job with the same name exists. If a job with the same name name exists, use the `ibmcloud ce job delete --name JOB_NAME` to delete the old job. The name of the job must be unique within your project. You cannot create or run the same job again.
2. Use the `ibmcloud ce jobdef list` command to list all defined job definitions and confirm that you are referencing a defined job definition. 
3. The image that is defined in your job definition cannot be updated by specifying a different image value when creating a running instance of a job that refers to your job definition. If you want to use another image, create a new job definition that refers to the image that you want to use, or you can create a job that does not refer to the job definition.

For more about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).

## Why is my running job not completing? (CLI) 
{: #ts-running-job-doesnotcomplete-cli}
{: troubleshoot}

{: tsSymptoms}
After creating a running instance of a job and when using the `ibmcloud ce job get` command in the CLI to display the details of the job, the job status result does not include the following output: 

```
Status:                True
Type:                  Complete
```
{: screen}

{: tsCauses}
There are several reasons why the job did not complete.   

1. The job requires more time to complete. 
2. The image that is used by your job does not exist. 
3. The environment variable parameters that are required by the job are not specified.
4. The commands or arguments that are passed to the job are not valid. 

{: tsResolve}
Try one of these solutions.

1. Check that the `--maxexecutiontime MAX_TIME` option is set properly and enough time is specified for the job to complete.
2. Check that the image that is used by your job exists and is referred to correctly. Use the `ibmcloud ce job get` command to display details of your job, which includes the name of the image.  Confirm that you are using an image that exists. 
3. Display the details of the job by using the `ibmcloud ce job get` command and review the results for the following:
  * Check to see if the environment variables that are set using the `--env KEY=VALUE`, `--env-from-secret SECRET_NAME`, and `--env-from-configmap CONFIGMAP_NAME` options are correct in the job details.
  * Use the `ibmcloud ce secret get --name SECRET_NAME` and `ibmcloud ce configmap get --name CONFIGMAP_NAME` commands to check that any environment variable that is stored in the secret and configmap does exist. 

4. Verify the commands and arguments are valid for the job by using the `ibmcloud ce job get` command. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, retrieve the logs of the job for further debugging by using the `[ickn]} job logs --name JOB_NAME` command. See [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-kn-job-deploy#view-joblog-cli) for more information.

## Why is my running job not completing? (console) 
{: #ts-running-job-doesnotcomplete-ui}
{: troubleshoot}

{: tsSymptoms}
After submitting a job, from the job details page in the console, there are instances of the job that seem to be stuck in `pending` or `running` status, or are in a `failed` status.

{: tsCauses}
There are several reasons why the job did not complete.   

1. The job requires more time to complete. 
2. The image that is used by your job does not exist. 
3. The environment variable parameters that are required by the job are not specified. 
4. The commands or arguments that are passed to the job are not valid.

{: tsResolve}
Try one of these solutions.

1. From the job definition page, click **Submit Job** to run a that that is based on the selected job definition and check that the **Job timeout** value is set properly and specifies enough time for the job to complete.
2. From the job definition page, check that the image that is specified for **Image reference** is correct and confirm that this image exists in the container registry.  
3.  View details of the job in the console by clicking the name of your job in the Jobs pane on your job definition page. From this page, you can review any environment variables that are set and check that the environment variables are correct. 

4. Verify the commands and arguments are valid for the job. View details of the job in the console by clicking the name of your job on the Jobs pane on your job definition page.  The job details page lists any commands or arguments that are defined for the job. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, retrieve the logs of the job for further debugging by using {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run on the console from your job details page. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-kn-job-deploy#view-joblogs-ui) for more information.


