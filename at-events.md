---

copyright:
  years: 2020, 2020
lastupdated: "2020-11-4"

keywords: events, serverless, codeengine, activity tracker

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif

# Viewing {{site.data.keyword.cloudaccesstrailshort}} events
{: #activity_tracker}

You can view, manage, and audit user-initiated activities made in your {{site.data.keyword.codeenginefull}} service instance by using the {{site.data.keyword.at_full_notm}} service.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to follow regulatory audit requirements. You can also be alerted about actions as they happen. The events that are collected follow the Cloud Auditing Data Federation (CADF) standard. For more information, see the [Getting Started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).


## List of events
{: #events}

The following list of {{site.data.keyword.codeenginefull}} events is sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

<table>
  	<col style="width:40%">
	<col style="width:60%">
  <thead>
    <tr>
      <th>Action</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>codeengine.project.create</code></td>
            <td>Create a project.</td>
    </tr>
    <tr>
      <td><code>codeengine.project.read</code></td>
            <td>Get project information.</td>
    </tr>
	  <tr>
      <td><code>codeengine.project.update</code></td>
            <td>Update a project.</td>
    </tr>
    <tr>
      <td><code>codeengine.project.delete</code></td>
            <td>Delete a project.</td>
    </tr>
    <tr>
      <td><code>codeengine.projectconfig.read</code></td>
            <td>Get a project kubeconfig.</td>
    </tr>
    <tr>
      <td><code>codeengine.appliction.create</code></td>
            <td>Create an application.</td>
    </tr>
    <tr>
      <td><code>codeengine.appliction.read</code></td>
            <td>Get application information.</td>
    </tr>
	  <tr>
      <td><code>codeengine.appliction.update</code></td>
            <td>Update an application.</td>
    </tr>
        <tr>
      <td><code>codeengine.appliction.delete</code></td>
            <td>Delete an application.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmaps.create</code></td>
      <td>Create a configmap in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmaps.read</code></td>
      <td>Get configmap information.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmaps.update</code></td>
      <td>Update a configmap.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmaps.delete</code></td>
      <td>Delete a configmap.</td>
    </tr>
    <tr>
      <td><code>codeengine.secrets.create</code></td>
      <td>Create a secret in project.</td>
    </tr>
        <tr>
      <td><code>codeengine.secrets.read</code></td>
            <td>Get secret information.</td>
    </tr>
        <tr>
      <td><code>codeengine.secrets.update</code></td>
            <td>Update a secret.</td>
    </tr>
    <tr>
      <td><code>codeengine.secrets.delete</code></td>
            <td>Delete a secret.</td>
    </tr>
            <tr>
      <td><code>codeengine.build.create</code></td>
            <td>Create a build job in project.</td>
    </tr>
            <tr>
      <td><code>codeengine.build.read</code></td>
            <td>Get build job information.</td>
    </tr>
            <tr>
      <td><code>codeengine.build.update</code></td>
            <td>Update a build job.</td>
    </tr>            
    <tr>
      <td><code>codeengine.build.delete</code></td>
            <td>Delete a build job</td>
    </tr>
                <tr>
      <td><code>codeengine.buildrun.create</code></td>
            <td>Create a build run in project.</td>
    </tr>
                <tr>
      <td><code>codeengine.buildrun.read</code></td>
            <td>Get build run information.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.update</code></td>
            <td>Update a build run.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.delete</code></td>
            <td>Delete build run.</td>
    </tr>
     <tr>
      <td><code>codeengine.job.create</code></td>
            <td>Create a batch job in project.</td>
    </tr>
	   <tr>
      <td><code>codeengine.job.read</code></td>
            <td>Get batch job information.</td>
    </tr>
    <tr>
      <td><code>codeengine.job.update</code></td>
            <td>Update a batch job.</td>
    </tr>
    <tr>
      <td><code>codeengine.job.delete</code></td>
            <td>Delete build job.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.create</code></td>
            <td>Create a job run in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.read</code></td>
            <td>Get job run information.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.update</code></td>
            <td>Update a job run.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.delete</code></td>
            <td>Delete job run.</td>
    </tr>
    <tr>
      <td><code>codeengine.job.delete</code></td>
            <td>Delete build job.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.create</code></td>
            <td>Create an eventing subscription in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.read</code></td>
            <td>Get eventing subscription information.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.update</code></td>
            <td>Update an eventing subscription.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.delete</code></td>
            <td>Delete an eventing subscription.</td>
    </tr>
  </tbody>
</table>

Note: 
- Update event does not include initial value, it only includes new value.  
- {{site.data.keyword.codeenginefull}} also support `kubectl` command, so other kubernates resource type(such as pods, services, serviceaccounts etc.) events are also sent to {{site.data.keyword.at_full_notm}}. 

## Viewing events
{: #view}

{{site.data.keyword.codeenginefull_notm}} sends audit logs to the [{{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started) service of the same region as the {{site.data.keyword.codeenginefull_notm}} project. For example, audit logs of a {{site.data.keyword.codeenginefull_notm}} project in `us-south` are sent to a LogDNA instance in `us-south`. For more information about setting up {{site.data.keyword.at_full_notm}}, see [Provisioning an instance](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-provision).

## Analyzing events
{: #at_events_analyze}

After viewing events that are captured by {{site.data.keyword.at_full_notm}}, you can then analyze the events.
{: shortdesc}

**Identifying the {{site.data.keyword.codeengineshort}} project that generates the event**.

To identify the project for which the event was generated, look at the `target.id` field. You can use this field to filter events in LogDNA, for example, showing events for only a specific project. 

You can use the CLI to find details about your [project](/docs/codeengine?topic=codeengine-manage-project).

**Getting the unique ID of a request**

Each action that you perform on a {{site.data.keyword.codeengineshort}} project resource has a unique ID.

To find the unique ID of a request, look at the `transactionID` value that is set in the `transactionID` field.


**Getting information for failures**

All events that are issued for failed actions display `failure` in the `outcome` field, and in addition provide more details as part of the `reason` field. Note that the `reason.reasonForFailure` field might be especially helpful, as it contains details of the failure. 

**Custom views**

For more information about generating custom views by using event fields, see [Creating custom views in LogDNA](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-views).
