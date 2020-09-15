---

copyright:
  years: 2020
lastupdated: "2020-09-15"

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


# Troubleshooting tips 
{: #kn-troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}}.
{: shortdesc}

## Why can't I access a project?
{: #ts-access-project}
{: troubleshoot}

{: tsSymptoms}
You cannot access a project that was created by someone else.

{: tsCauses}
Whenever you use an IBM Cloud account to create or use a project that is not owned by you, you must be assigned proper system roles. 

{: tsResolve}
To perform operations with a project that is not owned by you, you must have `Viewer` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-codeengine-iam).

## Why can't I create a project?
{: #ts-create-project}
{: troubleshoot}

{: tsSymptoms}
You cannot create a project in your resource group.

{: tsCauses}
There are several reasons why you might not be able to create a project in your resource group.

1. Your project name must be unique in the region. 
2. You might already have a project in the region. During the Beta release, you are limited to creating a single project in a region.
3. You might not have the proper platform access to create a project. 

{: tsResolve}
Try one of these solutions.

1. If you receive a warning message about your project name not being unique, select a different name. 
2. You can create only one project per region. For more information, see [Beta release limitations](/docs/codeengine?topic=codeengine-limits#beta-limits).
3. In order to create a project, you must have `Administrator` set for `Platform Access` and `Reader` for `Service Access`. For more information, see [Managing user access](/docs/codeengine?topic=codeengine-codeengine-iam).

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).

## Why can't I submit a jobrun with the CLI?
{: #ts-create-job-cli-fails}
{: troubleshoot}

{: tsSymptoms}
After you create a job configuration, you cannot submit (or run) a job based on that configuration with the CLI. When you run the `ibmcloud ce jobrun submit` command, you receive the following error message:

```
Creating job run 'JOBRUN_NAME'...
FAILED
Failed to create job run
```
{: screen}

{: tsCauses}
There are several reasons why you might not be able to submit a jobrun.  

1. Your jobrun name is not unique within the project.  
2. If you reference a job configuration and the job doesn't exist, the jobrun does not create a running instance and an error occurs.  
3. If you reference a job configuration and you specify an image that is different from the image in the job configuration, the jobrun does not create a running instance and an error occurs. 

{: tsResolve}
Try one of these solutions.

1. Use the `ibmcloud ce jobrun list` command to list all of the defined jobruns and check whether a jobrun with the same name exists. If a jobrun with the same name exists, use the `ibmcloud ce jobrun delete --name JOB_NAME` to delete the old jobrun. The name of the jobrun must be unique within your project. You cannot submit another jobrun with the same name until you have deleted the first one.  
2. Use the `ibmcloud ce job list` command to list all defined job configurations and confirm that you are referencing a defined job.
3. The image that is defined in the configuration of your job cannot be updated by specifying a different image value when you submit a jobrun that refers to your job configuration. If you want to use another image, update your job configuration to refer to the image that you want to use, or you can submit a jobrun that refers to the image that you want to use and does not refer to the job configuration. 

For more about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).

## Why is my submitted jobrun not completing? (CLI) 
{: #ts-running-job-doesnotcomplete-cli}
{: troubleshoot}

{: tsSymptoms}
After you create a job configuration and submitting your jobrun, when you run the `ibmcloud ce jobrun get` command in the CLI to display the details of the jobrun, the jobrrun status result does not include the following output: 

```
Status:                True
Type:                  Complete
```
{: screen}

{: tsCauses}
There are several reasons why the jobrun did not complete.   

1. The jobrun requires more time to complete. 
2. The image that is used by your jobrun does not exist. 
3. The environment variable parameters that are required by the jobrun are not specified.
4. The commands or arguments that are passed to the jobrun are not valid. 

{: tsResolve}
Try one of these solutions.

1. Check that the `--maxexecutiontime MAX_TIME` option for the jobrun is set properly and enough time is specified for the jobrun to complete.
2. Check that the image that is used by your jobrun exists and is referred to correctly. Use the `ibmcloud ce jobrun get` command to display details of your jobrun, which includes the name of the image.  Confirm that you are using an image that exists. 
3. Display the details of the jobrun by using the `ibmcloud ce jobrun get` command and review the results for the following items:
  * Check to see whether the environment variables that are set by using the `--env KEY=VALUE`, `--env-from-secret SECRET_NAME`, and `--env-from-configmap CONFIGMAP_NAME` options are correct in the jobrun details.
  * Use the `ibmcloud ce secret get --name SECRET_NAME` and `ibmcloud ce configmap get --name CONFIGMAP_NAME` commands to confirm that any environment variable that is stored in the secret and configmap does exist. 

4. Verify that the commands and arguments are valid for the jobrun by using the `ibmcloud ce jobrun get` command. The sequence in the commands and arguments is important. 

If these solutions do not solve your issue, retrieve the logs of the job for further debugging by using the `[ickn]} jobrun logs --instance JOBRUN_INSTANCE` command. For more information, see [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-kn-job-deploy#view-joblog-cli).

## Why is my running job not completing? (console) 
{: #ts-running-job-doesnotcomplete-ui}
{: troubleshoot}

{: tsSymptoms}
After you submit a job, from the job details page in the console, instances of the job seem to be stuck in `pending` or `running` status, or are in a `failed` status.

{: tsCauses}
There are several reasons why the job did not complete.   

1. The job requires more time to complete. 
2. The image that is used by your job does not exist. 
3. The environment variable parameters that are required by the job are not specified. 
4. The commands or arguments that are passed to the job are not valid.

{: tsResolve}
Try one of these solutions.

1. From your job page, click **Submit Job** to submit your job that is based on the selected your configuration values.  Check that the **Job timeout** value is set properly and specifies enough time for the job to complete.
2. From your job page, check that the image that is specified for **Image reference** is correct and confirm that this image exists in the container registry.  
3. View details of the job in the console by clicking the name of your job in the Jobs pane. From the details page, you can review any environment variables that are set and check that the environment variables are correct. 
4. Verify that the commands and arguments are valid for the job. View details of the job in the console by clicking the name of your job on the Jobs pane. The details page for your job lists any commands or arguments that are defined for the job. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, retrieve the logs of the job for further debugging by using {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run on the console from your job details page. For more information, see [Viewing job logs from the console](/docs/codeengine?topic=codeengine-kn-job-deploy#view-joblogs-ui).

