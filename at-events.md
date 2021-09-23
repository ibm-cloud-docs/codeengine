---
copyright:
  years: 2020, 2021
lastupdated: "2021-09-17"

keywords: events, serverless, code engine, activity tracker, analyzing events

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# Auditing events for {{site.data.keyword.codeengineshort}}
{: #at_events}

You can view, manage, and audit user-initiated activities made in your {{site.data.keyword.codeenginefull}} service instance by using the {{site.data.keyword.at_full_notm}} service.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to follow regulatory audit requirements. You can also be alerted about actions as they happen. The events that are collected follow the Cloud Auditing Data Federation (CADF) standard. For more information, see the [Getting Started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## List of events from {{site.data.keyword.cloud_notm}} console and CLI actions
{: #list-events-cli-console}

The following events are generated when an initiator interacts with the {{site.data.keyword.codeenginefull_notm}} console and CLI or with the **`kubectl`** and **`kn`** commands. These events are sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

### Project events
{: #project-events}

These actions generate project events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.project.create` | Create a project. | 
| `codeengine.project.read` | Get information about or list projects. |
| `codeengine.project.update` | Update a project. |
| `codeengine.project.delete` | Delete a project. |
| `codeengine.projectconfig.read` | Get a project `kubeconfig` file. |
{: caption="Table 1. Actions that generate project events" caption-side="top"}

### Application events
{: #app-events}

These actions generate application events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.application.create` | Create an application in a project. | 
| `codeengine.application.read` | Get information about an application. | 
| `codeengine.application.list` | List applications. | 
| `codeengine.application.update` | Update an application. | 
| `codeengine.application.delete` | Delete one or more applications. | 
{: caption="Table 2. Actions that generate application events" caption-side="top"}

### Configmap events
{: #configmap-events}

These actions generate configmap events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.configmap.create` | Create a configmap in a project. | 
| `codeengine.configmap.read` | Get information about a configmap. | 
| `codeengine.configmap.list` | List configmaps. | 
| `codeengine.configmap.update` | Update a configmap. | 
| `codeengine.configmap.delete` | Delete one or more configmaps. |
{: caption="Table 3. Actions that generate configmap events" caption-side="top"}

### Secret events
{: #secret-events}

These actions generate secret events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.secret.create` | Create a secret in a project. | 
| `codeengine.secret.read` | Get information about a secret. | 
| `codeengine.secret.list` | List secrets. | 
| `codeengine.secret.update` | Update a secret. | 
| `codeengine.secret.delete` | Delete one or more secrets. |
{: caption="Table 4. Actions that generate secret events" caption-side="top"}

### Build and build run events
{: #build-events}

These actions generate build and build run events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.build.create` | Create a build in a project. | 
| `codeengine.build.read` | Get information about a build. | 
| `codeengine.build.list` | List builds. | 
| `codeengine.build.update` | Update a build. | 
| `codeengine.build.delete` | Delete one or more builds. | 
| `codeengine.buildrun.create` | Submit a build run in a project. | 
| `codeengine.buildrun.read` | Get information about a build run. | 
| `codeengine.buildrun.list` | List build runs. | 
| `codeengine.buildrun.delete` | Delete one or more build runs. |
{: caption="Table 5. Actions that generate build and build run events" caption-side="top"}

### Job and job run events
{: #job-events}

These actions generate job and job run events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.job.create` | Create a job in a project. | 
| `codeengine.job.read` | Get information about a job. | 
| `codeengine.job.list` | List jobs. |
| `codeengine.job.update` | Update a job. | 
| `codeengine.job.delete` | Delete one or more jobs. | 
| `codeengine.jobrun.create` | Submit a job run. | 
| `codeengine.jobrun.read` | Get information about a job run. | 
| `codeengine.jobrun.list` | List job runs. | 
| `codeengine.jobrun.delete` | Delete one or more job runs. |
{: caption="Table 6. Actions that generate job and job run events" caption-side="top"}

### Subscription events
{: #subscription-events}

These actions generate subscription events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.subscription.create` | Create subscription in a project. | 
| `codeengine.subscription.read` | Get information about a subscription. | 
| `codeengine.subscription.list` | List subscriptions. | 
| `codeengine.subscription.update` | Update a subscription. | 
| `codeengine.subscription.delete` | Delete one or more subscriptions. |
{: caption="Table 7. Actions that generate subscription events" caption-side="top"}

## List of events from **`kubectl`** and **`kn`** commands
{: #kubect1-events}
The following events are generated when an initiator interacts with the **`kubectl`** and **`kn`** commands. These events are sent to {{site.data.keyword.at_full_notm}}.

### Pod events
{: #kubect1-pod-events}

These actions generate pod events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.pods.create` | Create a pod in a project. | 
| `codeengine.pods.read` | Get information about a pod. | 
| `codeengine.pods.list` | List pods. |
| `codeengine.pods.update` | Update a pod. |
| `codeengine.pods.delete` | Delete a pod. |
{: caption="Table 8. Actions that generate pod events" caption-side="top"}

### Service account events
{: #kubect1-serviceaccount-events}

These actions generate service account events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.serviceaccounts.read` | Get information about a service account. | 
| `codeengine.serviceaccounts.list` | List service accounts. | 
{: caption="Table 9. Actions that generate service account events" caption-side="top"}

### Event events
{: #kubect1-event-events}

These actions generate event-type events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.events.read` | Get information about an event. | 
| `codeengine.events.list` | List events. | 
{: caption="Table 10. Actions that generate event-type events" caption-side="top"}

### Resource quota events
{: #kubect1-resourcequote-events}

These actions generate resource quota events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.resourcequotas.read` | Get information about a resource quota. | 
| `codeengine.resourcequotas.list` | List resource quotas. | 
{: caption="Table 11. Actions that generate resource quota events" caption-side="top"}

### Limit range events
{: #kubect1-limitrange-events}

These actions generate limit range events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.limitranges.read` | Get information about a limit range. | 
| `codeengine.limitranges.list` | List limit ranges. | 
{: caption="Table 12. Actions that generate limit range events" caption-side="top"}

### Deployment events
{: #kubect1-deployment-events}

These actions generate deployment events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.deployments.read` | Get information about a deployment. | 
| `codeengine.deployments.list` | List deployments. | 
{: caption="Table 13. Actions that generate deployment events" caption-side="top"}

### Service binding events
{: #kubect1-servicebinding-events}

These actions generate service bind events.

| Action             | Description      | 
|--------------------|------------------|
| `codeengine.servicebindings.create` | Create a service binding in a project. | 
| `codeengine.servicebindings.read` | Get information about a service binding. | 
| `codeengine.servicebindings.list` | List service bindings. |
| `codeengine.servicebindings.update` | Update a service binding. |
| `codeengine.servicebindings.delete` | Delete a service binding. |
{: caption="Table 14. Actions that generate service bind events" caption-side="top"}

Note: 
- The update event does not include the original value; it includes only the new value that is provided in request body. To find the original value, you can run read action before you run the update action.
- The `requestData` field includes request body and verb of action.
- The `responseData` field includes response body of action.
- For some actions, for example `codeengine.pods.list` or `codeengine.pods.get` actions, the event length might exceed 16 K. If this event length occurs,  the `responseData` field is set to `Information about the action is not included for performance and size reasons.`

## Viewing events
{: #view}

{{site.data.keyword.codeenginefull_notm}} sends audit logs to the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started) service in the same region as the {{site.data.keyword.codeenginefull_notm}} project. For example, audit logs in an {{site.data.keyword.codeenginefull_notm}} project in `us-south` are sent to a logging instance in `us-south`. For more information about setting up {{site.data.keyword.at_full_notm}}, see [Provisioning an instance](/docs/activity-tracker?topic=activity-tracker-provision).

## Analyzing events
{: #at_events_analyze}

After you view events that are captured by {{site.data.keyword.at_full_notm}}, you can then analyze the events.
{: shortdesc}

**Identifying the {{site.data.keyword.codeengineshort}} project that generates the event**.

To identify the project for which the event was generated, look at the `target.id` field. You can use this field to filter events in {{site.data.keyword.loganalysisshort_notm}}, for example, showing events for only a specific project. 

You can use the CLI to find details about your [project](/docs/codeengine?topic=codeengine-manage-project).

**Getting the unique ID of a request**

Each action that you perform on a {{site.data.keyword.codeengineshort}} project resource has a unique ID.

To find the unique ID of a request, look at the `correlationId` value that is set in the `correlationId` field.

**Getting information for failures**

All events that are issued for failed actions display `failure` in the `outcome` field, and in addition provide more details as part of the `reason` field. Note that the `reason.reasonForFailure` field might be especially helpful, as it contains details of the failure. 

**Custom views**

For more information about generating custom views by using event fields, see [Creating custom views in {{site.data.keyword.loganalysislong_notm}}](/docs/activity-tracker?topic=activity-tracker-views).


