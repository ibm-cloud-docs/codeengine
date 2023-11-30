---

copyright:
  years: 2020, 2023
lastupdated: "2023-11-30"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting batch jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, job, job run

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I find information about my job run?  
{: #ts-jobrun-learnmore}
{: troubleshoot}

You can display information about your job run instances to help you manage runs of your jobs from the console or with the CLI. 
{: tsSymptoms}

If you cannot find information about your job runs, determine whether one of the following cases is true. 
{: tsCauses}


1. [Access details of your job](/docs/codeengine?topic=codeengine-access-job-details) with the console or the CLI.  
    * From the console, go to the job details page for your job and click the **Job runs** tab for a list of all your job runs that have been submitted from your job configuration. 

    * From the CLI,  
        * To view details about all job runs for a particular job configuration, run the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command. For example, to get details about the `myjob` job including all job runs that are associated with this configuration,

            ```txt
            ibmcloud ce job get --name myjob
            ```
            {: pre}

            Example output

            ```txt
            Getting job 'myjob'...
            OK

            Name:          myjob
            ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
            Project Name:  myproject
            Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
            Age:           2m4s
            Created:       2021-02-17T15:41:12-05:00

            Last Job Run:
            Name:     myjob-jobrun-abcde
            Age:      32d
            Created:  2021-10-06T13:50:02-04:00

            Image:                icr.io/codeengine/firstjob
            Resource Allocation:
                CPU:     1
                Memory:  4G

            Runtime:
                Mode:                  task
                Array Indices:         0
                Array Size:            1
                Max Execution Time:    7200
                Retry Limit:           3
            ```
            {: screen}

        * To view details of a specific job run, use the **`jobrun get`** command. It can be helpful to first view a list of all job runs with the **`jobrun list`** command. For example, to view details of the `myjob-jobrun-abcde` job run,

            ```txt
            ibmcloud ce jobrun get --name myjob-jobrun-abcde
            ```
            {: pre}

            Example output

            ```txt
            Getting jobrun 'myjob-jobrun-abcde'...
            Getting instances of jobrun 'myjob-jobrun-abcde'...
            Getting events of jobrun 'myjob-jobrun-abcde'...
            For troubleshooting information visit: https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-job.
            Run 'ibmcloud ce jobrun events -n myjob-jobrun-abcde' to get the system events of the job run instances.
            Run 'ibmcloud ce jobrun logs -f -n myjob-jobrun-abcde' to follow the logs of the job run instances.
            OK

            Name:          myjob-jobrun-abcde 
            ID:            cd86393d-8150-46d5-b012-15f5225871b0  
            Project Name:  myproject  
            Project ID:    1b52c15b-7f4f-4d0c-b4fd-08cd2f2b8c29  
            Age:           4m52s  
            Created:       2022-08-29T14:26:53-04:00  

            Job Ref:              myjob  
            Image:                icr.io/codeengine/helloworld  
            Resource Allocation:    
            CPU:                1  
            Ephemeral Storage:  400M  
            Memory:             4G  

            Runtime:
                Mode:                  task
                Array Indices:         0-2 
                Array Size:            3
                JOP_ARRAY_SIZE Value:  3
                Max Execution Time:    7200
                Retry Limit:           3

            Status:       
            Completed:          4m45s  
            Instance Statuses:    
                Succeeded:  3  
            Conditions:         
                Type      Status  Last Probe  Last Transition  
                Pending   True    4m52s       4m52s  
                Running   True    4m49s       4m49s  
                Complete  True    4m45s       4m45s  

            Events:       
            Type    Reason     Age                    Source                Messages  
            Normal  Updated    4m46s (x6 over 4m53s)  batch-job-controller  Updated JobRun "myjob-jobrun-abcde"  
            Normal  Completed  4m46s                  batch-job-controller  JobRun completed successfully  

            Instances:    
            Name                    Running  Status     Restarts  Age  
            myjob-jobrun-abcde-0-0  0/1      Succeeded  0         4m53s  
            myjob-jobrun-abcde-1-0  0/1      Succeeded  0         4m53s  
            myjob-jobrun-abcde-2-0  0/1      Succeeded  0         4m53s  

            ```
            {: screen}

2. {{site.data.keyword.codeengineshort}} keeps job runs that you trigger in the system until you delete them. However, {{site.data.keyword.codeengineshort}}  automatically deletes job runs after some time, depending on system resources, to free up resources that are associated with instances of a job run.

3. If your job is triggered by an event subscription, such as Cron or {{site.data.keyword.cos_full_notm}}, then the associated job runs are deleted after after 10 minutes. See [Where is my job run?](/docs/codeengine?topic=codeengine-ts-jobrun-deleted).



Try one of these solutions.
{: tsResolve}

1. Debug runs of your job by getting [logs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-gettinglogs). 

    To view logs from the console, you must first add logging capabilities by creating an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-logs-ui).

    To view logs with the CLI, 
    * Use the [**`ibmcloud ce jobrun list`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list) command to list all your defined job runs.
    * To display logs of all the instances of your running job, use the [**`ibmcloud ce jobrun logs --jobrun JOBRUN_NAME --f`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. The `--f` option specifies to stream the logs of the job run instance. 
    * To display logs for a specific job run instance, use the [**`ibmcloud ce jobrun logs --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command.

2. Debug runs of your job by getting [system event data](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent). 

    To view system event information for your job runs with the CLI,  

    * To display system events for all the instances of your running job, use the [**`ibmcloud ce jobrun events --jobrun JOBRUN_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command.

    * To display system events for a specific instance of your job run, use the [**`ibmcloud ce jobrun events --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command.

These CLI commands can retrieve logs and system event information as long as the job run instances are in the system. If you want to access logs for job runs that have been completed hours or days ago, then use {{site.data.keyword.la_full_notm}} capabilities. {{site.data.keyword.la_short}} offers various plans to control the retention period for logs. If your job runs are no longer in the system, use an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. See [Getting started with {{site.data.keyword.la_full_notm}}](/docs/log-analysis?topic=log-analysis-getting-started).
{: important}


For more information about working with jobs and job runs, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).






