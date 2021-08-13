---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-13"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Why can't I submit a job run with the CLI?  
{: #ts-jobrun-submit-fails-cli}
{: troubleshoot}

{: tsSymptoms}

You cannot submit a job run with the CLI. When you run the **`ibmcloud ce jobrun submit`** command, you receive the following error message: 

```
Submitting job run 'JOB_NAME'...
FAILED
Failed to create job run
```
{: screen}

{: tsCauses}

If you cannot submit a job run, determine whether one of the following cases is true.

1. The name of your job run is not unique within the project.  
2. If you reference a job and the job doesn't exist, the job run is not submitted and an error occurs.  
3. When you submit a job run with the **`jobrun submit`** command and you reference a job and you also specify an image on this command that is different from the image that is specified in the job, the job run is not submitted and an error occurs.
4. The job run resource size exceeds the maximum size, which is 10 KiB. 

{: tsResolve}

Try one of these solutions.

1. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all defined job runs and check whether a job run with the same name exists. If a job run with the same name exists, use the `ibmcloud ce jobrun delete --name JOBRUN_NAME` command to delete the old job run. The name of the job run must be unique within your project. You cannot submit a job run with the same job run name again. 
2. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all defined jobs and confirm that you are referencing a defined job. 
3. The image that is defined in your job cannot be overwritten by specifying a different image value when you submit a job run that refers to your job. If you want to use another image for your job run, create a new job that refers to the image that you want to use, or you can submit a job run that does not refer to the job. 
4. The maximum size for jobs and job runs is 10 KiB. When you create or update jobs and job runs with the console, CLI, or API, {{site.data.keyword.codeengineshort}} checks the size of the job or job run. If the operation exceeds the limit, you receive a size limit exceeded error. If you receive this error, try reducing the size of your job or your job run in one of the following ways:
  * If you are using commands and arguments, try reducing the use of these options, make them shorter, or move them into the container image that is used by your job or job run.
  * If you are using environment variables, try using fewer environment variables or make them shorter. You can use secrets or configmaps to define environment variables and import them into the job by using the ` --env-from-secret` or ` --env-from-configmap` options with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`ibmcloud ce job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), and [**`ibmcloud ce jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

For more information about job size limits, see [Job size limit](/docs/codeengine?topic=codeengine-limits#job_size_limit). For more information about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-run-job).

