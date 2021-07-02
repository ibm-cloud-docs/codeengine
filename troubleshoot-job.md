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


# Debugging jobs
{: #troubleshoot-job}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} jobs and runs of your job.
{: shortdesc}

## Job limits to consider 
{: #ts-job-limits}

The maximum number of jobs that you can have per project is 100. You are limited to a total of 100 job runs per project before you need to remove or clean up old ones. 

For more information about limits for jobs including memory and cpu, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Getting logs for my jobs 
{: #ts-jobrun-gettinglogs}

Logs can be helpful to troubleshoot problems when you run jobs. You can view job logs from the console or with the CLI. 
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} job. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your jobs. You can view job logs after you add logging capabilities. For more information, see [viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui).

When working with the CLI, you can display logs of all of the instances of your running job or display logs of a specific instance of your job. 

1. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all of your defined job runs; for example,
 
     ```
    ibmcloud ce jobrun list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command to get the details of your job run, including the name of the instances for the job run; for example,
 
  ```
  ibmcloud ce jobrun get --name myjobrun 
  ```
  {: pre}

  **Example output** 

  ```
  Getting jobrun 'myjobrun'...
  Getting instances of jobrun 'myjobrun'...
  Getting events of jobrun 'myjobrun'...
  OK

  Name:          myjobrun
  [...]
  Created:       2021-03-03T14:47:04-05:00

  Image:                ibmcom/firstjob
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

  Runtime:
    Array Indices:       1-4
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          28m
    Instance Statuses:
      Succeeded:  4
    Conditions:
      Type      Status  Last Probe  Last Transition
      Pending   True    28m         28m
      Running   True    28m         28m
      Complete  True    28m         28m

  Events:
    Type    Reason     Age                Source                Messages
    Normal  Updated    29m (x8 over 29m)  batch-job-controller  Updated JobRun "myjobrun"
    Normal  Completed  29m                batch-job-controller  JobRun completed successfully

  Instances:
    Name          Running  Status     Restarts  Age
    myjobrun-1-0  0/1      Succeeded  0         29m
    myjobrun-2-0  0/1      Succeeded  0         29m
    myjobrun-3-0  0/1      Succeeded  0         29m
    myjobrun-4-0  0/1      Succeeded  0         29m
  ```
  {: screen}

3. Display the logs of instances of your job run. 

  * To display the logs of a specific instance of your job run, use the [**`ibmcloud ce jobrun logs --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command; for example,
  
    ```
    ibmcloud ce jobrun logs --instance  myjobrun-4-0
    ```
    {: pre} 
      
    **Example output** 

    ```
    Getting logs for job run instance 'myjobrun-4-0'...
    OK

    myjobrun-4-0/myjobrun:
    Hi from a batch job! My index is: 4
    ```
    {: screen}

  * To display the logs of all of the instances of your job run, use the [**`ibmcloud ce jobrun logs --jobrun JOBRUN_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command; for example,
  
    ```
    ibmcloud ce jobrun logs --jobrun myjobrun 
    ```
    {: pre} 
    
    **Example output** 

    ```
    Getting logs for all instances of job run 'myjobrun'...
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    OK

    myjobrun-1-0/myjobrun:
    Hi from a batch job! My index is: 1

    myjobrun-2-0/myjobrun:
    Hi from a batch job! My index is: 2

    myjobrun-3-0/myjobrun:
    Hi from a batch job! My index is: 3

    myjobrun-4-0/myjobrun:
    Hi from a batch job! My index is: 4
    ```
    {: screen}

For more information, see [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-joblog-cli).

## Getting system event information for my jobs 
{: #ts-job-gettingevent}

System event information can be helpful to troubleshoot problems when you run jobs. You can view system event information with the CLI.
{: shortdesc}

You can display system events of all of the instances of a job run or display system events of a specific instance of a job run. 

1. Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all of your defined job runs; for example,
 
     ```
    ibmcloud ce jobrun list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command to get the details of your job run, including the name of the instances of the job run; for example,
 
  ```
  ibmcloud ce jobrun get --name myjobrun 
  ```
  {: pre}

  **Example output** 

  ```
  Getting jobrun 'myjobrun'...
  Getting instances of jobrun 'myjobrun'...
  Getting events of jobrun 'myjobrun'...
  OK

  Name:          myjobrun
  [...]
  Created:       2021-03-03T14:47:04-05:00

  Image:                ibmcom/firstjob
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

  Runtime:
    Array Indices:       1-4
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          28m
    Instance Statuses:
      Succeeded:  4
    Conditions:
      Type      Status  Last Probe  Last Transition
      Pending   True    28m         28m
      Running   True    28m         28m
      Complete  True    28m         28m

  Events:
    Type    Reason     Age                Source                Messages
    Normal  Updated    29m (x8 over 29m)  batch-job-controller  Updated JobRun "myjobrun"
    Normal  Completed  29m                batch-job-controller  JobRun completed successfully

  Instances:
    Name          Running  Status     Restarts  Age
    myjobrun-1-0  0/1      Succeeded  0         29m
    myjobrun-2-0  0/1      Succeeded  0         29m
    myjobrun-3-0  0/1      Succeeded  0         29m
    myjobrun-4-0  0/1      Succeeded  0         29m
  ```
  {: screen}

3. Display the system events of instances of your job run.  

  * To display the events of a specific instance of your job run, use the [**`ibmcloud ce jobrun events --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command; for example,
  
    ```
    ibmcloud ce jobrun events --instance myjobrun-4-0 
    ```
    {: pre} 
      
    **Example output** 

    ```
    Getting events for job run instance 'myjobrun-4-0'...
    OK

    myjobrun-4-0:
      Type    Reason     Age    Source                 Messages
      Normal  Scheduled  2m14s  default-scheduler      Successfully assigned 4svg40kna19/myjobrun-4-0 to 10.240.64.10
      Normal  Pulling    2m13s  kubelet, 10.240.64.10  Pulling image "ibmcom/firstjob"
      Normal  Pulled     2m12s  kubelet, 10.240.64.10  Successfully pulled image "ibmcom/firstjob" in 1.234456436s
      Normal  Created    2m11s  kubelet, 10.240.64.10  Created container myjobrun
      Normal  Started    2m11s  kubelet, 10.240.64.10  Started container myjobrun
    ```
    {: screen}

  * To display events of all of the instances of your job run, use the [**`ibmcloud ce jobrun events --jobrun JUBRUN_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command; for example,
  
    ```
    ibmcloud ce jobrun events --jobrun myjobrun 
    ```
    {: pre} 
    
    **Example output** 

    ```
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    Getting events for all instances of job run 'myjobrun'...
    OK

    myjobrun-1-0:
      Type    Reason     Age  Source                  Messages
      Normal  Scheduled  66s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-1-0 to 10.240.128.22
      Normal  Pulling    65s  kubelet, 10.240.128.22  Pulling image "ibmcom/firstjob"
      Normal  Pulled     64s  kubelet, 10.240.128.22  Successfully pulled image "ibmcom/firstjob" in 427.276949ms
      Normal  Created    64s  kubelet, 10.240.128.22  Created container myjobrun
      Normal  Started    64s  kubelet, 10.240.128.22  Started container myjobrun

    myjobrun-2-0:
      Type    Reason     Age  Source                Messages
      Normal  Scheduled  66s  default-scheduler     Successfully assigned 4svg40kna19/myjobrun-2-0 to 10.240.0.11
      Normal  Pulling    65s  kubelet, 10.240.0.11  Pulling image "ibmcom/firstjob"
      Normal  Pulled     63s  kubelet, 10.240.0.11  Successfully pulled image "ibmcom/firstjob" in 1.268252989s
      Normal  Created    63s  kubelet, 10.240.0.11  Created container myjobrun
      Normal  Started    63s  kubelet, 10.240.0.11  Started container myjobrun

    myjobrun-3-0:
      Type    Reason     Age  Source                Messages
      Normal  Scheduled  66s  default-scheduler     Successfully assigned 4svg40kna19/myjobrun-3-0 to 10.240.0.37
      Normal  Pulling    65s  kubelet, 10.240.0.37  Pulling image "ibmcom/firstjob"
      Normal  Pulled     63s  kubelet, 10.240.0.37  Successfully pulled image "ibmcom/firstjob" in 1.118647987s
      Normal  Created    63s  kubelet, 10.240.0.37  Created container myjobrun
      Normal  Started    63s  kubelet, 10.240.0.37  Started container myjobrun

    myjobrun-4-0:
      Type    Reason     Age  Source                 Messages
      Normal  Scheduled  66s  default-scheduler      Successfully assigned 4svg40kna19/myjobrun-4-0 to 10.240.64.10
      Normal  Pulling    65s  kubelet, 10.240.64.10  Pulling image "ibmcom/firstjob"
      Normal  Pulled     64s  kubelet, 10.240.64.10  Successfully pulled image "ibmcom/firstjob" in 1.234456436s
      Normal  Created    63s  kubelet, 10.240.64.10  Created container myjobrun
      Normal  Started    63s  kubelet, 10.240.64.10  Started container myjobrun
    ```
    {: screen}

