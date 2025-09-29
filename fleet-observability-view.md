---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-29"

keywords: fleets observability, viewing logs for fleets, viewing, viewing logs, monitoring for fleets, monitoring data

subcollection: codeengine

---


{{site.data.keyword.attribute-definition-list}}

# Viewing logs and monitoring data for fleets
{: #fleet-observability-view}

Logging and monitoring can help you troubleshoot issues in {{site.data.keyword.codeenginefull}} and can provide insight into your workload performance. Follow these steps to view logs and monitoring data for fleets.
{: shortdesc}

- [Viewing fleet logs](#log-view)
- [Viewing monitoring data](#monitor-view)

## Viewing fleet logs
{: #log-view}

Follow the steps to view logs for fleets.

1. Navigate to the [IBM Cloud logging dashboard](https://cloud.ibm.com/observability/logging){: external}.

2. Find the **Instances** page and click on the logging instance for the Code Engine project that your fleets run in. Then click **Dashboard** to view the instance logs. 

3. In the left hand navigation menu, click **Explore logs** > **Logs**.

4. To adjust the logging timeframe, click **Last 15 minutes**, then select the timeframe you want to view. 

You can change the display view for logs by clicking **Columns** and choosing the column headers you want to view.
{: tip}

5. To filter through the logs, click **Add filter** and select the fields to filter for. For a full list of fields and their descriptions, see [Logging fields]().

You can save this logging view and filter settings for other workloads.
{: tip}

### Logging fields
{: #log-fields}


| Field name | Description | Set by? | Example value |
|---------|-----------|------------------|------------------|
| `applicationName` | Predefined ICL field that indicates which service instance emitted the log line. | `iclr-agent`, or `fleet-logging` | `ibm-platform-logs` |
| `subsystemName` | Predefined ICL field that indicates the log line is a platform log line. | `iclr-agent`, or `fleet-logging` | `codeengine:<project-guid>` |
| `app` | The cloud service that emitted the platform log line. For Code Engine, this will always be `codeengine`. | `iclr-agent`, or `fleet-logging` | `codeengine` |
| `tag` | Field set by fluentbit and derived from the input ID set in the fluentbit config. | `iclr-agent`, or `fleet-logging` | `platform.<id>.codeengine` |
| `originator` | Where the log line originated. This can indicate either Code Engine or the user. | `iclr-agent`, or `fleet-logging` | Possible values: `codeengine` or `user` |
| `codeengine.region` | The region of the Code Engine project. | system component, `iclr-agent`, `fleet-logging` | `eu-de` |
| `codeengine.project` | The name of the Code Engine project. | system component, `iclr-agent`, or `fleet-logging` | User defined string |
| `codeengine.projectGuid` | The GUID of the Code Engine project. | system component,`iclr-agent`, or `fleet-logging`| `edf5a781-9673-4c73-b2e2-cd4e04f673b4` |
| `codeengine.componentType` | The Code Engine component that relates to the log line. | System component, `iclr-agent`, or `fleet-logging` | Possible values: `app`, `job`, `job_run`, `fleet`, `function`, `build`, `build_run`, `container` |
| `codeengine.component` | The user defined component name that relates to this log line. | System component, `iclr-agent`, or `fleet-logging` | User defined string |
| `codeengine.subcomponentType` | The Code Engine subcomponent that relates to this log line. | System component, `iclr-agent`, or `fleet-logging`| Possible values: `app_revision`, `job_run`, `fleet_worker`, `fleet_instance`, `function`, `build_run`, `container` |
| `codeengine.subcomponent` | The user defined component name that is related to this log line. | System component, `iclr-agent`, or `fleet-logging`  |  User defined string |
| `codeengine.instanceId` | Optional. The pod name (for apps, jobs, and builds) or container instance ID (for functions and fleets). | `iclr-agent`, or `fleet-logging` | `my-app-0001-pod-abcde` |
| `codeengine.*` | Optional. Meta information useful for the user to create dashboards or alerts.| System component | `durationSeconds` | 
| `resourceGroupId` | Predefined ICL field. The resource group CRN for the Code Engine project. |  System component, `iclr-agent`, or `fleet-logging` | `crn:v1:bluemix:public:resource-controller::a/1010101ea01db1010101ebe1b0e10101d::resource-group:c1d01d010ec10101b0a10a1010101b010` |
| `messageKey` | A unique, human-readable identifier that you can use to filter logs and troubleshoot problems.  | System component |  `codengine.job-run-completed` |
| `logSourceCRN` | Predefined ICL field. The CRN of the Code Engine project. This field is only specified in multi-tenant log lines. | System component |  `<code engine project CRN>` |
| `message.message` | The human-readable log message. | System component or `iclr-agent` | String defined by system component or user | 
| `message.serviceName` |The name of the service that emitted that log line. | System component, `iclr-agent`, or `fleet-logging` | `codeengine` |
{: caption="Fleets logging fields." caption-side="bottom"}

## Viewing monitoring data
{: #monitor-view}

Follow the steps to view your fleet monitoring data.

1. Navigate to the [Monitoring instances page](https://cloud.ibm.com/observability/monitoring) in the console{: external}.
   
3. Find the monitoring instance for the Code Engine project that your fleet runs in and click **Dashboard**.
   
5. In the monitoring dashboard, click **Dashboards** > **Host Infrastructure** > **Host Resource Usage** to view the monitoring data.
   
7. Optional. Customize the monitoring dashboard to tailor it to your fleets data.
    1. Click **Copy to My Dashboards**.
    2. Add a name for the custom dashboard.
    3. Click the pencil icon to customize the settings,
    4. In the **Select a label** drop down, filters for `agent_tag_project_region`, `agent_tag_project_name` and `agent_tag_fleet`.
    5. Click **Save**.
    6. You can now filter your data by region, project name, and fleet name.
