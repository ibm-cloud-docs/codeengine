---

copyright:
  years: 2025, 2026
lastupdated: "2026-09-08"

keywords: fleets, fleets in code engine, large volumes in code engine, deploy fleets in code engine, running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume, add task

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Running a fleet
{: #fleet-run}

Follow these steps to run a {{site.data.keyword.codeengineshort}} fleet with the CLI or with the console.
{: shortdesc}

## Before you begin
{: #fleet-run-before}

To successfully run a fleet, make sure you have followed the steps in [Preparing to run your fleet](/docs/codeengine?topic=codeengine-fleet-prep). You also have the option to use {{site.data.keyword.codeengineshort}} to [build the image](/docs/codeengine?topic=codeengine-plan-build) you reference when you create your fleet.

## Running a fleet by using the console
{: #fleet-run-ui}
{: ui}

Follow these steps to run a fleet in the {{site.data.keyword.codeengineshort}} console.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/containers/serverless/overview){: external} console.
2. Click **Start creating**.
3. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to run a fleet.
4. Select the option to create a fleet.
5. Specify a name for the fleet. Make sure the name is unique across all fleets within the project.
6. Specify a container image for your fleet, for example, `icr.io/codeengine/helloworld`. If you have your own source code that you want to turn into a container image, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.
7. Follow the prompts to configure your fleet. For details on the significance of scaling parameters, see [Configuring fleet scaling](/docs/codeengine?topic=codeengine-fleet-scalingconfig#fleet-scaling-params-ui).
8. In the Tasks section, configure the task specification method for the fleet. For more information, see [Task specification](#fleet-task-spec).
9. In the Resources and scaling section, configure your instance resources and specify how your instances scale up or down.
10. In the Network placement section, click **Select subnet pools**.
    1. Create a new subnet pool to specify the network placement of the workers of this fleet. See [Working with subnet pool connectivity in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-connectivity-subnetpool) for more information.
    2. Or select one or more existing subnet pools to specify the network placement of the workers of this fleet.
    3. Click **Apply** to confirm your selection.
11. In the **Environment variables** and **Volume mounts** sections, add optional key-value pairs, configmaps, or additional files that can be used by your running code.
12. Click **Create**.

## Task specification
{: #fleet-task-spec}

You can create a fleet with or without initial tasks, and add tasks at any time.

### Specifying tasks in the console
{: #fleet-task-spec-ui}
{: ui}

To create a fleet without initial tasks, see [Creating a fleet without initial tasks by using the console](#fleet-without-task-console). To add tasks after creation, see [Adding tasks to a fleet by using the console](#fleet-add-task-console).

You can specify tasks in the following ways:

- **Number of tasks**: Select **Number of tasks** and specify any positive integer.
- **Task indexes**: To specify a range of tasks, you can specify a task index that includes a comma-separated list of ranges and positive integers, such as `2-5,7-8,10`. Select **Task indexes** and enter the ranges.
- **Tasks from file**: To have different tasks run with different commands or arguments, you can create a task specification file that overrides the image definition. The optional `idx` field can be used to specify a custom task index. This file must be formatted as JSONL. Select **Tasks from file**. Either upload a local file or specify a path to a file in {{site.data.keyword.cos_full_notm}}. See the following example of lines that can be added to a task specification file.
    ```json
    { "cmds": ["my", "multipart", "command"], "args": ["arg1", "arg2"] }
    { "cmds": ["other", "cmd"], "args": ["arg"], "idx": "foo" }
    { "args": ["argA", "argB", "argC"], "idx": "bar" }
    { "cmds": ["just", "another", "command"], "idx": "1234" }
    ```
    {: codeblock}

- **Tasks from {{site.data.keyword.cos_full_notm}}**: Specify tasks based on the objects in a persistent data store ({{site.data.keyword.cos_short}} bucket). Each object generates one task. Select **Tasks from Cloud Object Storage** and create or select a persistent data store. Optionally, specify a bucket subpath.


### Specifying tasks in the CLI
{: #fleet-task-spec-cli}
{: cli}

To create a fleet without initial tasks, see [Creating a fleet without initial tasks by using the CLI](#fleet-without-task-cli). To add tasks after creation, see [Adding tasks to an existing fleet by using the CLI](#fleet-add-task-cli). To create a fleet with initial tasks, see [Creating a fleet with initial tasks by using the CLI](#fleet-with-initial-task-cli).

You can specify tasks in the following ways:

- **Number of tasks**: Specify any positive integer. Use the `--tasks` option to specify the number of tasks you want to run. To create a fleet without tasks, omit the `--tasks` option.
- **Task indexes**: To specify a range of tasks, you can specify a task index that includes a comma-separated list of ranges and positive integers, such as `2-5,7-8,10`. Use the `--task-indexes` option.
- **Tasks from file**: To have different tasks run with different commands or arguments, you can create a task specification file that overrides the image definition. The optional `idx` field can be used to specify a custom task index. This file must be formatted as JSONL. Specify the file with the `--tasks-from-local-file` or `--tasks-from-cos-object` option. See the following example of lines that can be added to a task specification file.
    ```json
    { "cmds": ["my", "multipart", "command"], "args": ["arg1", "arg2"] }
    { "cmds": ["other", "cmd"], "args": ["arg"], "idx": "foo" }
    { "args": ["argA", "argB", "argC"], "idx": "bar" }
    { "cmds": ["just", "another", "command"], "idx": "1234" }
    ```
    {: codeblock}

- **Tasks from {{site.data.keyword.cos_full_notm}}**: Specify tasks based on the objects in a persistent data store ({{site.data.keyword.cos_short}} bucket). Each object generates one task. Use the `--tasks-from-cos-bucket` option to specify a {{site.data.keyword.cos_short}} bucket and an optional bucket subpath.

## Creating a fleet without initial tasks by using the console
{: #fleet-without-task-console}
{: ui}

You can create a fleet without providing any tasks. If **Min container slots** or **Spare container slots** is non-zero, workers are provisioned immediately. Otherwise, no workers are created until the first tasks are added.

This is useful when the fleet is a shared, long-lived resource that receives tasks from multiple sources or on a schedule.

To create a fleet without initial tasks, follow the steps in [Running a fleet by using the console](#fleet-run-ui). In step 8, set **Specify an initial set of tasks** to **No**.

## Adding tasks to a fleet by using the console
{: #fleet-add-task-console}
{: ui}

You can add tasks to a fleet at any time — whether the fleet is in `pending`, `running` or `standby` status — by using the **Add tasks** button.

Asynchronously, {{site.data.keyword.codeengineshort}} creates the task records and, if needed, provisions additional workers.

Follow these steps to add tasks to an existing fleet in the Code Engine console.

1. Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. Click the name of your project to open the Overview page.
3. Click **Fleets** to open a list of your fleets. Click the name of your fleet to open the details page.
4. Click **Add tasks**.
5. Specify a set of tasks to add to the fleet. See also [Task specification](#fleet-task-spec).
6. Click **Add**.

## Creating a fleet without initial tasks by using the CLI
{: #fleet-without-task-cli}
{: cli}

Use the following example command to run a fleet without an initial task. This command allows additional options. For a complete list of all available command options, see the [CLI reference](/docs/codeengine?topic=codeengine-cli#cli-fleet-create).

```sh
ibmcloud ce fleet run --name my-fleet --image icr.io/codeengine/helloworld --subnetpool-name my-pool --tasks-state-store mytaskstore
```
{: pre}

`--name`
:   The name of the fleet. This value must be unique across all fleets within the same project. If no fleet name is specified, a random one is generated.

`--image`
:   The reference to the container image that is used to process the tasks. This value is **required**.

`--subnetpool-name` or `--subnetpool-id`
:   The name of the subnet pool to use for the fleet network placement.
:   The ID of the subnet pool to use for the fleet network placement.

You must specify either `--subnetpool-name` or `--subnetpool-id`.

`--tasks-state-store`
:   Specify the persistent data store that stores the state of the tasks of the fleet. This value is **required**.

Example output.

```txt
Successfully created fleet with name 'my-fleet' and ID '1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e'
Run 'ibmcloud ce fleet get --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to check the fleet status.
Run 'ibmcloud ce fleet worker list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of provisioned workers.

OK
```
{: screen}

## Adding tasks to an existing fleet by using the CLI
{: #fleet-add-task-cli}
{: cli}

Use the following example command to add tasks to an existing fleet. This command allows additional options. For a complete list of all available command options, see the [CLI reference](/docs/codeengine?topic=codeengine-cli#cli-fleet-task-create).

Alternatively, you can use the `fleet task add` command.

```sh
ibmcloud ce fleet task create --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e --tasks 6
```
{: pre}

`--fleet-id`
:   The UUID of the fleet the task belongs to. This value is **required**.

`--tasks`
:   Specify the number of tasks that are to be processed by the fleet. This value is **required**.

Example output.

```txt
Successfully added tasks to fleet with name 'my-fleet' and ID '1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e'
Run 'ibmcloud ce fleet get --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to check the fleet status.
Run 'ibmcloud ce fleet worker list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of provisioned workers.
Run 'ibmcloud ce fleet task list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of tasks.

OK
```
{: screen}

## Creating a fleet with initial tasks by using the CLI
{: #fleet-with-initial-task-cli}
{: cli}

Use the following example command to run a fleet with initial tasks. This command allows additional options. For a complete list of all available command options, see the [CLI reference](/docs/codeengine?topic=codeengine-cli#cli-fleet-create).

When all available tasks are processed, the fleet enters the **Standby** state. Workers that are no longer needed for providing **Min container slots** are scaled down until new tasks are added.

```sh
ibmcloud ce fleet run --name my-fleet --image icr.io/codeengine/helloworld --subnetpool-name my-pool --tasks-state-store mytaskstore --tasks 1
```
{: pre}

`--name`
:   The name of the fleet. This value must be unique across all fleets within the same project. If no fleet name is specified, a random one is generated.

`--image`
:   The reference to the container image that is used to process the tasks. This value is **required**.

`--subnetpool-name` or `--subnetpool-id`
:   The name of the subnet pool to use for the fleet network placement.
:   The ID of the subnet pool to use for the fleet network placement.

You must specify either `--subnetpool-name` or `--subnetpool-id`.

`--tasks-state-store`
:   Specify the persistent data store that stores the state of the tasks of the fleet. This value is **required**.

`--tasks`
:   The number of tasks to run.

Example output.

```txt
Successfully created fleet with name 'my-fleet' and ID '1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e'
Run 'ibmcloud ce fleet get --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to check the fleet status.
Run 'ibmcloud ce fleet worker list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of provisioned workers.
Run 'ibmcloud ce fleet task list --fleet-id 1a1a1a1a-2b2b-3c3c-4d4d-5e5e5e5e5e5e' to retrieve a list of tasks.
OK
```
{: screen}
