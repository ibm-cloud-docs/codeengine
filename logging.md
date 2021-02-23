---

copyright:
  years: 2021
lastupdated: "2021-02-23"

keywords: logging for code engine, logs for code engine, job logs for code engine, app logs for code engine, build logs for code engine

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
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Viewing logs
{: #view-logs}

Logging can help you troubleshoot issues in {{site.data.keyword.codeengineshort}}. 
{: shortdesc}

## Viewing logs in {{site.data.keyword.la_full_notm}}
{: #view-logs-ui}

{{site.data.keyword.codeengineshort}} logs are forwarded to an {{site.data.keyword.loganalysislong_notm}} service where they are indexed, enabling full-text search through all generated messages and convenient querying based on specific fields.
{: shortdesc}

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: important}

To get started, complete the following steps.

1. Navigate to {{site.data.keyword.loganalysislong_notm}} with LogDNA service and create an instance in the same region as your {{site.data.keyword.codeengineshort}} project.

2. Configure the {{site.data.keyword.loganalysislong_notm}} with LogDNA instance to receive platform service logs, by using one of the following methods,

   * After the {{site.data.keyword.la_short}} instance is configured, from an Action menu, click **Add logging** to configure platform logs. When the dialog opens, select a {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your instance. Click **Configure**.

   * From the [Observability dashboard](https://cloud.ibm.com/observe/logging), [configure platform logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs#config_svc_logs_ui). Click **Configure platform logs**. Select the {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. Click **Configure**.

   * (Optional) To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

Now that you enabled logging, you can click **Launch logging** from the Action menu to open the {{site.data.keyword.la_short}} page.

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the {{site.data.keyword.la_short}} page, you can modify and scope the preset filter to display log data at a specific level or a more granular level of a specific app, job, or build run. For example, the filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:'Code Engine' app:myjob` scopes the log data to the job level. 

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

To view app logs for a specific app with the CLI, use the `application logs` command. You can display logs of all of the instances of an app or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

* To view the logs for all instances of the `myapp` app, specify the name of the app with the `--app` option; for example,  

   ```
   ibmcloud ce app logs --app myapp 
   ```
   {: pre}

   **Example output**

   ```
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
  
## Viewing build logs with the CLI
{: #view-build-cli}

To view build logs for a specific build with the CLI, use the `buildrun logs` command. You can display logs of all of the instances of a build or display logs of a specific instance of a build. The `build get` command displays details about your build, including the running instances of the build.

To view the logs for all instances of the `mybuildrun` build run, specify the name of the build run with the `--name` option; for example,  

```
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

**Example output**

```
Getting build run 'mybuildrun'...
Getting logs for build run 'mybuildrun'...
OK
mybuildrun:    
{"level":"info","ts":1605028483.8789494,"caller":"git/git.go:164","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 5202975e6d8907726c4215dcd332a420f7dc3fe8 (grafted, HEAD, origin/main) in path /workspace/source"}  
{"level":"info","ts":1605028484.738955,"caller":"git/git.go:205","msg":"Successfully initialized and updated submodules in path /workspace/source"}  
INFO[0004] Retrieving image manifest node:12-alpine       
INFO[0004] Retrieving image node:12-alpine                
INFO[0004] Retrieving image manifest node:12-alpine       
INFO[0004] Retrieving image node:12-alpine                
INFO[0005] Built cross stage deps: map[]                  
INFO[0005] Retrieving image manifest node:12-alpine       
INFO[0005] Retrieving image node:12-alpine                
INFO[0006] Retrieving image manifest node:12-alpine       
INFO[0006] Retrieving image node:12-alpine                
INFO[0007] Executing 0 build triggers                     
INFO[0007] Unpacking rootfs as cmd RUN npm install requires it.   
INFO[0010] RUN npm install                                
INFO[0010] Taking snapshot of full filesystem...          
INFO[0011] cmd: /bin/sh                                   
INFO[0011] args: [-c npm install]                         
INFO[0011] Running: [/bin/sh -c npm install]              
npm WARN saveError ENOENT: no such file or directory, open '/package.json'  
npm notice created a lockfile as package-lock.json. You should commit this file.  
npm WARN enoent ENOENT: no such file or directory, open '/package.json'  
npm WARN !invalid#2 No description  
npm WARN !invalid#2 No repository field.  
npm WARN !invalid#2 No README data  
npm WARN !invalid#2 No license field.  
up to date in 0.34s  
found 0 vulnerabilities  
INFO[0012] Taking snapshot of full filesystem...          
INFO[0012] COPY server.js .                               
INFO[0012] Taking snapshot of files...                    
INFO[0012] EXPOSE 8080                                    
INFO[0012] cmd: EXPOSE                                    
INFO[0012] Adding exposed port: 8080/tcp                  
INFO[0012] CMD [ "node", "server.js" ]
```
{: screen}
