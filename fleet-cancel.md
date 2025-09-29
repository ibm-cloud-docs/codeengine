---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-29"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Canceling or deleting fleets and workers
{: #fleets-cancel}

Review this information carefully before you cancel or delete a fleet. 

## Canceling a fleet
{: #fleets-cancel-type}

When you cancel a fleet, you can choose to implement a `soft stop` to cancel only pending tasks and allow any running tasks to complete, or you can implement a `hard stop` to immediately cancel all tasks.  

Soft stop
:   All pending tasks are changed to the `canceled` status. However, any instances or tasks that are already running will continue to run until they are completed. Worker nodes begin to de-provision as instances and tasks finish running. This is the default behavior for canceling a fleet.

Hard stop
:   All instances are deleted immediately, and any tasks that are already running or in a `pending` status are changed to the `canceled` status. No new instances are started and instances and worker nodes are deprovisioned immediately. 

### Canceling a fleet in the CLI
{: #fleets-cancel-cli}
{: cli}

To cancel a fleet in the CLI, run the following command. When prompted, specify `y` to confirm that you want to cancel the fleet.

```txt
ibmcloud ce fleet cancel --fleet-id FLEET_ID [--hard] [--force]
```
{: pre}

`--fleet-id`
:   The ID of the fleet.

`--hard`
:   Implement a hard stop cancelation to immediately delete all instances. Any tasks that are already running or in a `pending` status are changed to the `canceled` status. No new instances are started and instances and worker nodes are deprovisioned immediately. 

`--force`
:   Force the cancelation without a confirmation prompt. 


### Canceling a fleet in the UI
{: #fleets-cancel-ui}
{: ui}

Follow the steps to cancel a fleet in the UI.

1. Navigate to the [{{site.data.keyword.codeengineshort}} project page](https://cloud.ibm.com/containers/serverless/projects){external}. Select the relevant project, then select the fleet you want to cancel. 
2. Click **Actions**.
3. Click **Cancel**. 
4. Follow the prompt to cancel the fleet. If you want to implement a hard stop to cancel all tasks immediately and delete all instances and workers, select the option to do so. 
5. Click **Confirm cancelation**.


## Deleting a fleet
{: #fleet-delete}

When you delete a fleet, all of the fleet's tasks, instances, and workers are deleted immediately. 

### Deleting a fleet in the CLI
{: #fleet-delete-cli}
{: cli}

To delete a fleet in the CLI, run the following command. When prompted, specify `y` to confirm that you want to delete the fleet. 

```txt
ibmcloud ce fleet delete --fleet_id FLEET_ID [--force] [--ignore-not-found] [--wait] [--wait-timout]
```
{: pre}

`--fleet_id`
:   The ID of the fleet.

`--force`
:   Force the cancelation without a confirmation prompt. 

`--ignore-not-found`
:   Do not fail if the specified fleet is not found.

`--wait`
:   Specify to wait for confirmation that the fleet is deleted.

`--wait-timeout`
:   The number of seconds to wait for the fleet to be deleted.

### Deleting a fleet in the UI
{: #fleet-delete-ui}
{: ui}

Follow the steps to delete a fleet in the UI.

1. Navigate to the [{{site.data.keyword.codeengineshort}} project page](https://cloud.ibm.com/containers/serverless/projects){external}. Select the relevant project, then select the fleet you want to delete. 
2. Click **Actions**.
3. Click **Delete**. 
4. Follow the prompt to delete the fleet.

## Deleting fleet workers
{: #fleet-delete-worker}

When you delete a worker, it is deprovisioned and a new worker is immediately provisioned in its place. You can choose to implement a `soft stop` or a `hard stop` for a worker.

Soft stop
:   All pending tasks on the worker are changed to the `canceled` status. However, any instances or tasks that are already running will continue to run until they are completed. The worker is deprovisioned after the running tasks are complete, and a new worker node is provisioned in its place. This is the default behavior for deleting worker nodes.

Hard stop
:   All instances on the worker are deleted immediately, and any tasks that are already running or in a `pending` status are changed to the `canceled` status. The worker is deprovisioned immediately and a new worker node is provisioned in its place.

You can delete individual or groups of workers in a fleet. The remaining workers continue to run as normal. 

### Deleting a worker in the CLI
{: #fleet-delete-worker-cli}

To delete a worker in a fleet, run the following command. You can specify more than one worker. When prompted, specify `y` to confirm that you want to delete the worker.

```txt
ibmcloud ce fleet worker delete --fleet-id FLEET_ID --worker-name WORKER_NAME_1 --worker-name WORKER_NAME_2 [--hard] [--force] [--ignore-not-found] [--wait]
```
{: pre}

`--fleet-id`
:   The ID of the fleet.

`--worker-name`
:  The name of the worker to delete. You can specify more than one worker.

`--hard`
:   Implement a hard stop deletion to immediately delete all instances on the worker node. Any tasks that are already running or in a `pending` status are changed to the `canceled` status. The worker node is immediately deprovisioned and a new worker is provisioned in its place.

`--force`
:   Force the deletion without a confirmation prompt. 

`--ignore-not-found`
:   Specify to avoid error if the ID of a non-existing fleet is provided. 

`--wait` 
:   Specify to wait for confirmation that the worker no longer exists.

### Deleting a worker in the UI
{: #fleet-delete-worker-ui}

Follow the steps to delete a fleet worker in the UI.

1. Navigate to the [{{site.data.keyword.codeengineshort}} project page](https://cloud.ibm.com/containers/serverless/projects){external}. Select the relevant project. Then select the relevant fleet.
2. From the fleet page, select the **Workers** tab.
3. In the workers list, select each worker that you want to delete.
4. Click **Delete**.
5. Follow the prompt to delete the workers.  If you want to implement a hard stop to immediately cancel all tasks and instances on the workers, select the option to do so.
6. Click **Delete**.
