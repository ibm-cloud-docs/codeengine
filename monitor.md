---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-17"

keywords: monitoring for code engine, performance metrics, monitor, metrics, requests, pods, application, attributes, jobrun, panic mode

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
4. After the instance is ready, enable platform metrics by clicking **Configure platform metrics**.
5. Select a region and then a {{site.data.keyword.mon_short}} instance from that region. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region.

You can also start monitoring from your {{site.data.keyword.codeengineshort}} dashboard by selecting **Launch Monitoring**.
{: tip}

## Accessing your {{site.data.keyword.mon_full_notm}} metrics
{: #access-monitor}

To see your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}:

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**.
3. Click **Open dashboard** to open the dashboard for your monitoring instance.
4. From the navigation menu, select **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Project Overview**. If you don't see the {{site.data.keyword.codeengineshort}} dashboard in the menu, you can start monitoring from your {{site.data.keyword.codeengineshort}} application or job by selecting **Launch Monitoring**.
5. Select the `10M` timeline or greater. Because Platform Metrics data has a 1 minute granularity, the first timeline that shows metrics is the `10M` timeline.

You can also start the {{site.data.keyword.mon_short}} dashboard at any time by selecting **Monitoring** from the {{site.data.keyword.codeengineshort}} Action menu.


When you use the {{site.data.keyword.mon_full_notm}} service to monitor {{site.data.keyword.codeengineshort}} workloads, there can be delays before the data is processed and available in {{site.data.keyword.mon_short}}. For example, right after you create your monitoring instance, it takes a few minutes before there is a meaningful monitoring data to display. Be aware that it might take around 5 minutes for your monitoring data to show in {{site.data.keyword.mon_short}}.
{: important}


## Metrics available for {{site.data.keyword.codeengineshort}}
{: #metrics-by-plan}

| Metric Name |
|-----------|
| [`ibm_codeengine_application_actual_instances`](#ibm_codeengine_application_actual_instances) |
| [`ibm_codeengine_application_requested_instances`](#ibm_codeengine_application_requested_instances) |
| [`ibm_codeengine_application_not_ready_instances`](#ibm_codeengine_application_not_ready_instances) |
| [`ibm_codeengine_application_pending_instances`](#ibm_codeengine_application_pending_instances) |
| [`ibm_codeengine_application_desired_instances`](#ibm_codeengine_application_desired_instances) |
| [`ibm_codeengine_application_terminating_instances`](#ibm_codeengine_application_terminating_instances) |
| [`ibm_codeengine_application_requests_total`](#ibm_codeengine_application_requests_total) |
| [`ibm_codeengine_application_revision_count`](#ibm_codeengine_application_revision_count) |
| [`ibm_codeengine_application_service_count`](#ibm_codeengine_application_service_count) |
| [`ibm_codeengine_application_route_count`](#ibm_codeengine_application_route_count) |
| [`ibm_codeengine_application_target_concurrency_per_pod`](#ibm_codeengine_application_target_concurrency_per_pod) |
| [`ibm_codeengine_application_panic_request_concurrency`](#ibm_codeengine_application_panic_request_concurrency) |
| [`ibm_codeengine_application_stable_request_concurrency`](#ibm_codeengine_application_stable_request_concurrency) |
| [`ibm_codeengine_application_panic_mode`](#ibm_codeengine_application_panic_mode) |
| [`ibm_codeengine_jobruns`](#ibm_codeengine_jobruns) |
{: caption="Table 1: Metrics available for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

### `ibm_codeengine_application_actual_instances`
{: #ibm_codeengine_application_actual_instances}

Number of pods that are currently allocated.

Use this metric to observe the behavior of automatic application scaling and to observe how many application instances are running. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_actual_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 2: Number of pods that are currently allocated" caption-side="bottom"}

### `ibm_codeengine_application_requested_instances`
{: #ibm_codeengine_application_requested_instances}

Number of pods that the autoscaler requested from Kubernetes.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).


| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requested_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 3: Number of pods that the autoscaler requested" caption-side="bottom"}

### `ibm_codeengine_application_not_ready_instances`
{: #ibm_codeengine_application_not_ready_instances}

Number of pods that are not ready currently.

Use this metric to observe if there are issues with your running application.

Application instances that are in *not ready* state cannot serve requests. This *not ready* state indicates that something is preventing the app from becoming ready.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_not_ready_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 4: Number of pods that are not ready currently" caption-side="bottom"}

### `ibm_codeengine_application_pending_instances`
{: #ibm_codeengine_application_pending_instances}

Number of pods that are pending currently.

Use this metric to observe if there are issues with your running application.

You might observe pending applications when you observe automatic application scaling. Application instances that are pending are waiting to be scheduled. If your application remains in a pending state, perhaps the application cannot start because of insufficient resources, such as memory or CPU. See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_pending_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 5: Number of pods that are pending currently" caption-side="bottom"}

### `ibm_codeengine_application_desired_instances`
{: #ibm_codeengine_application_desired_instances}

Number of pods that the autoscaler wants to allocate.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to determine if you need to adjust the configurable values for your application.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_desired_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 6: Number of pods that the autoscaler wants to allocate" caption-side="bottom"}

### `ibm_codeengine_application_terminating_instances`
{: #ibm_codeengine_application_terminating_instances}

Number of pods that are terminating currently.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if an application terminates when applications are scaled down.

The number of running instances of an app are automatically scaled up or down based on configuration settings and your workloads. Application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale) and be aware of [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_terminating_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 7: Number of pods that are terminating currently" caption-side="bottom"}

### `ibm_codeengine_application_requests_total`
{: #ibm_codeengine_application_requests_total}

Total number of HTTPS requests to the application.

Use this metric to monitor the number of HTTPS requests that are received by your application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requests_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name, http status code` |
{: caption="Table 8: Total number of HTTPS requests to the application" caption-side="bottom"}

### `ibm_codeengine_application_revision_count`
{: #ibm_codeengine_application_revision_count}

Number of revisions per application.

Use this metric to observe the number of revisions per application.

An application contains one or more revisions. Each update of an application configuration property creates a new revision of the application. {{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_revision_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 9: Number of revisions per application" caption-side="bottom"}

### `ibm_codeengine_application_service_count`
{: #ibm_codeengine_application_service_count}

Number of applications per project.

Use this metric to observe how many applications are in your project.

{{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_service_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 10: Number of applications per project" caption-side="bottom"}

### `ibm_codeengine_application_route_count`
{: #ibm_codeengine_application_route_count}

Number of routes per application.

{{site.data.keyword.codeengineshort}} supports only 1 route per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_route_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 11: Number of routes per application" caption-side="bottom"}

### `ibm_codeengine_application_target_concurrency_per_pod`
{: #ibm_codeengine_application_target_concurrency_per_pod}

The number of concurrent requests that you want for each pod.

Use this metric to observe the target concurrency value that is set for your application.

Target concurrency for application scaling is configurable. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_target_concurrency_per_pod`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 12: The number of concurrent requests that you want for each pod" caption-side="bottom"}

### `ibm_codeengine_application_panic_request_concurrency`
{: #ibm_codeengine_application_panic_request_concurrency}

Average of requests count over the panic window.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if the application traffic arrives in bursts or if the traffic is steady.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 13: Average of requests count over the panic window" caption-side="bottom"}


### `ibm_codeengine_application_stable_request_concurrency`
{: #ibm_codeengine_application_stable_request_concurrency}

Average of requests count over the stable window.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe if the application traffic arrives in bursts or if the traffic is steady.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_stable_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 14: Average of requests count over the stable window" caption-side="bottom"}

### `ibm_codeengine_application_panic_mode`
{: #ibm_codeengine_application_panic_mode}

Specifies whether panic mode is enabled.

Use this metric to observe the behavior of automatic application scaling. Monitor this value to observe whether panic mode is used.

While *stable* mode is used for general operations, *panic* mode has a much shorter window, and is used to quickly scale up an application revision if a burst of traffic occurs.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_mode`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 15: Specifies if panic mode is enabled" caption-side="bottom"}

### `ibm_codeengine_jobruns`
{: #ibm_codeengine_jobruns}

Total number of job runs.

Use this metric to monitor how many job runs are in your project. {{site.data.keyword.codeengineshort}} has a quota for the number of jobs and job runs in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).  

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_jobruns`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, the jobrun condition` |
{: caption="Table 16: Total number of job runs" caption-side="bottom"}

## Attributes for segmentation
{: #attributes}

### Global Attributes
{: #global-attributes}

The following attributes are available for segmenting all the metrics previously listed.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of `public`, `dedicated`, or `local`. |
| `Location` | `ibm_location` | The location of the monitored resource, which can be a region, data center, or global. |
| `Resource` | `ibm_resource` | The resource that is measured by the service, which is typically an identifying name or GUID. |
| `Resource Type` | `ibm_resource_type` | The type of the resource that is measured by the service. |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created. |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that is generating this metric. |
{: caption="Table 17: Global attributes" caption-side="bottom"}

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
| `Jobrun condition` | `ibm_codeengine_jobrun_condition` | The condition of the job run. |
| `Project name` | `ibm_codeengine_project_name` | Name of the project. |
{: caption="Table 18: Segmentation options" caption-side="bottom"}




