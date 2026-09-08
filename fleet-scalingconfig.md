---

copyright:
  years: 2026
lastupdated: "2026-09-08"

keywords: fleets, fleet scaling, fleet scaling parameters, scale_max_instances, scale_min_instances, scale_spare_instances, scale_down_delay, Max container slots, Min container slots, Spare container slots, Scale down delay, fleets in code engine, --scale-max, --scale-min, --scale-spare, --scale-down-delay

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring fleet scaling
{: #fleet-scalingconfig}

When creating a fleet, use scaling parameters to control how many workers your {{site.data.keyword.codeengineshort}} fleet deploys and how it responds to changes in task load.
{: shortdesc}

All scaling parameters are optional and can be set when you create a fleet.

## Scaling parameters in the {{site.data.keyword.codeengineshort}} CLI
{: #fleet-scaling-params-cli}
{: cli}

To create a fleet, you use the `ibmcloud ce fleet run` or `ibmcloud ce fleet create` command. It takes the following options for fleet scaling. For a complete list of all available command options, see the [CLI reference](/docs/codeengine?topic=codeengine-cli#cli-fleet-create).

`--scale-max`
:   The upper bound on the total number of concurrent task slots across all workers. The fleet never creates workers beyond the capacity needed to run this many tasks simultaneously. Defaults to `10`.

`--scale-min`
:   The minimum number of concurrent task slots that are always kept provisioned, even when there are no pending or running tasks. Workers providing this capacity are kept alive and are never scaled down automatically.

    A fleet with active workers due to this setting, but without pending or running tasks has the **Standby** status.

    Must be less than or equal to `--scale-max`. Defaults to `0`.

`--scale-spare`
:   The number of free concurrent task slots maintained above the current number of running tasks. When all workers are busy, the fleet provisions additional workers to restore the spare buffer — up to `--scale-max`. New tasks arriving while spare capacity exists start immediately without waiting for a new worker.

    Must be less than or equal to `--scale-max`. Defaults to `0`.

`--scale-down-delay`
:   How long a worker stays alive after completing its last task before it becomes eligible for scale-down. A worker whose last task completed within the delay window picks up new tasks immediately when they arrive.

    Accepts a positive integer denoting the number of seconds of the delay. Defaults to `0` (workers scale down as soon as they are no longer needed).

## Scaling parameters in the {{site.data.keyword.codeengineshort}} console
{: #fleet-scaling-params-ui}
{: ui}

Max container slots
:   The upper bound on the total number of concurrent task slots across all workers. The fleet never creates workers beyond the capacity needed to run this many tasks simultaneously. Defaults to `10`.

Min container slots
:   The minimum number of concurrent task slots that are always kept provisioned, even when there are no pending or running tasks. Workers providing this capacity are kept alive and are never scaled down automatically.

    A fleet with active workers due to this setting, but without pending or running tasks has the **Standby** status.

    Must be less than or equal to **Max container slots**. Defaults to `0`.

Spare container slots
:   The number of free concurrent task slots maintained above the current number of running tasks. When all workers are busy, the fleet provisions additional workers to restore the spare buffer — up to **Max container slots**. New tasks arriving while spare capacity exists start immediately without waiting for a new worker.

    Must be less than or equal to **Max container slots**. Defaults to `0`.

Scale down delay
:   How long a worker stays alive after completing its last task before it becomes eligible for scale-down. A worker whose last task completed within the delay window picks up new tasks immediately when they arrive.

    Denotes the number of minutes of the delay. Defaults to `0` (workers scale down as soon as they are no longer needed).

## Workload patterns and relevant parameters
{: #fleet-scaling-patterns}

Which parameters to use depends on how tasks are produced, what your latency requirements are, and how stable the fleet configuration is.

### One-shot batch workload in the {{site.data.keyword.codeengineshort}} CLI
{: #fleet-scaling-one-shot-cli}
{: cli}

You know all tasks up front, supply them when you create the fleet, and the fleet finishes when the last task completes. This is the simplest model and requires no special scaling configuration beyond setting `--scale-max` to control how many tasks run in parallel. Use this approach when you need a dedicated fleet configuration for a batch of tasks.

**Relevant option:** `--scale-max`

### One-shot batch workload in the {{site.data.keyword.codeengineshort}} console
{: #fleet-scaling-one-shot-ui}
{: ui}

You know all tasks up front, supply them when you create the fleet, and the fleet finishes when the last task completes. This is the simplest model and requires no special scaling configuration beyond setting **Max container slots** to control how many tasks run in parallel. Use this approach when you need a dedicated fleet configuration for a batch of tasks.

**Relevant parameter:** Max container slots

### Scheduled batch workload in the {{site.data.keyword.codeengineshort}} CLI
{: #fleet-scaling-scheduled-cli}
{: cli}

You keep a fleet around and add a new batch of tasks on a schedule. Between batches, the fleet has no pending tasks. The gap between batches is predictable and long enough that keeping workers warm is not worthwhile, so there is no benefit to using `--scale-min`, `--scale-spare`, or `--scale-down-delay`. The fleet configuration remains stable for all batches.

**Relevant option:** `--scale-max`

### Scheduled batch workload in the {{site.data.keyword.codeengineshort}} console
{: #fleet-scaling-scheduled-ui}
{: ui}

You keep a fleet around and add a new batch of tasks on a schedule. Between batches, the fleet has no pending tasks. The gap between batches is predictable and long enough that keeping workers warm is not worthwhile, so there is no benefit to using **Min container slots**, **Spare container slots**, or **Scale down delay**. The fleet configuration remains stable for all batches.

**Relevant parameter:** Max container slots

### Continuous, latency-sensitive workload in the {{site.data.keyword.codeengineshort}} CLI
{: #fleet-scaling-continuous-cli}
{: cli}

Tasks arrive unpredictably throughout the day — triggered by user actions, sensor readings, or other real-time events. Waiting for a new worker to boot each time a task arrives would add unacceptable latency. Instead, configure the fleet to keep a pool of warm workers ready so that tasks can start immediately.

**Relevant options:** `--scale-max`, `--scale-min`, `--scale-spare`, `--scale-down-delay`

- Use `--scale-min` to ensure a baseline worker pool is always running, even when no tasks are queued. This is useful when traffic can drop to zero for a period, but you still want an instant start when it resumes.
- Use `--scale-spare` to keep a number of free task slots available above the current number of running tasks. When a task arrives, processing begins immediately on an already-running worker, and the fleet provisions more workers in the background to replenish the spare capacity.
- Use `--scale-down-delay` to prevent workers from scaling down immediately after their last task completes. This setting is useful when tasks arrive intermittently with temporary gaps between them, allowing workers to remain available and avoiding unnecessary scale-down and scale-up cycles. By keeping workers warm, it can reduce task startup latency, minimize worker initialization overhead, and lower the cost associated with repeatedly provisioning new workers.

### Continuous, latency-sensitive workload in the {{site.data.keyword.codeengineshort}} console
{: #fleet-scaling-continuous-ui}
{: ui}

Tasks arrive unpredictably throughout the day — triggered by user actions, sensor readings, or other real-time events. Waiting for a new worker to boot each time a task arrives would add unacceptable latency. Instead, configure the fleet to keep a pool of warm workers ready so that tasks can start immediately.

**Relevant parameters:** **Max container slots**, **Min container slots**, **Spare container slots**, **Scale down delay**

- Use **Min container slots** to ensure a baseline worker pool is always running, even when no tasks are queued. This is useful when traffic can drop to zero for a period, but you still want an instant start when it resumes.
- Use **Spare container slots** to keep a number of free task slots available above the current number of running tasks. When a task arrives, processing begins immediately on an already-running worker, and the fleet provisions more workers in the background to replenish the spare capacity.
- Use **Scale down delay** to prevent workers from scaling down immediately after their last task completes. This setting is useful when tasks arrive intermittently with temporary gaps between them, allowing workers to remain available and avoiding unnecessary scale-down and scale-up cycles. By keeping workers warm, it can reduce task startup latency, minimize worker initialization overhead, and lower the cost associated with repeatedly provisioning new workers.
