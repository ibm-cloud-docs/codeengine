---

copyright:
  years: 2022
lastupdated: "2022-07-05"

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

To set up your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}, you must create a service instance and then enable Platform Metrics in the same region as the {{site.data.keyword.codeengineshort}} projects that you want to monitor. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region. For more information, see [{{site.data.keyword.mon_short}} Getting started tutorial](/docs/monitoring?topic=monitoring-getting-started).
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
{: tip}

## Metrics available by Service Plan
{: #metrics-by-plan}

| Metric Name |
|-----------|
| [Average of requests count over the panic window](#ibm_codeengine_application_panic_request_concurrency) | 
| [Average of requests count over the stable window](#ibm_codeengine_application_stable_request_concurrency) | 
| [Number of pods autoscaler requested from Kubernetes](#ibm_codeengine_application_requested_instances) |
| [Number of applications per project](#ibm_codeengine_application_service_count) | 
| [Number of pods autoscaler wants to allocate](#ibm_codeengine_application_desired_instances) | 
| [Number of pods that are allocated currently](#ibm_codeengine_application_actual_instances) | 
| [Number of pods that are not ready currently](#ibm_codeengine_application_not_ready_instances) | 
| [Number of pods that are pending currently](#ibm_codeengine_application_pending_instances) | 
| [Number of pods that are terminating currently](#ibm_codeengine_application_terminating_instances) | 
| [Number of revisions per application](#ibm_codeengine_application_revision_count) | 
| [Number of routes per application](#ibm_codeengine_application_route_count) | 
| [The number of concurrent requests that you want for each pod](#ibm_codeengine_application_target_concurrency_per_pod) | 
| [Total number of HTTPS requests to the application](#ibm_codeengine_application_requests_total) |
| [Total number of `jobruns`](#ibm_codeengine_jobruns) |
| [Panic mode enabled or not](#ibm_codeengine_application_panic_mode) | 
{: caption="Table 1: Metrics available by plan names" caption-side="top"}

### Average of requests count over the panic window 
{: #ibm_codeengine_application_panic_request_concurrency}

Average of requests count over the panic window.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 2: Average of requests count over the panic window metric metadata." caption-side="top"}

### Average of requests count over the stable window 
{: #ibm_codeengine_application_stable_request_concurrency}

Average of requests count over the stable window.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_stable_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 3: Average of requests count over the stable window metric metadata." caption-side="top"}

### Number of pods that the autoscaler requested from Kubernetes 
{: #ibm_codeengine_application_requested_instances}

Number of pods that the autoscaler requested from Kubernetes.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requested_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 6: Number of pods autoscaler requested from Kubernetes metric metadata." caption-side="top"}

### Number of applications per project 
{: #ibm_codeengine_application_service_count}

Number of applications per project.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_service_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 5: Number of applications per project metric metadata." caption-side="top"}


### Number of pods that the autoscaler wants to allocate 
{: #ibm_codeengine_application_desired_instances}

Number of pods that the autoscaler wants to allocate.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_desired_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 7: Number of pods autoscaler wants to allocate metric metadata." caption-side="top"}

### Number of pods that are allocated currently 
{: #ibm_codeengine_application_actual_instances}

Number of pods that are allocated currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_actual_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 8: Number of pods that are allocated currently metric metadata." caption-side="top"}

### Number of pods that are not ready currently 
{: #ibm_codeengine_application_not_ready_instances}

Number of pods that are not ready currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_not_ready_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 9: Number of pods that are not ready currently metric metadata." caption-side="top"}

### Number of pods that are pending currently 
{: #ibm_codeengine_application_pending_instances}

Number of pods that are pending currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_pending_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 10: Number of pods that are pending currently metric metadata." caption-side="top"}

### Number of pods that are terminating currently 
{: #ibm_codeengine_application_terminating_instances}

Number of pods that are terminating currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_terminating_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 11: Number of pods that are terminating currently metric metadata." caption-side="top"}

### Number of revisions per application 
{: #ibm_codeengine_application_revision_count}

Number of revisions per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_revision_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 12: Number of revisions per application metric metadata." caption-side="top"}

### Number of routes per application 
{: #ibm_codeengine_application_route_count}

Number of routes per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_route_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name` |
{: caption="Table 13: Number of routes per application metric metadata." caption-side="top"}

### The number of concurrent requests that you want for each pod
{: #ibm_codeengine_application_target_concurrency_per_pod}

The number of concurrent requests that you want for each pod.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_target_concurrency_per_pod`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 14: The number of concurrent requests that you want for each pod metric metadata." caption-side="top"}

### Total number of HTTPS requests to the application 
{: #ibm_codeengine_application_requests_total}

Total number of HTTPS requests to the application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requests_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name, http status code` |
{: caption="Table 17: Total number of HTTPS requests to the application metric metadata." caption-side="top"}

### Total number of `jobruns`
{: #ibm_codeengine_jobruns}

Total number of `jobruns`

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_jobruns`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, the jobrun condition` |
{: caption="Table 18: Total number of job runs metric metadata." caption-side="top"}

### Is panic mode enabled or not 
{: #ibm_codeengine_application_panic_mode}

Returns `1` if autoscaler is in panic mode, `0` otherwise.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_mode`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, application name, application revision name` |
{: caption="Table 19: Is panic mode enabled or not metric metadata." caption-side="top"}

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
{: caption="Table 20: Global attributes" caption-side="top"}

### More attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the previous tables. See the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Name of the namespace` | `ibm_codeengine_namespace` | Name of the namespace. |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
| `HTTP status code` | `ibm_codeengine_status` | HTTP status code. |
| `Application name` | `ibm_codeengine_application_name` | Application name. |
| `Application revision name` | `ibm_codeengine_revision_name` | Application revision name. |
| `Gateway instance` | `ibm_codeengine_gateway_instance` | The gateway instance. |
| `Jobrun condition` | `ibm_codeengine_jobrun_condition` | The `jobrun` condition. |
| `Project name` | `ibm_codeengine_project_name` | Project name. |
{: caption="Table 21: Segmentation options" caption-side="top"}

