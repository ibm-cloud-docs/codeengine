---

copyright:
  years: 2022, 2026
lastupdated: "2026-10-20"

keywords: monitoring for code engine, performance metrics, monitor, metrics, requests, pods, application, attributes, jobrun, panic mode, functions, platform metrics, IBM Cloud Monitoring, project settings, standard metrics, Compute Metrics, GPU Metrics, fleet monitoring

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring for {{site.data.keyword.codeengineshort}}
{: #monitor}

Get insight into the performance of your workloads that are deployed with {{site.data.keyword.codeenginefull}}. Metrics can help you find bottlenecks or predict possible production problems.
{: shortdesc}

You can use the {{site.data.keyword.mon_full}} service to monitor your {{site.data.keyword.codeengineshort}} workloads. {{site.data.keyword.codeengineshort}} forwards selected information about your workloads to {{site.data.keyword.mon_short}} so that you can monitor specific metrics such as requests, revisions, and duration.

## Set up your {{site.data.keyword.mon_full_notm}} service instance
{: #setup-monitor}

To set up your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}, you must create a {{site.data.keyword.mon_short}} instance and then enable Platform Metrics in the same region as the {{site.data.keyword.codeengineshort}} projects that you want to monitor. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region. For more information, see [{{site.data.keyword.mon_short}} Getting started tutorial](/docs/monitoring?topic=monitoring-getting-started).
{: shortdesc}

To set up {{site.data.keyword.mon_short}},

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**.
3. Either use an existing {{site.data.keyword.mon_short}} service instance or create a new one.
4. After the instance is ready, click **Configure platform metrics** to enable platform metrics.
5. Select a region and then a {{site.data.keyword.mon_short}} instance from that region. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region.
6. Enable monitoring in your project settings. For more information, see [Configuring project settings for observability](#project-settings-observability).

You can also start monitoring from your {{site.data.keyword.codeengineshort}} dashboard by selecting **Launch Monitoring**.
{: tip}

You can adapt the dashboards by creating a copy of a dashboard template and by editing it.
{: tip}

## Configuring Project Settings for Observability
{: #project-settings-observability}

You can configure Monitoring Settings for your project to control the flow of metrics. By enabling or disabling specific metrics at the project level, you can manage which performance metrics are collected and forwarded to your monitoring service instance.
{: shortdesc}

The rollout plan for these capabilities includes a pre-configuration phase. During this phase, settings are visible and editable but not yet active. For details, see [Upcoming changes to IBM Cloud Code Engine monitoring capabilities](https://cloud.ibm.com/notifications?selected=1790885511618){: external}.
{: attention}

### Metric Selection
{: #project-settings-observability-metric-selection}

When you configure monitoring settings using the console or CLI, you can configure metric selection with the following options:

* **All**: All metrics are enabled for the project. {{site.data.keyword.codeengineshort}} collects and forwards application, function, job, compute, and GPU Metrics to your monitoring instance.
* **None**: Metric collection is disabled for the project. {{site.data.keyword.codeengineshort}} does not scrape or forward any metrics.
* **Custom**: Granularly configure which metric categories are collected and forwarded. You can individually enable (`On`) or disable (`Off`) the following metrics:
  * **Applications**: Metrics for {{site.data.keyword.codeengineshort}} applications. See [Configure Application Metrics](#project-monitoring-applications).
  * **Functions**: Metrics for {{site.data.keyword.codeengineshort}} functions. See [Configure Function Metrics](#project-monitoring-functions).
  * **Jobs**: Metrics for {{site.data.keyword.codeengineshort}} jobs. See [Configure Job Metrics](#project-monitoring-jobs).
  * **Compute**: Container-level CPU and memory metrics. See [Configure Compute Metrics](#project-monitoring-compute).
  * **GPU**: GPU utilization and performance metrics for fleet workloads. See [Configure GPU Metrics for fleets](#project-monitoring-gpu).

You can configure monitoring settings from the console or by using the CLI.

### Configuring Monitoring Settings from the Console
{: #project-settings-observability-ui}

Use the {{site.data.keyword.codeengineshort}} console to configure project-wide monitoring settings.
{: shortdesc}

Before you can customize workload metrics, you must first connect an {{site.data.keyword.mon_full_notm}} instance to enable platform metrics for the project's region.
{: note}

1. Go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external} in the console.
2. Select your project.
3. Select **Project settings** > **Observability**.
4. In the **Platform Monitoring** section, verify that platform metrics are enabled. If not enabled, click **Add monitoring** to connect a monitoring instance in the project's region.
5. In the **Metrics selection** section, select your preferred mode:
   - **All**: Collect and forward all application, function, job, compute, and GPU Metrics.
   - **None**: Disable metric forwarding for all workloads in this project.
   - **Custom**: Granularly enable or disable specific metric categories.
6. Click **Save**.

### Configuring Monitoring Settings with the CLI
{: #project-settings-observability-cli}

Use CLI commands to view and update project-wide monitoring settings.
{: shortdesc}

1. To retrieve the current monitoring settings for your project, run the **`ibmcloud ce settings monitoring get`** command.

    ```sh
    ibmcloud ce settings monitoring get
    ```
    {: pre}

    By default, the command returns the following output, where standard metrics are set to `Custom`:

    ```text
    Enable metrics:  custom

    Standard metrics:
      Functions:     on
      Applications:  on
      Jobs:          on
      Compute:       off
      GPU:           off
    ```
    {: screen}

2. To change the monitoring settings for your project, run the **`ibmcloud ce settings monitoring update`** command with one of the following options.

    - To set metric selection to `all`, run the command with the `--standard-metrics all` option.

        ```sh
        ibmcloud ce settings monitoring update --standard-metrics all
        ```
        {: pre}

        ```text
        Updating project monitoring settings...
        OK

        Project Name:  myproject
        Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111

        Enable metrics:  all

        All standard metrics are enabled for this project.

        Standard metrics:
          Functions
          Applications
          Jobs
          Compute
          GPU
        ```
        {: screen}

    - To disable metric selection, run the command with the `--standard-metrics none` option.

        ```sh
        ibmcloud ce settings monitoring update --standard-metrics none
        ```
        {: pre}

        ```text
        Updating project monitoring settings...
        OK

        Project Name:  myproject
        Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111

        Enable metrics:  none

        Standard metrics are disabled for this project.
        ```
        {: screen}

    - To enable custom (granular) metric selection, run the command with the `--standard-metrics custom` option. When you set metric selection to `custom`, the granular settings take precedence on the basis of being set to `on` or `off`.

        ```sh
        ibmcloud ce settings monitoring update --standard-metrics custom
        ```
        {: pre}

        ```text
        Updating project monitoring settings...
        OK

        Project Name:  myproject
        Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111

        Enable metrics:  custom

        Standard metrics:
          Functions:     on
          Applications:  on
          Jobs:          on
          Compute:       on
          GPU:           off
        ```
        {: screen}

### Configure Application Metrics
{: #project-monitoring-applications}

When the Applications Metrics setting is set to `On`, {{site.data.keyword.codeengineshort}} collects and forwards scaling, traffic, and concurrency metrics for your application workloads.

The following table describes the standard Application Metrics:

| Metric | Description |
|---|---|
| [`ibm_codeengine_application_actual_instances`](#ibm_codeengine_application_actual_instances) | Number of pods that are currently allocated |
| [`ibm_codeengine_application_requested_instances`](#ibm_codeengine_application_requested_instances) | Number of pods requested |
| [`ibm_codeengine_application_not_ready_instances`](#ibm_codeengine_application_not_ready_instances) | Number of pods that are allocated but not yet ready to receive requests |
| [`ibm_codeengine_application_pending_instances`](#ibm_codeengine_application_pending_instances) | Number of pods that are pending allocation |
| [`ibm_codeengine_application_desired_instances`](#ibm_codeengine_application_desired_instances) | Number of pods that are desired by the autoscaler |
| [`ibm_codeengine_application_terminating_instances`](#ibm_codeengine_application_terminating_instances) | Number of pods that are terminating |
| [`ibm_codeengine_application_requests_total`](#ibm_codeengine_application_requests_total) | Total number of requests that are received by the application |
| [`ibm_codeengine_application_revision_count`](#ibm_codeengine_application_revision_count) | Total number of revisions for the application |
| [`ibm_codeengine_application_service_count`](#ibm_codeengine_application_service_count) | Total number of services |
| [`ibm_codeengine_application_route_count`](#ibm_codeengine_application_route_count) | Total number of routes |
| [`ibm_codeengine_application_target_concurrency_per_pod`](#ibm_codeengine_application_target_concurrency_per_pod) | Configured target concurrency per pod |
| [`ibm_codeengine_application_panic_request_concurrency`](#ibm_codeengine_application_panic_request_concurrency) | Target concurrency during panic mode |
| [`ibm_codeengine_application_stable_request_concurrency`](#ibm_codeengine_application_stable_request_concurrency) | Target concurrency during stable mode |
| [`ibm_codeengine_application_panic_mode`](#ibm_codeengine_application_panic_mode) | Specifies whether the autoscaler is operating in panic mode |
{: caption="Application Metrics" caption-side="bottom"}

### Configure Function Metrics
{: #project-monitoring-functions}

When the Functions Metrics setting is set to `On`, {{site.data.keyword.codeengineshort}} collects and forwards invocation, execution duration, and status metrics for your functions.

The following table describes the standard Function Metrics:

| Metric | Description |
|---|---|
| [`ibm_codeengine_functions_activations`](#ibm_codeengine_functions_activations) | Total number of function invocations |
| [`ibm_codeengine_functions_exceeded_limit`](#ibm_codeengine_functions_exceeded_limit) | Total number of function requests that exceed execution limits |
| [`ibm_codeengine_functions_execution_time_count`](#ibm_codeengine_functions_execution_time_count) | Count of recorded execution time measurements |
| [`ibm_codeengine_functions_execution_time_sum`](#ibm_codeengine_functions_execution_time_sum) | Cumulative execution time (in milliseconds) |
| [`ibm_codeengine_functions_init_time_count`](#ibm_codeengine_functions_init_time_count) | Count of initialization time measurements |
| [`ibm_codeengine_functions_init_time_sum`](#ibm_codeengine_functions_init_time_sum) | Cumulative initialization time (in milliseconds) |
| [`ibm_codeengine_functions_status_success`](#ibm_codeengine_functions_status_success) | Number of successfully executed function invocations |
| [`ibm_codeengine_functions_status_error_application`](#ibm_codeengine_functions_status_error_application) | Number of function invocations that fail with an application error |
| [`ibm_codeengine_functions_status_error_developer`](#ibm_codeengine_functions_status_error_developer) | Number of invoked functions that fail with an error in your code |
{: caption="Function Metrics" caption-side="bottom"}

### Configure Job Metrics
{: #project-monitoring-jobs}

When the Jobs Metrics setting is set to `On`, {{site.data.keyword.codeengineshort}} collects and forwards workload execution metrics for your batch jobs.

The following table describes the standard Job Metrics:

| Metric | Description |
|---|---|
| [`ibm_codeengine_jobruns`](#ibm_codeengine_jobruns) | Total number of job runs in your project |
{: caption="Job Metrics" caption-side="bottom"}

### Configure Compute Metrics
{: #project-monitoring-compute}

When the Compute Metrics setting is set to `On`, {{site.data.keyword.codeengineshort}} collects and forwards container-level CPU and memory usage metrics for the project's instances.

The following table describes the Compute Metrics for applications, jobs, and builds:

| Metric | Description |
|---|---|
| [`ibm_codeengine_instance_cpu_usage_millicores`](#ibm_codeengine_instance_cpu_usage_millicores) | Actual CPU usage of the instance in millicores |
| [`ibm_codeengine_instance_cpu_limit_millicores`](#ibm_codeengine_instance_cpu_limit_millicores) | CPU limit configured for the instance in millicores |
| [`ibm_codeengine_instance_memory_usage_bytes`](#ibm_codeengine_instance_memory_usage_bytes) | Actual memory usage of the instance in bytes |
| [`ibm_codeengine_instance_memory_limit_bytes`](#ibm_codeengine_instance_memory_limit_bytes) | Memory limit configured for the instance in bytes |
{: caption="Compute Metrics" caption-side="bottom"}

For fleets, enabling Compute Metrics collects container-level metrics from the Sysdig metrics library. For more information, see the [Sysdig container metrics library](https://docs.sysdig.com/en/docs/sysdig-monitor/metrics/metricslibrary/container/){: external}.

### Configure GPU Metrics for fleets
{: #project-monitoring-gpu}

When the GPU Metrics setting is set to `On`, {{site.data.keyword.codeengineshort}} collects and forwards NVIDIA GPU utilization and hardware performance metrics for your GPU-enabled fleet workers.

To enable GPU Metrics, the Compute Metrics setting must also be set to `On`. The combination of `Compute: Off` and `GPU: On` is invalid and cannot be configured.

The following table describes the standard GPU Metrics:

| Metric | Description |
|---|---|
| [`ibm_codeengine_xpu_utilization_ratio`](#ibm_codeengine_xpu_utilization_ratio) | GPU utilization (%) |
| [`ibm_codeengine_xpu_memory_used_bytes`](#ibm_codeengine_xpu_memory_used_bytes) | Framebuffer memory used (MiB) |
| [`ibm_codeengine_xpu_memory_free_bytes`](#ibm_codeengine_xpu_memory_free_bytes) | Framebuffer memory free (MiB) |
| [`ibm_codeengine_xpu_temperature_celsius`](#ibm_codeengine_xpu_temperature_celsius) | GPU temperature (°C) |
| [`ibm_codeengine_xpu_power_usage_watts`](#ibm_codeengine_xpu_power_usage_watts) | Power draw (W) |
| [`ibm_codeengine_xpu_clock_mhz`](#ibm_codeengine_xpu_clock_mhz) | Streaming multiprocessor clock (MHz) |
| [`ibm_codeengine_xpu_pcie_rx_bytes_total`](#ibm_codeengine_xpu_pcie_rx_bytes_total) | PCIe RX throughput (bytes/s) |
| [`ibm_codeengine_xpu_pcie_tx_bytes_total`](#ibm_codeengine_xpu_pcie_tx_bytes_total) | PCIe TX throughput (bytes/s) |
| [`ibm_codeengine_xpu_encoder_utilization_ratio`](#ibm_codeengine_xpu_encoder_utilization_ratio) | GPU encoder utilization (%) |
| [`ibm_codeengine_xpu_decoder_utilization_ratio`](#ibm_codeengine_xpu_decoder_utilization_ratio) | GPU decoder utilization (%) |
{: caption="GPU Metrics" caption-side="bottom"}

## Accessing your {{site.data.keyword.mon_full_notm}} metrics
{: #access-monitor}

To see your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}:

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**. Then select **Instances**.
3. Click **Dashboard** in the **View** column of your monitoring instance to open the dashboard for your monitoring instance.
4. From the navigation menu, select **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Project Overview**, **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Functions Overview**, **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Instance Resource Overview**, or **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Fleet GPU Monitoring**. If you don't see the {{site.data.keyword.codeengineshort}} dashboard in the menu, you can start monitoring from your {{site.data.keyword.codeengineshort}} application or job by selecting **Add Monitoring**.
5. Select the `10M` timeline or greater. Because Platform Metrics data has a 1 minute granularity, the first timeline that shows metrics is the `10M` timeline.

You can also start the {{site.data.keyword.mon_short}} dashboard at any time by selecting **Monitoring** from the {{site.data.keyword.codeengineshort}} Action menu.


When you use the {{site.data.keyword.mon_full_notm}} service to monitor {{site.data.keyword.codeengineshort}} workloads, delays can occur before the data is processed and available in {{site.data.keyword.mon_short}}. For example, right after you create your monitoring instance, it takes a few minutes before meaningful monitoring data is displayed. Be aware that it might take around 5 minutes for your monitoring data to show in {{site.data.keyword.mon_short}}.
{: important}

### `ibm_codeengine_application_actual_instances`
{: #ibm_codeengine_application_actual_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that are currently allocated.

Use this metric to observe the behavior of automatic application scaling and to observe how many application instances are running. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_actual_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that are currently allocated" caption-side="bottom"}

### `ibm_codeengine_application_requested_instances`
{: #ibm_codeengine_application_requested_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that the autoscaler requested from Kubernetes.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).


| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requested_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that the autoscaler requested" caption-side="bottom"}

### `ibm_codeengine_application_not_ready_instances`
{: #ibm_codeengine_application_not_ready_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that are not ready currently.

Use this metric to observe if there are issues with your running application.

Application instances that are in *not ready* state cannot serve requests. This *not ready* state indicates that something is preventing the app from becoming ready.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_not_ready_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that are not ready currently" caption-side="bottom"}

### `ibm_codeengine_application_pending_instances`
{: #ibm_codeengine_application_pending_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that are pending currently.

Use this metric to observe if there are issues with your running application.

You might observe pending applications when you observe automatic application scaling. Application instances that are pending are waiting to be scheduled. If your application remains in a pending state, perhaps the application cannot start because of insufficient resources, such as memory or CPU. See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_pending_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that are pending currently" caption-side="bottom"}

### `ibm_codeengine_application_desired_instances`
{: #ibm_codeengine_application_desired_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that the autoscaler wants to allocate.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_desired_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that the autoscaler wants to allocate" caption-side="bottom"}

### `ibm_codeengine_application_terminating_instances`
{: #ibm_codeengine_application_terminating_instances}

[Configure Application Metrics](#project-monitoring-applications)

Number of pods that are terminating currently.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if an application terminates when applications are scaled down.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_terminating_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Number of pods that are terminating currently" caption-side="bottom"}

### `ibm_codeengine_application_requests_total`
{: #ibm_codeengine_application_requests_total}

[Configure Application Metrics](#project-monitoring-applications)

Total number of HTTPS requests to the application.

Use this metric to monitor the number of HTTPS requests that are received by your application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requests_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name, http status code` |
{: caption="Total number of HTTPS requests to the application" caption-side="bottom"}

### `ibm_codeengine_application_revision_count`
{: #ibm_codeengine_application_revision_count}

[Configure Application Metrics](#project-monitoring-applications)

Number of revisions per application.

Use this metric to observe the number of revisions per application.

An application contains one or more revisions. Each update of an application configuration property creates a new revision of the application. {{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_revision_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Number of revisions per application" caption-side="bottom"}

### `ibm_codeengine_application_service_count`
{: #ibm_codeengine_application_service_count}

[Configure Application Metrics](#project-monitoring-applications)

Number of applications per project.

Use this metric to observe how many applications are in your project.

{{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_service_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Number of applications per project" caption-side="bottom"}

### `ibm_codeengine_application_route_count`
{: #ibm_codeengine_application_route_count}

[Configure Application Metrics](#project-monitoring-applications)

Number of routes per application.

{{site.data.keyword.codeengineshort}} supports only 1 route per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_route_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Number of routes per application" caption-side="bottom"}

### `ibm_codeengine_application_target_concurrency_per_pod`
{: #ibm_codeengine_application_target_concurrency_per_pod}

[Configure Application Metrics](#project-monitoring-applications)

The number of concurrent requests that you want for each pod.

Use this metric to observe the target concurrency value that is set for your application.

Target concurrency for application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_target_concurrency_per_pod`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="The number of concurrent requests that you want for each pod" caption-side="bottom"}

### `ibm_codeengine_application_panic_request_concurrency`
{: #ibm_codeengine_application_panic_request_concurrency}

[Configure Application Metrics](#project-monitoring-applications)

Average of requests count over the panic window.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if the application traffic arrives in bursts or if the traffic is steady.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Average of requests count over the panic window" caption-side="bottom"}


### `ibm_codeengine_application_stable_request_concurrency`
{: #ibm_codeengine_application_stable_request_concurrency}

[Configure Application Metrics](#project-monitoring-applications)

Average of requests count over the stable window.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if the application traffic arrives in bursts or if the traffic is steady.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_stable_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Average of requests count over the stable window" caption-side="bottom"}

### `ibm_codeengine_application_panic_mode`
{: #ibm_codeengine_application_panic_mode}

[Configure Application Metrics](#project-monitoring-applications)

Specifies whether panic mode is enabled.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe whether panic mode is used.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_mode`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Specifies if panic mode is enabled" caption-side="bottom"}


### `ibm_codeengine_functions_activations`
{: #ibm_codeengine_functions_activations}

[Configure Function Metrics](#project-monitoring-functions)

Number of invoked functions.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_activations`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name, function type` |
{: caption="Number of invoked functions" caption-side="top"}

### `ibm_codeengine_functions_exceeded_limit`
{: #ibm_codeengine_functions_exceeded_limit}

[Configure Function Metrics](#project-monitoring-functions)

Number of functions that are invoked after the limit for your project is exceeded. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_exceeded_limit`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name, function type` |
{: caption="Number of invoked functions after exceeding project limit" caption-side="top"}

### `ibm_codeengine_functions_execution_time_count`
{: #ibm_codeengine_functions_execution_time_count}

[Configure Function Metrics](#project-monitoring-functions)

Number of invoked functions that run to completion.

The `ibm_codeengine_functions_execution_time_count` and `ibm_codeengine_functions_execution_time_sum` metrics are used to determine the average execution time per invoked function.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_execution_time_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name` |
{: caption="Number of invoked functions that complete execution" caption-side="top"}

### `ibm_codeengine_functions_execution_time_sum`
{: #ibm_codeengine_functions_execution_time_sum}

[Configure Function Metrics](#project-monitoring-functions)

Sum of all execution time for invoked functions that run to completion.

The `ibm_codeengine_functions_execution_time_count` and `ibm_codeengine_functions_execution_time_sum` metrics are used to determine the average execution time per invoked function.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_execution_time_sum`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name` |
{: caption="Sum of all execution time for invoked functions" caption-side="top"}

### `ibm_codeengine_functions_init_time_count`
{: #ibm_codeengine_functions_init_time_count}

[Configure Function Metrics](#project-monitoring-functions)

Number of functions that complete initialization such that the code is loaded in {{site.data.keyword.codeengineshort}} and ready for execution.

The `ibm_codeengine_functions_init_time_count` and `ibm_codeengine_functions_init_time_sum` metrics are used to determine the average initialization time for invoked functions.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_init_time_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name` |
{: caption="Number of functions that complete initialization" caption-side="top"}

### `ibm_codeengine_functions_init_time_sum`
{: #ibm_codeengine_functions_init_time_sum}

[Configure Function Metrics](#project-monitoring-functions)

Sum of all initialization time for invoked functions.

The `ibm_codeengine_functions_init_time_count` and `ibm_codeengine_functions_init_time_sum` metrics are used to determine the average initialization time for invoked functions.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_init_time_sum`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name` |
{: caption="Sum of all initialization time for invoked functions" caption-side="top"}


### `ibm_codeengine_functions_status_success`
{: #ibm_codeengine_functions_status_success}

[Configure Function Metrics](#project-monitoring-functions)

Number of functions that are successfully invoked. A function is invoked successfully in {{site.data.keyword.codeengineshort}} after the function completes initialization, runs to completion, and your function code responds with a successful HTTP response status code.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_status_success`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name, function type` |
{: caption="Number of functions successfully invoked" caption-side="top"}

### `ibm_codeengine_functions_status_error_application`
{: #ibm_codeengine_functions_status_error_application}

[Configure Function Metrics](#project-monitoring-functions)

Number of invoked functions that fail during {{site.data.keyword.codeengineshort}} processing.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_status_error_application`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name, function type` |
{: caption="Number of invoked functions that fail within {{site.data.keyword.codeengineshort}}" caption-side="top"}

### `ibm_codeengine_functions_status_error_developer`
{: #ibm_codeengine_functions_status_error_developer}

[Configure Function Metrics](#project-monitoring-functions)

Number of invoked functions that fail with an error in your code.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_functions_status_error_developer`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, function name, function pod name, function type` |
{: caption="Number of invoked functions that fail with an error in your code" caption-side="top"}

### `ibm_codeengine_instance_cpu_usage_millicores`
{: #ibm_codeengine_instance_cpu_usage_millicores}

[Configure Compute Metrics](#project-monitoring-compute)

Actual CPU usage of the instance in millicores.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_instance_cpu_usage_millicores`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Project Name, Component Type, Component Name, instance` |
{: caption="Actual CPU usage of the instance in millicores" caption-side="bottom"}

### `ibm_codeengine_instance_cpu_limit_millicores`
{: #ibm_codeengine_instance_cpu_limit_millicores}

[Configure Compute Metrics](#project-monitoring-compute)

CPU limit configured for the instance in millicores.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_instance_cpu_limit_millicores`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Project Name, Component Type, Component Name, instance` |
{: caption="CPU limit configured for the instance in millicores" caption-side="bottom"}

### `ibm_codeengine_instance_memory_usage_bytes`
{: #ibm_codeengine_instance_memory_usage_bytes}

[Configure Compute Metrics](#project-monitoring-compute)

Actual memory usage of the instance in bytes.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_instance_memory_usage_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Project Name, Component Type, Component Name, instance`|
{: caption="Actual memory usage of the instance in bytes" caption-side="bottom"}

### `ibm_codeengine_instance_memory_limit_bytes`
{: #ibm_codeengine_instance_memory_limit_bytes}

[Configure Compute Metrics](#project-monitoring-compute)

Memory limit configured for the instance in bytes.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_instance_memory_limit_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Project Name, Component Type, Component Name, instance` |
{: caption="Memory limit configured for the instance in bytes" caption-side="bottom"}

### `ibm_codeengine_xpu_utilization_ratio`
{: #ibm_codeengine_xpu_utilization_ratio}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

GPU utilization ratio (%).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_utilization_ratio`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="GPU utilization ratio" caption-side="bottom"}

### `ibm_codeengine_xpu_memory_used_bytes`
{: #ibm_codeengine_xpu_memory_used_bytes}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

Framebuffer memory used (MiB).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_memory_used_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="Framebuffer memory used" caption-side="bottom"}

### `ibm_codeengine_xpu_memory_free_bytes`
{: #ibm_codeengine_xpu_memory_free_bytes}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

Framebuffer memory free (MiB).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_memory_free_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="Framebuffer memory free" caption-side="bottom"}

### `ibm_codeengine_xpu_temperature_celsius`
{: #ibm_codeengine_xpu_temperature_celsius}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

GPU temperature (°C).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_temperature_celsius`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="GPU temperature" caption-side="bottom"}

### `ibm_codeengine_xpu_power_usage_watts`
{: #ibm_codeengine_xpu_power_usage_watts}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

Power draw (W).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_power_usage_watts`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version`  |
{: caption="Power draw" caption-side="bottom"}

### `ibm_codeengine_xpu_clock_mhz`
{: #ibm_codeengine_xpu_clock_mhz}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

Streaming multiprocessor clock (MHz).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_clock_mhz`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="Streaming multiprocessor clock" caption-side="bottom"}

### `ibm_codeengine_xpu_pcie_rx_bytes_total`
{: #ibm_codeengine_xpu_pcie_rx_bytes_total}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

PCIe RX throughput (bytes/s).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_pcie_rx_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="PCIe RX throughput" caption-side="bottom"}

### `ibm_codeengine_xpu_pcie_tx_bytes_total`
{: #ibm_codeengine_xpu_pcie_tx_bytes_total}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

PCIe TX throughput (bytes/s).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_pcie_tx_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="PCIe TX throughput" caption-side="bottom"}

### `ibm_codeengine_xpu_encoder_utilization_ratio`
{: #ibm_codeengine_xpu_encoder_utilization_ratio}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

GPU encoder utilization (%).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_encoder_utilization_ratio`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="GPU encoder utilization" caption-side="bottom"}

### `ibm_codeengine_xpu_decoder_utilization_ratio`
{: #ibm_codeengine_xpu_decoder_utilization_ratio}

[Configure GPU Metrics for fleets](#project-monitoring-gpu)

GPU decoder utilization (%).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_xpu_decoder_utilization_ratio`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `project name, region, fleet name, worker name, device, model name, driver version` |
{: caption="GPU decoder utilization" caption-side="bottom"}

### `ibm_codeengine_jobruns`
{: #ibm_codeengine_jobruns}

[Configure Job Metrics](#project-monitoring-jobs)

Total number of job runs.

Use this metric to monitor how many job runs are in your project. {{site.data.keyword.codeengineshort}} has a quota for the number of jobs and job runs in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).  

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_jobruns`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, job Name, jobrun condition` |
{: caption="Total number of job runs" caption-side="bottom"}

## Attributes for segmentation
{: #attributes}

### Global Attributes
{: #global-attributes}

The following attributes are available for segmenting all the metrics previously listed. Not applicable for fleets GPU Metrics.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of `public`, `dedicated`, or `local`. |
| `Location` | `ibm_location` | The location of the monitored resource, which can be a region, data center, or global. |
| `Resource` | `ibm_resource` | The resource that is measured by the service, which is typically an identifying name or GUID. |
| `Resource Type` | `ibm_resource_type` | The type of the resource that is measured by the service. |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created. |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that is generating this metric. |
{: caption="Global attributes" caption-side="bottom"}

### More attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the previous tables. See the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Name of the namespace` | `ibm_codeengine_namespace` | Name of the namespace. This unique identifier is contained in the URL of your application. The default URL for applications is of the format `https://<appname>.<uuid>.<region>.codeengine.appdomain.cloud` where `appname` is the name of your application, `uuid` is the automatically generated unique identifier, and `region` is the region in which your {{site.data.keyword.codeengineshort}} project resides. The UUID portion of the URL is the name of the namespace. |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
| `HTTP status code` | `ibm_codeengine_status` | HTTP status code. |
| `Application name` | `ibm_codeengine_application_name` | Name of the application. |
| `Application revision name` | `ibm_codeengine_revision_name` | Name of the application revision. |
| `Gateway instance` | `ibm_codeengine_gateway_instance` | The gateway instance. |
| `Job Name` | `ibm_codeengine_job_name` | Name of the job that is used to create the job run.  |
| `Jobrun condition` | `ibm_codeengine_jobrun_condition` | The condition of the job run. |
| `Project name` | `ibm_codeengine_project_name` | Name of the project. |
| `Function name` | `ibm_codeengine_function_name` | Name of the invoked function.  |
| `Function pod name` | `ibm_codeengine_function_podname` | The name of the system pod that invoked the function.  |
| `Function type` | `ibm_codeengine_function_type` | The type for how the function was invoked (`sync` or `async`).  |
| `Component type` | `ibm_codeengine_component_type` | Type of the {{site.data.keyword.codeengineshort}} component that produced the metric. The value is `app`, `job`, or `build`. |
| `Component name` | `ibm_codeengine_component_name` | Name of the {{site.data.keyword.codeengineshort}} component (application name or job name) that produced the metric. |
| `Subcomponent type` | `ibm_codeengine_subcomponent_type` | Type of the {{site.data.keyword.codeengineshort}} subcomponent. The value is `app_revision` for application pods, `job_run` for job pods, or `build_run` for build pods. |
| `Subcomponent name` | `ibm_codeengine_subcomponent_name` | Name of the {{site.data.keyword.codeengineshort}} subcomponent (the revision name for application pods) that produced the metric. |
| `Instance name` | `ibm_codeengine_instance_name` | Name of the pod (instance) that produced the compute metric. |
| `Fleet project name` | `agent_tag_project_name` | Name of the project that contains the fleet. |
| `Fleet project region` | `agent_tag_project_region` | Region in which the project that contains the fleet resides. |
| `Fleet name` | `agent_tag_fleet` | Name of the fleet. |
| `Worker name` | `host_hostname` | Host name of the fleet worker. |
| `GPU model name` | `modelName` | Model name of the GPU. |
| `GPU device` | `device` | GPU device on the fleet worker. |
{: caption="Segmentation options" caption-side="bottom"}
