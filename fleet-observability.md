---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-09"

keywords: fleets, fleet logging, fleet monitoring, fleet observability, observability, logging, monitoring, Cloud Logs, Cloud Monitoring

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Setting up observability for fleets
{: #fleet-observability}

Logging and monitoring can help you troubleshoot issues in {{site.data.keyword.codeenginefull}} and can provide insight into your workload performance. Setting up logging and monitoring for fleets is done at the project level and is different from other {{site.data.keyword.codeengineshort}} features. 

- [Setting up logging for fleets](#fleet-log)
- [Setting up monitoring for fleets](#fleet-monitor)

Logging and monitoring are optional, and can be set up any time after a fleet is created.
{: note}

## Setting up logging for fleets
{: #fleet-log}

Logging for fleets is set up at the project level. After you perform these set up steps for a project, logging is available for all fleets in that project.

### 1. Make sure you have an existing Cloud Logs service instance
{: #log-instance}

You must have a Cloud Logs service instance that targets the region of the Code Engine project that your fleets run in. To check your existing Cloud Logs service instances, navigate to the [Logging routing page](https://cloud.ibm.com/observability/logs-routing/targets){: external} in the UI and identify the instance that targets the relevant region. If the region does not have a targeted logging instance, follow the UI prompts to set one. 

### 2. Set the permissions for the Cloud Logs instance
{: #log-perm}

Make sure you have a service ID and an API key that assign access to the Cloud Logs instance and set the required permissions.
1. [Create a service ID](/docs/account?topic=account-serviceids&interface=ui#create_serviceid). Then assign the service ID [an access policy](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console) that targets the Cloud Logs instance in your account. Assign this access policy the **Sender** service access level. 
2. [Create an API key for the service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#create_service_key). Save the API key in a secure location so you can reference it later. 

### 3. Get the private Ingress endpoint for the Cloud Logs instance
{: #log-ingress-endpoint}

Get the private Ingress endpoint for the Cloud Logs instance. 

1. Navigate to the [Logging instances page](https://cloud.ibm.com/observability/logging/51e1fabe-63dc-4a45-a161-83ddb2969a29/overview){: external} in the UI and click on the relevant instance.
2. Click **Endpoints**.
3. Find the private Ingress endpoint. Save this value in a secure location so you can reference it later.

### 4. Create a virtual private endpoint gateway that connects to the logging instance
{: #log-vpe}

Create a virtual private endpoint gateway that connects to the logging instance. This VPE gateway must be created in the VPC that your fleets run in. 

1. Navigate to the [VPE gateways page](https://cloud.ibm.com/infrastructure/network/endpointGateways){: external} in the console.
2. Click **Create**.
3. Select the location and region that your Cloud Logs instance exists in.
4. Select the VPC that your fleets run in.
5. Connect the service to your Cloud Logs instance.
    1. In the **Request connection to a service** section, select the option for **IBM Cloud Service**.
    2. Under **Cloud service offerings**, select **Cloud Logs**.
    3. Under **Cloud service regions**, select the region that your Cloud Logs instance exists in.
    4. From the table, select the relevant Cloud Logs instance to connect to the VPE. 
6. Click **Create**.

### 5. Create reserved IP addresses in the VPE gateway
{: #log-ip}

For each zone in the VPE, add a reserved IP address to one subnet. 

1. Navigate to the [VPE gateways page](https://cloud.ibm.com/infrastructure/network/endpointGateways){: external} in the console.
2. Click on the VPE you created in the previous step.
3. Click **Manage attached resources**.
4. Click **Reserve or bind IP**.
5. Follow the prompts to reserve an IP address for a subnet in one of the VPE zones.
6. Repeat this process for one subnet in each VPE zone. 


### 6. Add the logging values to the fleets default secret
{: #log-secret}

Add the required logging values to the fleets default secret.

1. In the console, go to the [Code Engine projects page](https://cloud.ibm.com/containers/serverless/projects){: external} and select the project that your fleets run in.
2. Click **Secrets and configmaps**.
3. Click on the `codeengine-fleet-defaults` secret.
   1. If it was not created before: click **Create**.
   2. Select **Generic secret**, then click **Next**.
   3. Name the secret `codeengine-fleet-defaults`. You must use this exact name and formatting.
4. Add the key-value pairs listed in the table below. Note that the `logging_sender_api_key` and `logging_ingress_endpoint` were saved in earlier steps.

| Key | Value |
| --- | ----- |
| `logging_ingress_endpoint` | The private Ingress endpoint for the Cloud Logs instance. This value is saved in a [previous step](#log-ingress-endpoint). |
| `logging_sender_api_key` | The API key for the service ID that targets the Cloud Logs instance. This value is saved in a [previous step](#log-perm). |
| `logging_ingress_port`| The port used to connect to the Cloud Logs instance. For private VPEs, specify `443`. |
| `logging_level_worker`| The level of details you want to include in your worker logs. Accepted levels include: `DEBUG`, `INFO`, `WARN`, and `ERROR`. Default level: `WARN`. |
| `logging_level_agent` | The level of details you want to include in your fleet agent logs. Accepted levels include: `DEBUG`, `INFO`, `WARN`, and `ERROR`.  Default level: `WARN`. |
{: caption="Logging key-value pairs for the fleets default secret." caption-side="bottom"}


### 7. View your fleets logs
{: #log-view}

Now that logging is set up for fleets in your Code Engine project, you can view your fleet logs. See [Viewing logs and monitoring data for fleets](/docs/codeengine?topic=codeengine-fleet-observability-view#log-view) for steps.

## Setting up monitoring for fleets
{: #fleet-monitor}

Monitoring for fleets is set up at the project level. After you perform these set up steps for a project, monitoring is available for all fleets in that project.

### 1. Make sure you have an existing Clouds Monitoring instance
{: #monitor-instance}

You must have a Cloud Monitoring instance in the same region of the Code Engine project that your fleet belongs to. To check your existing Cloud Monitoring service instances, navigate to the [Monitoring instances](https://cloud.ibm.com/observability/monitoring){: external} page in the UI and identify an instance in the relevant region. If you do not have a suitable instance, follow the UI prompts to create one. 

### 2. Get the monitoring agent key
{: #monitor-key}

Find the agent key for the monitoring instance. 

1. Navigate to the [Monitoring instances](https://cloud.ibm.com/observability/monitoring){: external} page in the UI and click on the relevant instance. On the instance details page, click **Actions** > **Manage key**, then click the option to view all keys in the dashboard. 
2. Click the agent key, which may have a format similar to `ab1c2345-****-678d9efgh012`. Then click the option to copy the full agent key. 
3. Save the agent key in a secure location where you can access it later. 

### 3. Create a virtual private endpoint gateway that connects to the monitoring instance
{: #monitor-vpe}

Create a virtual private endpoint gateway that connects to the monitoring instance. This VPE gateway must be created in the VPC that your fleets run in. 

1. Navigate to the [VPE gateways page](https://cloud.ibm.com/infrastructure/network/endpointGateways){: external} in the console.
2. Click **Create**.
3. Select the location and region that your Cloud Logs instance exists in.
4. Select the VPC that your fleets run in.
5. Connect the service to your Cloud Logs instance.
    1. In the **Request connection to a service** section, select the option for **IBM Cloud Service**.
    2. Under **Cloud service offerings**, select **Cloud Monitoring**.
    3. Under **Cloud service regions**, select the region that your Cloud Monitoring instance exists in.
    4. From the table, select the relevant Cloud Monitoring instance to connect to the VPE. 
6. Click **Create**.

### 4. Create reserved IP addresses in the VPE gateway
{: #monitor-ip}

For each zone in the VPE, add a reserved IP address to one subnet. 

1. Navigate to the [VPE gateways page](https://cloud.ibm.com/infrastructure/network/endpointGateways){: external} in the console.
2. Click on the VPE you created in the previous step.
3. Click **Manage attached resources**.
4. Click **Reserve or bind IP**.
5. Follow the prompts to reserve an IP address for a subnet in one of the VPE zones.
6. Repeat this process for one subnet in each VPE zone. 

### 5. Add monitoring values to the fleets default secret
{: #monitor-secret}

1. In the console, go to the [Code Engine projects page](https://cloud.ibm.com/containers/serverless/projects){: external} and select the project that your fleets run in.
2. Click **Secrets and configmaps**.
3. Click on the `codeengine-fleet-defaults` secret.
   1. If it was not created before: click **Create**.
   2. Select **Generic secret**, then click **Next**.
   3. Name the secret `codeengine-fleet-defaults`. You must use this exact name and formatting.
4. Add the key-value pairs listed in the table below. Note that the `monitoring_ingestion_key` was saved in an earlier step.

| Key | Value |
| --- | ----- |
| `monitoring_ingestion_region` | The region that the Cloud Monitoring instance exists in. Example: `au-syd`.  |
| `monitoring_ingestion_key` | The monitoring agent key. This value was found in a [previous step](#monitor-key). |
{: caption="Logging key-value pairs for the fleets default secret." caption-side="bottom"}

### 6. View your fleets data in the monitoring dashboard
{: #monitor-view}

Now that monitoring is set up for fleets in your Code Engine project, you can view your fleet monitoring data. See [Viewing logs and monitoring data for fleets](/docs/codeengine?topic=codeengine-fleet-observability-view#monitor-view) for steps.
