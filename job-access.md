---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-09"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Accessing job details
{: #access-job-details}

Find details about your job from the console or with the CLI.
{: shortdesc}

## Accessing job details from the console
{: #access-jobdetails-ui}

After you submit your job, the results of the specific job run are available in the console from the Job run details page. From the console, you can also view details of your job and specific job runs from the Jobs page. 
* To view job details, click the **Jobs** tab, and click the name of the job you want to work with. 
* To view details for a specific job run, click the **Job runs** tab, and click the name of the job run that you want to work with. 


## Accessing job details with the CLI
{: #access-jobdetails-cli}

To view details of your job with the CLI, use the **`job get`** command. For a complete listing of options, see the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command. 
{: shortdesc}

For example, the following **`job get`** command displays details about the `myjob` job.

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


## Accessing job details for a specific run of your job with the CLI
{: #access-specific-jobdetails-cli}

To view details of a specific run of your job with the CLI, use the **`jobrun get`** command. For a complete listing of options, see the [**`ibmcloud ce jobrun get`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get) command. 
{: shortdesc}

For example, the following **`jobrun get`** command displays details about the `testjobrun` job run.

```txt
ibmcloud ce jobrun get --name testjobrun
```
{: pre}

Example output

```txt
Getting jobrun 'testjobrun'...
Getting instances of jobrun 'testjobrun'...
Getting events of jobrun 'testjobrun'...
[...]
Name:          testjobrun
ID:            abcdefgh-abcd-abcd-abcd-1d733051eb02
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m44s
Created:       2021-02-09T13:32:25-05:00

Job Ref:              myjob
Image:                icr.io/codeengine/firstjob
Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

Runtime:
    Mode:                  task
    Array Indices:         1 - 5
    Array Size:            5
    JOP_ARRAY_SIZE Value:  5
    Max Execution Time:    7200
    Retry Limit:           3

Status:
    Completed:          4m
    Instance Statuses:
        Succeeded:  5
    Conditions:
        Type      Status  Last Probe  Last Transition
    Pending   True    4m6s        4m6s
    Running   True    4m3s        4m3s
    Complete  True    4m          4m

Events:
    Type    Reason     Age                  Source                Messages
    Normal  Updated    4m3s (x8 over 4m9s)  batch-job-controller  Updated JobRun "testjobrun"
    Normal  Completed  4m3s                 batch-job-controller  JobRun completed successfully

Instances:
    Name            Running  Status     Restarts  Age
    testjobrun-1-0  0/1      Succeeded  0         4m9s
    testjobrun-2-0  0/1      Succeeded  0         4m9s
    testjobrun-3-0  0/1      Succeeded  0         4m9s
    testjobrun-4-0  0/1      Succeeded  0         4m9s
    testjobrun-5-0  0/1      Succeeded  0         4m9s
```
{: screen}


## Job status
{: #job-status}

The following table shows the possible status that your job might have.

| Status | Description |
| ------ | ------------|
| Pending | The job is accepted by the system, but one or more of the instances of the job are not yet created. This status includes time before a job is scheduled and time that is spent downloading images over the network, which might take a while. |
| Running | The job instances are created. At least one instance is still running, or is starting or restarting. |
| Succeeded | All job instances finished successfully and none are restarting. |
| Failed | All job instances finished, and at least one instance ended in failure. That is, the instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the job cannot be obtained, typically due to an error in communicating with the host. |
{: caption="Job status" caption-side="bottom"}
