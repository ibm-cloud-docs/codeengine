---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-10"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Running a fleet
{: #fleet-run}

Follow these steps to run a fleet with the CLI or with the console. Note that fleets run as soon as they are created, so that `running` a fleet and `creating` a fleet are the same operation.
{: shortdesc} 

## Before you begin
{: #fleet-run-before}

To successfully run a fleet, make sure you have followed the steps in [Preparing to run your fleet](/docs/codeengine?topic=codeengine-fleet-prep). You also have the option to use Code Engine to [build the image](/docs/codeengine?topic=codeengine-plan-build) you reference when you create your fleet.

## Running a fleet by using the CLI
{: #fleet-run-cli}
{: cli}

Use the following example command to run a fleet. This command allows additional options. For a complete list of all available command options, see the [CLI docs](/docs/codeengine?topic=codeengine-cli#cli-fleet-create).

```txt
ibmcloud ce fleet run --name my-fleet --image icr.io/codeengine/helloworld --subnetpool-name my-pool --tasks-state-store mytaskstore --tasks 1
```
{: pre}

`--name`
:   The name of the fleet. This value must be unique across all fleets within the same project. If no fleet name is specified, a random one is generated. 

`--image`
:   The name of the container image that is used to process the tasks. This value is _required_.

`--subnetpool-name`
:   The name of the subnet pool to use for the fleet network placement.

`--tasks-state-store`
:   Specify the persistent data store that stores the state of the tasks of the fleet. This value is _required_.

`--tasks`
:   The number of tasks to run. 

Example output.

```sh
Successfully created fleet with name 'my-fleet' and ID '1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' 
Run 'ibmcloud ce fleet get --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to check the fleet status.
Run 'ibmcloud ce fleet worker list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of provisioned workers.
Run 'ibmcloud ce fleet task list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of tasks.
OK
```
{: screen}

## Running a fleet by using the console
{: #fleet-run-ui}
{: ui}

Follow these steps to run a fleet in the Code Engine console. 

1. Open the [Code Engine](https://cloud.ibm.com/containers/serverless/overview){: external} console.
2. Click **Start Creating**. 
3. Select a project from the list of available projects. You can also create a new one. You must have a selected project to run a fleet.
4. Select the option to create a fleet. 
5. Specify a name for the fleet. Make sure the name is unique across all fleets within the project.
6. Specify a container image for your fleet, for example, `icr.io/codeengine/helloworld`. If you have your own source code that you want to turn into a container image, see Planning your build. For more information about the code that is used for this example, see helloworld.
7. Follow the prompts to configure your fleet. 
8. In the Tasks section, configure the task specification method for the fleet. For more information, see [Task specification](#fleet-task-spec).
9. In the Resources and scaling section, configure your instance resources and specify how your instances scale up or down. 
10. In the Network placement section, click **Select subnet pools**.
    1. Create a new subnet pool to specify the network placement of the workers of this fleet. See [Working with subnet pool connectivity in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-connectivity-subnetpool) for more information.
    2. Or select one or more existing subnet pools to specify the network placement of the workers of this fleet.
    3. Click **Apply** to confirm your selection.
11. In the **Environment variables** and **Volume mounts** sections, add optional key-value pairs, configmaps, or additional files that can be used by your running code. 
12. Click create. 

## Task specification
{: #fleet-task-spec}

Fleets always have at least one task, but can have a much larger number. You can specify the number of tasks to complete, the number of task instances to run at a time, and the order in which tasks are completed. When you run your fleet, worker nodes automatically scale up based on the number of tasks to be completed.

You can specify tasks in the following ways: 

- **Number of tasks**: To run a specific number of tasks, you can specify any positive integer. In the CLI, use the `--tasks` option. In the UI, select **Number of tasks** and enter the number you want to run. 
- **Task index**: To specify a range of tasks, you can specify a task index that includes a comma separated list of ranges and positive integers, such as `2-5,7-8,10`. In the CLI, use the `--task-indexes` option. In the UI, select **Task indexes** and enter the range. 
- **Task file**: To have different tasks run with different commands or arguments, you can create a task specification file that overrides the image definition. The optional `idx` field can be used to specify a custom task index. This file needs to be formatted as JSONL. In the CLI, specify the file with the `--tasks-from-local-file` or `--tasks-from-cos-object` option. In the UI, select **Tasks from file** and specify the file name. See an example of lines that can be added to a task specification file below. 

Example lines in a task specification file.

```json
{ "cmds": ["my", "multipart", "command"], "args": ["arg1", "arg2"] }
{ "cmds": ["other", "cmd"], "args": ["arg"], "idx": "foo" }
{ "args": ["argA", "argB", "argC"], "idx": "bar" }
{ "cmds": ["just", "another", "command"], "idx": "1234" }
```
{: screen}


## Deleting a fleet by using the CLI
{: #fleet-delete-cli}
{: cli}

A fleet is not deleted automatically when it reaches its final state. Since there is a quota limit of 1000 fleets per project (see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas)), delete the fleet using the CLI when you do not need it anymore.

Use the following example command to delete a fleet. This command allows additional options. For a complete list of all available command options, see the [CLI docs](/docs/codeengine?topic=codeengine-cli#cli-fleet-delete).

```txt
ibmcloud ce fleet delete --force --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e
```
{: pre}

## Deleting a fleet by using the console
{: #fleet-delete-ui}
{: ui}

A fleet is not deleted automatically when it reaches its final state. Since there is a quota limit of 1000 fleets per project (see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas)), delete the fleet using the CLI when you do not need it anymore.

Follow these steps to delete a fleet in the console.

1. Go to the Fleets page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Fleets** to see a list of existing fleets.
2. Go to the row with the fleet that you want to remove and click the delete (trash can) icon.
3. Confirm the deletion when prompted.
