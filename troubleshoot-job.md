---

copyright:
  years: 2021
lastupdated: "2021-03-03"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine

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
If you cannot submit a job run, determine whether one of the following cases is true.

1. The name of your job run is not unique within the project.  
2. If you reference a job and the job doesn't exist, the job run is not submitted and an error occurs.  
3. When you submit a job run with the `jobrun submit` command and you reference a job and you also specify an image on this command that is different from the image that is specified in the job, the job run is not submitted and an error occurs.  

{: tsResolve}
Try one of these solutions.

1. Use the `ibmcloud ce jobrun list` command to list all defined job runs and check whether a job run with the same name exists. If a job run with the same name exists, use the `ibmcloud ce jobrun delete --name JOBRUN_NAME` command to delete the old job run. The name of the job run must be unique within your project. You cannot submit a job run with the same job run name again. 
2. Use the `ibmcloud ce job list` command to list all defined jobs and confirm that you are referencing a defined job. 
3. The image that is defined in your job cannot be overwritten by specifying a different image value when you submit a job run that refers to your job. If you want to use another image for your job run, create a new job that refers to the image that you want to use, or you can submit a job run that does not refer to the job. 

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
If your job did not complete, determine whether one of the following cases is true.  

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

If these solutions do not solve your issue, for further debugging, try retrieving the logs or the system event information for your job run. For more information, see [How do I get logs for my job run instances? (CLI)](#ts-jobrun-gettinglogs-cli) and [How do I get system event information for my job run instances? (CLI)](#ts-jobrun-gettingevent-cli).

## Why is my running job not completing? (console) 
{: #ts-jobrun-doesnotcomplete-ui}
{: troubleshoot}

{: tsSymptoms}
After you submit a job, from the job details page in the console, instances of the job seem to be stuck in `pending` or `running` status, or are in a `failed` status.

{: tsCauses}
If your job did not complete, determine whether one of the following cases is true. 

1. Your job run submit requires more time to complete. 
2. The image that is used by your job does not exist. 
3. The environment variable parameters that are required by the job are not specified. 
4. The commands or arguments that are passed to the job are not valid.

{: tsResolve}
Try one of these solutions.

1. From your job page, click **Submit Job** to run a job that is based on the selected job and its defined properties. Check that the **Job timeout** value is set properly and specifies enough time for the job run to complete.
2. From your job page, check that the image that is specified for **Image reference** is correct and confirm that this image exists in the container registry.  
3. View details of your submitted job in the console by clicking the name of your job run in the Jobs pane on your job page. From the submitted job details page, you can review any environment variables that are set and check that the environment variables are correct. 
4. Verify that the commands and arguments are valid for the job. View details of the submitted job in the console by clicking the name of your job run in the Jobs pane on your job page. The submitted job details page lists any commands or arguments that are defined for the submitted job. The sequence in the commands and arguments is important.  

If these solutions do not solve your issue, for further debugging, try retrieving the logs or the system event information for your job run. For more information, see [How do I get logs for my job run instances? (CLI)](#ts-jobrun-gettinglogs-cli) and [How do I get system event information for my job run instances? (CLI)](#ts-jobrun-gettingevent-cli).

## How do I get logs for my job run instances? (CLI) 
{: #ts-jobrun-gettinglogs-cli}

Your job isn't behaving as expected and you want to look at the logs to see whether any messages are generated to help you debug the problem. Logs can be helpful to troubleshoot problems when you run your jobs.  

You can display logs of all of the instances of your running job or display logs of a specific instance of your job. The `jobrun get` command displays details about your job run, including the running instances of the job run.

1. Use the [`ibmcloud ce jobrun list `](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all of your defined job runs; for example,
 
     ```
    ibmcloud ce jobrun list  
    ```
    {: pre}

2. Use the [`ibmcloud ce jobrun get`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command to get the details of your job run, including the name of the instances for the job run; for example,
 
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
    Memory:             128Mi

  Runtime:
    Array Indices:       1-5
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          28m
    Instance Statuses:
      Succeeded:  5
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

3. Display the logs of your job run. 

  * To display the logs of a specific instance of your job run, use the [`ibmcloud ce jobrun logs --instance INSTANCE_NAME`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command; for example,
  
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

  * To display the logs of all of the instances of your app, use the [`ibmcloud ce jobrun logs --application JOBRUN_NAME`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command; for example,
  
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

    myjobrun-2-0/myjobrun:
    Hi from a batch job! My index is: 1

    myjobrun-3-0/myjobrun:
    Hi from a batch job! My index is: 2

    myjobrun-4-0/myjobrun:
    Hi from a batch job! My index is: 3

    myjobrun-5-0/myjobrun:
    Hi from a batch job! My index is: 4
    ```
    {: screen}

For more information, see [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-joblog-cli).

## How do I get system event information for my job run instances? (CLI) 
{: #ts-jobrun-gettingevent-cli}

Your job isn't behaving as expected and you want to look at the system event information to see whether any messages are generated to help you debug the problem. System event information can be helpful to troubleshoot problems when you run jobs.

You can display system events of all of the instances of a job run or display system events of a specific instance of a job run.  The `jobrun get` command displays details about your job run, including the running instances of the job run. 

1. Use the [`ibmcloud ce jobrun list `](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all of your defined job runs; for example,
 
     ```
    ibmcloud ce jobrun list  
    ```
    {: pre}

2. Use the [`ibmcloud ce jobrun get`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command to get the details of your job run, including the name of the instances of the job run; for example,
 
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
    Memory:             128Mi

  Runtime:
    Array Indices:       1-5
    Max Execution Time:  7200
    Retry Limit:         3

  Status:
    Completed:          28m
    Instance Statuses:
      Succeeded:  5
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

  * To display the events of a specific instance of your job run, use the [`ibmcloud ce jobrun events --instance INSTANCE_NAME`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command; for example,
  
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

  * To display events of all of the instances of your app, use the [`ibmcloud ce app events --application APP_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,
  
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
