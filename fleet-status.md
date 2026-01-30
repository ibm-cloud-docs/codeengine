---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-27"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Understanding the status of your fleet
{: #fleet-status}

After a fleet is created, you can check the status of the overall fleet, as well as the status of any tasks or instances. You can use this information to help with debugging.
{: shortdesc}

## Fleet status
{: #status-fleets}

The fleet status indicates the overall status of all tasks and instances that run on the fleet. 

### Active fleet statuses
{: #status-active}

These statuses indicate that the fleet is already running. Depending on their progress, tasks can be pending, running, or in a final state while the fleet is active.

| Fleet status | Description | Possible task statuses |
| -----------  | ----------- | ---------------------- |
| Deploying |  The fleet is initiated. Instances are pending and now worker nodes are provisioned | `Pending` |
| Running |  At least one instance is running and at least one worker node is provisioned. |`Pending` \n `Running` \n `Succeeded` \n `Failed` \n `Canceled`|
| Canceling | A user has initiated a soft-stop cancellation on the fleet and some instances are still running. Instances and tasks on the fleet that were already running continue to run until finished. Instances and tasks that were pending are cancelled and will not run. | `Running` \n `Succeeded` \n `Failed` \n `Canceled` |
{: caption="Description of active fleet statuses" caption-side="bottom"}

### Final fleet statuses
{: #status-final}

These statuses indicate that the fleet is no longer running. No instances are running. Tasks are not running and are in a `succeeded`, `failed`, or `canceled` state. 

| Fleet status | Description | Possible task statuses |
| ------------ | ----------- | ---------------------- |
| Succeeded | All tasks completed successfully. No instances are running and worker nodes are de-provisioned or in the process of de-provisioning. | `Succeeded` \n `Failed` \n `Canceled` |
| Failed | No tasks are running and at least one task failed. No instances are running and worker nodes are de-provisioned or in the process of de-provisioning. | `Succeeded` \n `Failed` \n `Canceled` |
| Canceled | The user has initiated a cancellation on the fleet and no instances are running. Worker nodes are de-provisioned or in the process of de-provisioning. Tasks for this fleet can end in the “succeeded”, “failed”, or “cancelled” state. | `Succeeded` \n `Failed` \n `Canceled` |
{: caption="Description of final fleet statuses" caption-side="bottom"}

### Checking fleet status
{: #fleet-status-check}

To check the status of your fleet, run the `ibmcloud ce fleet get` command. Specify the fleet name. 

```txt
ibmcloud ce fleet get -n FLEET
```
{: pre}

Example output. 

```sh
Name                         Status        Tasks       Instances        Workers       Age        Zone           ID
fleet-123456ab-1     running      1            1                       1                   8h          eu-de-1     1a2b3c4d-56ef-78gh-90ijklmno
```
{: screen}


## Task status 
{: #status-tasks}

The task status indicates the health of individual tasks running on the fleet. Each task runs on a single instance. 

| Task status | Description |
| ----------- | ----------- |
| Pending | The task has no associated instance. 
| Running | The task has exactly one associated instance running.
| Succeeded | The last instance started on behalf of this task ended successfully and the task is no longer running.
| Failed | The last instance started on behalf of this task failed and the task has reached its maximum number of retries. The task is no longer running. Note that failed tasks return to the “pending” status until the maximum number of retries has been met. |
| Canceled | A user has canceled the fleet and the task is no longer running. This task was canceled before it succeeded or failed. | 
{: caption="Description of task statuses" caption-side="bottom"}

### Checking the status of tasks
{: #status-task-check}

To check the status of your tasks, run the `ibmcloud ce fleet task list` command. Specify the fleet name. 

```sh
ibmcloud ce fleet task list --fn FLEET
```
{: pre}

Example output. 

```sh
Task Summary:Pending Tasks: 1
Running Tasks: 1
Failed Tasks: 0
Succeeded Tasks: 1
Canceled Tasks: 0
```
{: screen}

## Worker node status
{: #status-workers}

You can check the status of the worker nodes that your instances run on. For more information, see the following pages.
- [Worker node states for Kubernetes](/docs/containers?topic=containers-worker-node-state-reference)
- [Worker node states for Red Hat OpenShift](/docs/openshift?topic=openshift-worker-node-state-reference)

<!-- link to worker node status docs here? https://cloud.ibm.com/docs/containers?topic=containers-worker-node-state-reference >
