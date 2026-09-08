---

copyright:
  years: 2025, 2026
lastupdated: "2026-09-08"

keywords: fleets, fleets in code engine, large volumes in code engine, deploy fleets in code engine, running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume, fleet status, fleet task status

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Understanding the status of your {{site.data.keyword.codeengineshort}} fleet
{: #fleet-status}

After a fleet is created in {{site.data.keyword.codeengineshort}}, you can check the status of the overall fleet, as well as the statuses of any tasks. You can use this information to help with debugging.
{: shortdesc}

## Fleet status
{: #status-fleets}

The fleet status indicates the overall operational status of a fleet. It is not related to the statuses of tasks. If you want to find out what tasks were completed successfully you need to check the tasks' statuses.

| Fleet status | Description | Possible user actions |
| ------------ | ----------- | --------------------- |
| Pending | There are tasks pending, but no tasks running. | **Add tasks**, **Cancel**, **Delete** |
| Running | There are running tasks. | **Add tasks**, **Cancel**, **Delete** |
| Standby | All tasks have been completed, there are no pending tasks. The fleet is waiting for new tasks to be added. Whether worker nodes are provisioned depends on the fleet's [scaling parameters](/docs/codeengine?topic=codeengine-fleet-scalingconfig). | **Add tasks**, **Cancel**, **Delete** |
| Canceling | A user has initiated a cancellation of the fleet and some instances are still running. Running tasks either complete or are terminated, depending on the cancellation mode. Tasks that were pending are canceled and will not run. | **Delete** |
| Canceled | The user initiated cancellation of the fleet completed. All pending and running tasks were canceled. All workers have been deleted. The fleet still counts toward the [project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas). | **Delete** |
| Deleting | A user initiated the deletion of the fleet. Running tasks are terminated. Worker nodes are deleted or in the process of deletion. The fleet is removed when deletion completes. | None |
{: caption="Fleet statuses" caption-side="bottom"}

### Checking fleet status in the {{site.data.keyword.codeengineshort}} console
{: #fleet-status-check-ui}
{: ui}

1. Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. Click the name of your project to open the Overview page.
3. Click **Fleets** to open a list of the fleets defined in your project.
4. The status of each fleet appears in the **Status** column of the table.

### Checking fleet status in the {{site.data.keyword.codeengineshort}} CLI
{: #fleet-status-check-cli}
{: cli}

To check the status of your fleet, run the `ibmcloud ce fleet get` command. Specify the fleet ID.

#### Example
{: #fleet-get-example}

```txt
ibmcloud ce fleet get --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e
```
{: pre}

#### Example output
{: #fleet-get-example-output}

```txt
Getting fleet '1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e'...
OK

Name:            fleet-0123456789  
ID:              1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e  
Status:          running  
Created:         2025-09-26T10:46:02Z  
Project region:  eu-de  
Project name:    myproj  

Tasks status:             
  Pending:     893  
  Running:     12  
  Failed:      0  
  Canceled:    0  
  Successful:  96  
  Total:       1001  

Code:                     
  Container image reference:  icr.io/codeengine/helloworld  

Tasks specification:      
  Task state store:  mytaskstore  
  Indexes:           0-1000  

Resources and scaling:    
  Container instance resources:    
    CPU per instance:     1  
    Memory per instance:  2G  

  Scaling settings:                
    Maximum container slots:  12  
    Minimum container slots:  0  
    Spare container slots:    0  
    Scale-down delay:         0s  

  Resiliency settings:             
    Maximum retries per task:  3  

Network placement:        
  Subnet pools:    
    Name:                my-pool
    Number of subnets:   1  
                         
    Subnet CRN:          crn:v1:bluemix:public:is:eu-de-1:a/abcdefabcdefabcdefabcd1234567890::subnet:1a1a-2b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f   
    Security Group CRN:  crn:v1:bluemix:public:is:eu-de:a/abcdefabcdefabcdefabcd1234567890::security-group:2b2b-3c3c3c3c-4d4d-5e5e-6f6f-7g7g7g7g7g7g  

Environment Variables:    
  Type     Name   Value  
  Literal  FOO    bar
```
{: screen}

## Task status
{: #status-tasks}

The task status indicates the health of individual tasks running on the fleet. Each task runs on a single instance.

| Task status | Description |
| ----------- | ----------- |
| Pending | The task has no associated instance. |
| Running | The task has exactly one associated instance running. |
| Succeeded | The last instance started on behalf of this task ended successfully and the task is no longer running. |
| Failed | The last instance started on behalf of this task failed and the task has reached its maximum number of retries. The task is no longer running. Note that failed tasks return to the “pending” status until the maximum number of retries has been met. |
| Canceled | A user has canceled the fleet and the task is no longer running. This task was canceled before it succeeded or failed. |
{: caption="Description of task statuses" caption-side="bottom"}

### Checking the status of tasks in the {{site.data.keyword.codeengineshort}} console
{: #status-task-check-ui}
{: ui}

1. Navigate to your fleet page. One way to navigate to your fleet page is to
    1. Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the name of your project to open the Overview page.
    3. Click **Fleets** to open a list of your fleets. Click the name of your fleet to open its fleet page.

2. From the fleet page, you can view information about the tasks, workers, and configuration details.
3. The status of each task appears in the **Status** column of the table.

### Checking the status of tasks in the {{site.data.keyword.codeengineshort}} CLI
{: #status-task-check-cli}
{: cli}

To check the status of your tasks, run the `ibmcloud ce fleet task list` command. Specify the fleet ID.

#### Example
{: #fleet-task-list-example}

```txt
ibmcloud ce fleet task list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e
```
{: pre}

#### Example output
{: #fleet-task-list-example-output}

```txt
Listing serverless fleet tasks...
OK

Task index  ID                                    Batch name  Status     Result code  Started               Duration  Worker name  
0           5b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  default     succeeded  exit_0       2026-08-06T19:48:13Z  26s       fleet-1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e-0 
1           4b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  default     running                 2026-08-06T19:52:14Z            fleet-1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e-1 
2           3b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  test2       pending
3           2b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  test2       running                 2026-08-06T19:57:14Z            fleet-1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e-1 
4           1b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  test2       failed     exit_0       2026-08-06T19:58:14Z  0s        fleet-1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e-0 
foobar      0b0b0b0b-3c3c-4d4d-5e5e-6f6f6f6f6f6f  test3       succeeded  exit_0       2026-08-06T19:59:14Z  1m        fleet-1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e-2 
```
{: screen}

## Worker node status
{: #status-workers}

You can check the status of the worker nodes that your instances run on. For more information, see the following pages.
- [Worker node states for Kubernetes](/docs/containers?topic=containers-worker-node-state-reference)
- [Worker node states for Red Hat OpenShift](/docs/openshift?topic=openshift-worker-node-state-reference)
