---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-02"

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
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


# Why is my job not completing? 
{: #ts-jobrun-doesnotcomplete}
{: troubleshoot}

{: tsSymptoms}

When using the console, you submit a job and the job does not complete. 

When using the CLI, after you submit a job run, the job run does not complete. You can confirm this result by running the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command to display the details of the job run, and the job run status result does not include the following output: 

```
Status:                True
Type:                  Complete
```
{: screen}

{: tsCauses}
If your job did not complete, determine whether one of the following cases is true.  

1. The job run requires more time to complete. 
2. The image that is used by your job run does not exist. 
3. The environment variable parameters that are required by the job run are not specified.
4. The commands or arguments that are passed to the job run are not valid. 

{: tsResolve}
Try one of these solutions.

1. Check that enough time is specified for the job to run.
    * From the console, from your job page, click **Submit Job** to run a job that is based on the selected job and its defined properties. Check that the **Job timeout** value is set properly and specifies enough time for the job run to complete.

    * With the CLI, check that the `--maxexecutiontime MAX_TIME` option is set properly and enough time is specified for the job run to complete.

2. Check that the image that is used by your job run exists and is referred to correctly. 

    * From the console, from your job page, check that the image that is specified for **Image reference** is correct and confirm that this image exists in the container registry. 

    * With the CLI, use the **`ibmcloud ce jobrun get`** command to display details of your job run, which includes the name of the image. Confirm that you are using an image that exists.

3. View details of the submitted job.

    * From the console, view details of your submitted job by clicking the name of your job run in the Jobs pane on your job page. From the submitted job details page, you can review any environment variables that are set and check that the environment variables are correct. 

    * With the CLI, use the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command and review the results for the following items:
        * Check to see whether any environment variables that are set by using the `--env KEY=VALUE`, `--env-from-secret SECRET_NAME`, and `--env-from-configmap CONFIGMAP_NAME` options are correct in the job run details.
        * Use the `ibmcloud ce secret get --name SECRET_NAME` and `ibmcloud ce configmap get --name CONFIGMAP_NAME` commands to check that any environment variable that is stored in the secret and configmap does exist. 

4. Verify that the commands and arguments are valid for the job.

    * From the console, view details of the submitted job in the console by clicking the name of your job run in the Jobs pane on your job page. The submitted job details page lists any commands or arguments that are defined for the submitted job. The sequence in the commands and arguments is important.  
    
    * With the CLI, use the view details of the submitted job by using the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, for further debugging, try retrieving the logs or the system event information for your job run. For more information, see [How do I get logs for my job run instances?](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-gettinglogs) and [How do I get system event information for my job run instances? (CLI)](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent).

For more about running jobs, see [Running jobs](/docs/codeengine?topic=codeengine-job-deploy).

