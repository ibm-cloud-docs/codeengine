---
copyright:
  years: 2021
lastupdated: "2021-01-20"

keywords: events, serverless, codeengine, activity tracker

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



# Viewing {{site.data.keyword.cloudaccesstrailshort}} events
{: #activity_tracker}

You can view, manage, and audit user-initiated activities made in your {{site.data.keyword.codeenginefull}} service instance by using the {{site.data.keyword.at_full_notm}} service.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to follow regulatory audit requirements. You can also be alerted about actions as they happen. The events that are collected follow the Cloud Auditing Data Federation (CADF) standard. For more information, see the [Getting Started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started).


## List of events
{: #events}

The following list of {{site.data.keyword.codeenginefull}} events is sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

## List of events from IBM Cloud UI and CLI actions
The following events are generated when an initiator interacts with the {{site.data.keyword.codeenginefull_notm}} UI and CLI or with the `kubectl` and `kn` commands.

### project events

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
          <td>Get or list projects.</td>
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
          <td>Get a project `kubeconfig`.</td>
    </tr>
  </tbody>
</table>

### application events

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
      <td><code>codeengine.application.create</code></td>
          <td>Create an application in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.application.read</code></td>
          <td>Get an application.</td>
    </tr>
    <tr>
      <td><code>codeengine.application.list</code></td>
          <td>List applications.</td>
    </tr>
    <tr>
      <td><code>codeengine.application.update</code></td>
          <td>Update an application.</td>
    </tr>
    <tr>
      <td><code>codeengine.application.delete</code></td>
          <td>Delete one or more applications.</td>
    </tr>
  </tbody>
</table>

### configmap events
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
      <td><code>codeengine.configmap.create</code></td>
          <td>Create a configmap in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmap.read</code></td>
          <td>Get a configmap.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmap.list</code></td>
          <td>List configmaps.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmap.update</code></td>
          <td>Update a configmap.</td>
    </tr>
    <tr>
      <td><code>codeengine.configmap.delete</code></td>
          <td>Delete one or more configmaps.</td>
    </tr>
 </tbody>
</table>

### secret events
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
      <td><code>codeengine.secret.create</code></td>
          <td>Create a secret in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.secret.read</code></td>
          <td>Get a secret.</td>
    </tr>
    <tr>
      <td><code>codeengine.secret.list</code></td>
          <td>List secrets.</td>
    </tr>
    <tr>
      <td><code>codeengine.secret.update</code></td>
          <td>Update a secret.</td>
    </tr>
    <tr>
      <td><code>codeengine.secret.delete</code></td>
          <td>Delete one or more secrets.</td>
    </tr>
 </tbody>
</table>

### build and buildrun events
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
      <td><code>codeengine.build.create</code></td>
          <td>Create a build in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.build.read</code></td>
          <td>Get a build.</td>
    </tr>
    <tr>
      <td><code>codeengine.build.list</code></td>
          <td>List builds.</td>
    </tr>
    <tr>
      <td><code>codeengine.build.update</code></td>
          <td>Update a build.</td>
    </tr>            
    <tr>
      <td><code>codeengine.build.delete</code></td>
          <td>Delete one or more builds.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.create</code></td>
          <td>Submit a build run in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.read</code></td>
          <td>Get a build run.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.list</code></td>
          <td>List build runs.</td>
    </tr>
    <tr>
      <td><code>codeengine.buildrun.delete</code></td>
          <td>Delete one or more build runs.</td>
    </tr>
 </tbody>
</table>

### job and jobrun events
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
      <td><code>codeengine.job.create</code></td>
          <td>Create a job in project.</td>
    </tr>
	  <tr>
      <td><code>codeengine.job.read</code></td>
          <td>Get a job.</td>
    </tr>
	  <tr>
      <td><code>codeengine.job.list</code></td>
          <td>List jobs.</td>
    </tr>
    <tr>
      <td><code>codeengine.job.update</code></td>
          <td>Update a job.</td>
    </tr>
    <tr>
      <td><code>codeengine.job.delete</code></td>
          <td>Delete one or more jobs.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.create</code></td>
          <td>Submit a job run.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.read</code></td>
          <td>Get a job run.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.list</code></td>
          <td>List job runs.</td>
    </tr>
    <tr>
      <td><code>codeengine.jobrun.delete</code></td>
          <td>Delete one or more job runs.</td>
    </tr>
 </tbody>
</table>

### subscription events
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
      <td><code>codeengine.subscription.create</code></td>
          <td>Create an event source in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.read</code></td>
          <td>Get a event source.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.list</code></td>
          <td>List event sources.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.update</code></td>
          <td>Update an event source.</td>
    </tr>
    <tr>
      <td><code>codeengine.subscription.delete</code></td>
          <td>Delete one or more event sources.</td>
    </tr>
  </tbody>
</table>

## List of events from kubectl and kn commands
The following events are generated when an initiator interacts with the `kubectl` and `kn` commands.

### pods events

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
      <td><code>codeengine.pods.create</code></td>
          <td>Create a pod in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.pods.read</code></td>
          <td>Get a pod.</td>
    </tr>
    <tr>
      <td><code>codeengine.pods.list</code></td>
          <td>List pods.</td>
    </tr>
    <tr>
      <td><code>codeengine.pods.update</code></td>
          <td>Update a pod.</td>
    </tr>
    <tr>
      <td><code>codeengine.pods.delete</code></td>
          <td>Delete a pod.</td>
    </tr>
  </tbody>
</table>

### serviceaccounts events

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
      <td><code>codeengine.serviceaccounts.read</code></td>
          <td>Get a serviceaccount.</td>
    </tr>
    <tr>
      <td><code>codeengine.serviceaccounts.list</code></td>
          <td>List serviceaccounts.</td>
    </tr>
  </tbody>
</table>

### `events` events

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
      <td><code>codeengine.events.read</code></td>
          <td>Get a event.</td>
    </tr>
    <tr>
      <td><code>codeengine.events.list</code></td>
          <td>List events.</td>
    </tr>
  </tbody>
</table>


### resourcequotas events

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
      <td><code>codeengine.resourcequotas.read</code></td>
          <td>Get a resourcequota.</td>
    </tr>
    <tr>
      <td><code>codeengine.resourcequotas.list</code></td>
          <td>List resourcequotas.</td>
    </tr>
  </tbody>
</table>


### limitranges events

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
      <td><code>codeengine.limitranges.read</code></td>
          <td>Get a limitrange.</td>
    </tr>
    <tr>
      <td><code>codeengine.limitranges.list</code></td>
          <td>List limitranges.</td>
    </tr>
  </tbody>
</table>

### deployments events

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
      <td><code>codeengine.deployments.read</code></td>
          <td>Get a deployment.</td>
    </tr>
    <tr>
      <td><code>codeengine.deployments.list</code></td>
          <td>List deployments.</td>
    </tr>
  </tbody>
</table>


### servicebindings events

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
      <td><code>codeengine.servicebindings.create</code></td>
          <td>Create a servicebinding in project.</td>
    </tr>
    <tr>
      <td><code>codeengine.servicebindings.read</code></td>
          <td>Get a servicebinding.</td>
    </tr>
    <tr>
      <td><code>codeengine.servicebindings.list</code></td>
          <td>List servicebindings.</td>
    </tr>
    <tr>
      <td><code>codeengine.servicebindings.update</code></td>
          <td>Update a servicebinding.</td>
    </tr>
    <tr>
      <td><code>codeengine.servicebindings.delete</code></td>
          <td>Delete a servicebinding.</td>
    </tr>
  </tbody>
</table>

Note: 
- Update event does not include original value, it only includes new value provided in request body. To get original value, you can run read action before update action.
- `requestData` includes request body and verb of action.
- `responseData` includes response body of action.
- For some actions, for example `codeengine.pods.list` or `codeengine.pods.get` actions, the event length may exceeds 16K, so we will set `responseData` to `Information about the action is not included for performance and size reasons.` if message length exceeds 16K.


## Viewing events
{: #view}

{{site.data.keyword.codeenginefull_notm}} sends audit logs to the [{{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started) service of the same region as the {{site.data.keyword.codeenginefull_notm}} project. For example, audit logs of an {{site.data.keyword.codeenginefull_notm}} project in `us-south` are sent to a LogDNA instance in `us-south`. For more information about setting up {{site.data.keyword.at_full_notm}}, see [Provisioning an instance](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-provision).

## Analyzing events
{: #at_events_analyze}

After viewing events that are captured by {{site.data.keyword.at_full_notm}}, you can then analyze the events.
{: shortdesc}

**Identifying the {{site.data.keyword.codeengineshort}} project that generates the event**.

To identify the project for which the event was generated, look at the `target.id` field. You can use this field to filter events in LogDNA, for example, showing events for only a specific project. 

You can use the CLI to find details about your [project](/docs/codeengine?topic=codeengine-manage-project).

**Getting the unique ID of a request**

Each action that you perform on a {{site.data.keyword.codeengineshort}} project resource has a unique ID.

To find the unique ID of a request, look at the `correlationId` value that is set in the `correlationId` field.

**Getting information for failures**

All events that are issued for failed actions display `failure` in the `outcome` field, and in addition provide more details as part of the `reason` field. Note that the `reason.reasonForFailure` field might be especially helpful, as it contains details of the failure. 

**Custom views**

For more information about generating custom views by using event fields, see [Creating custom views in LogDNA](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-views).
