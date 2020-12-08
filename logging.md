---
copyright:
  years: 2020
lastupdated: "2020-12-08"

keywords: serverless, codeengine, logging, code engine, logs

subcollection: codeengine

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
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Viewing logs
{: #view-logs}

Logging can help you troubleshoot issues in {{site.data.keyword.codeengineshort}}. 
{: shortdesc}

## Viewing job logs from the console
{: #view-joblogs-ui}

{{site.data.keyword.codeengineshort}} uses {{site.data.keyword.la_full}} for log management capabilities. You can access logs for jobs that are run in the console from your job details page. 

If you want to view logs for your job from the console, you must enable logging. 

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: important}

After you run a job, the system displays the status of the instances of your job on the job details page. If logging capabilities are not set, the **Add logging** option is displayed. Note that when logging capabilities are set, the job details page displays **Launch logging** instead of **Add logging**.

After you enable logging, you can keep the {{site.data.keyword.la_short}} window open to view your job log data. Keeping the {{site.data.keyword.la_short}} window open is useful when you use the Lite service plan as data is not retained with this plan. 
{: tip}

1. Click **Add logging** on the job details page to create a {{site.data.keyword.la_short}} log instance for your region.
2. From the {{site.data.keyword.la_short}} page, specify a region, review pricing information, select your plan, and review {{site.data.keyword.la_short}} resource information. Click **Create** to create the logging instance.

  Review the [service plan](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-service_plans) information as you consider retention, search, and log usage needs.
  {: tip}

3. Configure {{site.data.keyword.la_short}} platform logs by using one of the following ways: 

   * After the {{site.data.keyword.la_short}} instance is configured, from a job details page, click **Add logging** to configure platform logs. When the dialog opens, select a {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

   * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select the {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

   * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

4. Now that you enabled logging, you can click **Launch logging** from the job details page to open the {{site.data.keyword.la_short}} page for all jobs that are run.

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the {{site.data.keyword.la_short}} page, you can modify and scope the preset filter to display log data at the job level or a more granular level of a specific job run. For example, the filter `_platform:{{site.data.keyword.codeengineshort}} app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:Code Engine app:myjob` scopes the log data to the job level. 
{: tip}


## Viewing job logs with the CLI
{: #view-joblog-cli}

To view logs for a specific job run with the CLI, use the `jobrun logs` command. You can display logs of all of the instances of a job run or display logs of a specific instance of a job run. The `jobrun get` command displays details about your job run, including the running instances of the job run. 

* To view the logs for all instances of the `testjobrun` job run, specify the name of the job run with the `--jobrun` option; for example, 

  ```
  ibmcloud ce jobrun logs --jobrun testjobrun
  ```
  {: pre}

  **Example output**

  ```
  Getting jobrun 'testjobrun'...
  Getting instances of jobrun 'testjobrun'...
  Getting logs for all instances of job run 'testjobrun'...
  OK

  testjobrun-1-0:
  Hello World!

  testjobrun-2-0:
  Hello World!

  testjobrun-3-0:
  Hello World!

  testjobrun-4-0:
  Hello World!

  testjobrun-5-0:
  Hello World!
  ```
  {: screen}

* To view the logs for the `testjobrun-1-0` job run instance, specify the name of a specific instance of the job run with the `--instance` option; for example,

  ```
  ibmcloud ce jobrun logs --instance testjobrun-1-0 
  ```
  {: pre}

  **Example output**

  ```
  Getting logs for job run instance 'testjobrun-1-0'...
  OK

  testjobrun-1-0:
  Hello World!
  ```
  {: screen}

## Viewing application logs with the CLI
{: #view-applog-cli}

To view app logs for a specific app with the CLI, use the `application logs` command. You can display logs of all of the instances of an app or or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

* To view the logs for all instances of the `myapp` app, specify the name of the app with the `--app` option; for example,  

   ```
   ibmcloud ce app logs --app myapp 
   ```
   {: pre}

   **Example output**

   ```
   Getting application 'myapp'...
   Getting revisions for application 'myapp'...
   Getting instances for application 'myapp'...
   Getting logs for all instances of application 'myapp'...
   OK

   myapp-ii18y-2-deployment-7657c5f4f9-dgk5f:
   Server running at http://0.0.0.0:8080/
   ```
   {: screen}

* To view the logs for a specific instance of the app, specify the name of the specific instance of the app with the `--instance` option; for example, 

   ```
   ibmcloud ce app logs --instance myapp-ii18y-2-deployment-7657c5f4f9-dgk5f 
   ```
   {: pre}

   **Example output**
      
   ```
   Getting logs for application instance 'myapp-a5yp2-2-deployment-65766594d4-hj6c5'...
   OK

   myapp-a5yp2-2-deployment-65766594d4-hj6c5:
   Server running at http://0.0.0.0:8080/
   ```
   {: screen}


