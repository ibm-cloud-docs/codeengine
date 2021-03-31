---

copyright:
  years: 2021
lastupdated: "2021-03-31"

keywords: monitoring for code engine, performance metrics

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Monitoring for {{site.data.keyword.codeengineshort}} 
{: #monitor}

Get insight into the performance of your workloads that are deployed with {{site.data.keyword.codeengineshort}}. Metrics can help you find bottlenecks or predict possible production problems. 
{: shortdesc}

You can use the {{site.data.keyword.mon_full}} service to monitor your {{site.data.keyword.codeengineshort}} workloads. {{site.data.keyword.codeengineshort}} forwards selected information about your workloads to {{site.data.keyword.mon_short}} so that you can monitor specific metrics such as requests, revisions, and duration.

## Set up your {{site.data.keyword.mon_full_notm}} service instance
{: #setup-monitor}

To set up your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}, you must create a service instance and then enable Platform Metrics in the same region as the {{site.data.keyword.codeengineshort}} projects that you want to monitor. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region.
{: shortdesc}

To set up {{site.data.keyword.mon_short}},

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**.
3. Either use an existing {{site.data.keyword.mon_short}} service instance or create a new one.
4. After the instance is ready, enable platform metrics by clicking **Configure platform metrics**.
5. Select a region and then a {{site.data.keyword.mon_short}} instance from that region. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region.



## Accessing your {{site.data.keyword.mon_full_notm}} metrics
{: #access-monitor}

To see your {{site.data.keyword.codeengineshort}} customer metrics dashboards in {{site.data.keyword.mon_short}}:

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**.
3. Select **View dashboard** to open the dashboard.
4. From the navigation menu, select **Dashboards->IBM->IBM Codeengine Project Overview**.

<br />
## Metrics available by Service Plan
{: metrics-by-plan}

| Metric Name |
|-----------|
| [Average of requests count over the panic window ](#ibm_codeengine_application_panic_request_concurrency) | 
| [Average of requests count over the stable window ](#ibm_codeengine_application_stable_request_concurrency) | 
| [Number of applications per project (namespace) ](#ibm_codeengine_application_per_namespace_service_count) | 
| [Number of applications per project ](#ibm_codeengine_application_service_count) | 
| [Number of pods autoscaler requested from Kubernetes ](#ibm_codeengine_application_requested_instances) | 
| [Number of pods autoscaler wants to allocate ](#ibm_codeengine_application_desired_instances) | 
| [Number of pods that are allocated currently ](#ibm_codeengine_application_actual_instances) | 
| [Number of pods that are not ready currently ](#ibm_codeengine_application_not_ready_instances) | 
| [Number of pods that are pending currently ](#ibm_codeengine_application_pending_instances) | 
| [Number of pods that are terminating currently ](#ibm_codeengine_application_terminating_instances) | 
| [Number of revisions per application ](#ibm_codeengine_application_revision_count) | 
| [Number of routes per application ](#ibm_codeengine_application_route_count) | 
| [The number of concurrent requests that you want for each pod ](#ibm_codeengine_application_target_concurrency_per_pod) | 
| [Total duration of HTTPS requests to the application ](#ibm_codeengine_application_request_duration_milliseconds_sum) | 
| [Total number of duration metrics of HTTPS requests to the application ](#ibm_codeengine_application_request_duration_milliseconds_count) | 
| [Total number of HTTPS requests to the application ](#ibm_codeengine_application_requests_total) | 
| [Panic mode enabled or not ](#ibm_codeengine_application_panic_mode) | 
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}

### Average of requests count over the panic window 
{: #ibm_codeengine_application_panic_request_concurrency}

Average of requests count over the panic window.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 2: Average of requests count over the panic window metric metadata" caption-side="top"}

### Average of requests count over the stable window 
{: #ibm_codeengine_application_stable_request_concurrency}

Average of requests count over the stable window.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_stable_request_concurrency`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 3: Average of requests count over the stable window metric metadata" caption-side="top"}

### Number of applications per project (namespace) 
{: #ibm_codeengine_application_per_namespace_service_count}

Number of applications per project (namespace).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_per_namespace_service_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id` |
{: caption="Table 4: Number of applications per project (namespace) metric metadata" caption-side="top"}

### Number of applications per project 
{: #ibm_codeengine_application_service_count}

Number of applications per project.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_service_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name` |
{: caption="Table 5: Number of applications per project metric metadata" caption-side="top"}

### Number of pods that the autoscaler requested from Kubernetes 
{: #ibm_codeengine_application_requested_instances}

Number of pods that the autoscaler requested from Kubernetes.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requested_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 6: Number of pods autoscaler requested from Kubernetes metric metadata" caption-side="top"}

### Number of pods that the autoscaler wants to allocate 
{: #ibm_codeengine_application_desired_instances}

Number of pods that the autoscaler wants to allocate.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_desired_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 7: Number of pods autoscaler wants to allocate metric metadata" caption-side="top"}

### Number of pods that are allocated currently 
{: #ibm_codeengine_application_actual_instances}

Number of pods that are allocated currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_actual_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 8: Number of pods that are allocated currently metric metadata" caption-side="top"}

### Number of pods that are not ready currently 
{: #ibm_codeengine_application_not_ready_instances}

Number of pods that are not ready currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_not_ready_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 9: Number of pods that are not ready currently metric metadata" caption-side="top"}

### Number of pods that are pending currently 
{: #ibm_codeengine_application_pending_instances}

Number of pods that are pending currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_pending_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 10: Number of pods that are pending currently metric metadata" caption-side="top"}

### Number of pods that are terminating currently 
{: #ibm_codeengine_application_terminating_instances}

Number of pods that are terminating currently.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_terminating_instances`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 11: Number of pods that are terminating currently metric metadata" caption-side="top"}

### Number of revisions per application 
{: #ibm_codeengine_application_revision_count}

Number of revisions per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_revision_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name` |
{: caption="Table 12: Number of revisions per application metric metadata" caption-side="top"}

### Number of routes per application 
{: #ibm_codeengine_application_route_count}

Number of routes per application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_route_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name` |
{: caption="Table 13: Number of routes per application metric metadata" caption-side="top"}

### The number of concurrent requests that you want for each pod
{: #ibm_codeengine_application_target_concurrency_per_pod}

The number of concurrent requests that you want for each pod.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_target_concurrency_per_pod`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, application revision name` |
{: caption="Table 14: The number of concurrent requests that you want for each pod metric metadata" caption-side="top"}

### Total duration of HTTPS requests to the application 
{: #ibm_codeengine_application_request_duration_milliseconds_sum}

Total duration of HTTPS requests to the application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_request_duration_milliseconds_sum`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, status progress` |
{: caption="Table 15: Total duration of HTTPS requests to the application metric metadata" caption-side="top"}

### Total number of duration metrics of HTTPS requests to the application 
{: #ibm_codeengine_application_request_duration_milliseconds_count}

Total number of duration metrics of HTTPs requests to the application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_request_duration_milliseconds_count`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, status progress` |
{: caption="Table 16: Total number of duration metrics of HTTPS requests to the application metric metadata" caption-side="top"}

### Total number of HTTPS requests to the application 
{: #ibm_codeengine_application_requests_total}

Total number of HTTPS requests to the application.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_requests_total`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project id, application name, status progress` |
{: caption="Table 17: Total number of HTTPS requests to the application metric metadata" caption-side="top"}

### Is panic mode enabled or not 
{: #ibm_codeengine_application_panic_mode}

Returns `1` if autoscaler is in panic mode, `0` otherwise.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_codeengine_application_panic_mode`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, name of the namespace, project name, project ID, application name, application revision name` |
{: caption="Table 18: Is panic mode enabled or not metric metadata" caption-side="top"}

## Attributes for segmentation
{: attributes}

### Global Attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics previously listed.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated, or local. |
| `Location` | `ibm_location` | The location of the monitored resource, which can be a region, data center, or global. |
| `Resource` | `ibm_resource` | The resource that is measured by the service, which is typically an identifying name or GUID. |
| `Resource Type` | `ibm_resource_type` | The type of the resource that is measured by the service. |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created. |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that is generating this metric. |

### More attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the previous tables. See the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Name of the namespace` | `ibm_codeengine_namespace` | Name of the namespace. |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
| `status progress` | `ibm_codeengine_status` | Status progress. |
| `The application name` | `ibm_codeengine_application_name` | Application name. |
| `application revision name` | `ibm_codeengine_application_revision_name` | Application revision name. |
| `project id` | `ibm_codeengine_project_id` | Project ID. |
| `project name` | `ibm_codeengine_project_name` | Project name. |

