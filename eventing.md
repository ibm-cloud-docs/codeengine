---

copyright:
  years: 2021
lastupdated: "2021-01-26"

keywords: eventing for code engine, ping event in code engine, cos event in code engine, object storage event in code engine, accessing event producers from code engine apps

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


# Subscribing to event producers
{: #subscribing-events}

In distributed environments, oftentimes, you want your applications to react to messages (events) that are generated from other components, usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications can subscribe to event producers so that events that are of interest can be delivered as HTTP requests to those applications.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports two types of event producers. First, is a ping (cron) event producer that generates an event at regular intervals. This type of event producer is often used when an action needs to be taken at well-defined intervals or specific times. Secondly, is an {{site.data.keyword.cos_full_notm}} event producer. This type of event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform some action based on that change, perhaps consuming that new object.

Apps can subscribe to multiple event producers, but only one app can receive events from each subscription.

## Working with ping
{: #subscribe-ping}

The ping (cron) event producer generates an event at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals.
{: shortdesc}

Ping uses a standard crontab to specify interval details, in the format `* * * * *`, which stands for minute, hour, day of month, month, and day of week, respectively. For example, to schedule an event for midnight, specify `0 0 * * *`.  To schedule an event for every Friday at midnight, specify `0 0 * * FRI`.

For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

### Subscribing to ping events
{: #eventing-ping-existing-app}

When you subscribe to a ping event, you must provide a destination (app) for the subscription as well as a schedule. If you do not provide a schedule, then the default of `*/2 * * * *` (every 2 minutes) is used.

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

You can connect your application to the ping event source producer with the CLI by using the [`sub ping create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-create) command. 

```
ibmcloud ce sub ping create --name NAME --destination APPLICATION --schedule CRON
```
{: pre}

For example, to create a ping subscription that sends an event to an app that is called `myapp` every day at midnight,

```
ibmcloud ce sub ping create --name mypingevent --destination myapp --schedule '0 0 * * *'
```
{: pre}

You must wrap the schedule value in single quotes to ensure that it is treated as a single string.
{: note}

The following table summarizes the options that are used with the `sub ping create` command in this example. For more information about the command and its options, see the [`ibmcloud ce subscription ping create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-create) command.

<table>
<caption><code>subscription ping create</code> options</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's options</th>
</thead>
<tbody>
<tr>
<td><code>subscription ping create</code></td>
<td>The command to create the ping subscription.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the ping event source.
</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} application in the current project that receives the events from the event producer.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Indicates how often an event is generated. The format of the schedule follows the [`crontab`](http://crontab.org/){: external} format; for example, `*/2 * * * *`  generates an event every 2 minutes. If a schedule is not specified then by default an event will be generated ever minute.</td>
</tr>
</tbody>
</table>

To verify that your ping subscription was successfully created, run `ibmcloud ce sub ping get --name mypingevent`. 

**Example output**

```
Getting Ping source 'mypingevent'...
OK

Name:          mypingevent  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13 
Age:           2m21s  
Created:       2020-10-14 13:55:20 -0500 CDT  

Destination:  app:myapp 
Schedule:     0 0 * * *  
Ready:        true   
Events:
Type    Reason                Age                    From                   Messages  
Normal  PingSourceReconciled  5m45s (x3 over 5m46s)  pingsource-controller  PingSource reconciled: "abcdefgh-abcd/mypingevent"  
Normal  FinalizerUpdate       5m45s                  pingsource-controller  Updated "mypingevent" finalizers 
```
{: screen}

From this output, you can see that the destination application is `http://myapp.74c96c5f-f73a.svc.cluster.local`, the schedule is `0 0 * * *` (midnight), and the Ready state is `true`.

You can also create a ping subscription to an application that is not yet created by using the `--force` option.  Your ping subscription displays `false` as a Ready state until the application is created.
{: note}

## Working with {{site.data.keyword.cos_full_notm}} event producer

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. For each successful change to a bucket for which you have created a subscription, a separate event is received. You can subscribe to different events such as `write` events,`delete` events, or `all` events.
{: shortdesc}

In order to use the {{site.data.keyword.cos_full_notm}} subscription,

* Your {{site.data.keyword.cos_short}} bucket must be a regional bucket and must be in the same region as your project. Cross-region and single-site buckets are not supported. For more information about setting up buckets, see [Getting started with {{site.data.keyword.cos_short}}])docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
* You must [assign the Notifications Manager](#notify_mgr) role to your project for your {{site.data.keyword.cos_short}}.

### Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #notify_mgr}

Before you can create a {{site.data.keyword.cos_short}} subscription, you must assign the Notifications Manager role to {{site.data.keyword.codeengineshort}}. As a Notifications Manager, {{site.data.keyword.codeengineshort}} can view, modify, and delete notifications for an {{site.data.keyword.cos_short}} bucket.
{: shortdesc}

Only account administrators can assign the Notifications Manager role.
{: note}

When you assign the Notifications Manager role to your project, you can then create event subscriptions for any regional buckets in your {{site.data.keyword.cos_short}} instance that are in the same region as your project.

1. Navigate to the **Grant a Service Authorization** page in the [IAM dashboard](https://cloud.ibm.com/iam/authorizations/grant){: external}.
2. From **Source service**, select **Code engine**. Then, from **Source service instance**, select a {{site.data.keyword.codeengineshort}} project.
3. In **Target service**, select **Cloud Object Storage**, then from **Target service instance**, select your {{site.data.keyword.cos_full_notm}} instance.
4. Assign the **Notifications Manager** role and click **Authorize**.

You can also assign the Notifications Manager role to your project by using the [`ibmcloud iam authorization-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command. 

### Creating a {{site.data.keyword.cos_full_notm}} subscription
{: #obstorage_ev}

Set up your {{site.data.keyword.cos_full_notm}} event subscription by using the `sub cos create` command. For a complete listing of options, see the [`ibmcloud ce sub cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

For example, create a {{site.data.keyword.cos_short}} subscription event that is called `mycosevent` for a bucket that is called `mybucket` that is subscribed to an app called `myapp`. 

```
ibmcloud ce sub cos create --name mycosevent --destination myapp --bucket mybucket
```
{: pre}

The following table summarizes the options that are used with the `sub cos create` command in this example. For more information about the command and its options, see the [`ibmcloud ce sub cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.

<table>
<caption><code>subscription cos create</code> options</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's options</th>
</thead>
<tbody>
<tr>
<td><code>subscription cos create</code></td>
<td>The command to create the {{site.data.keyword.cos_short}} subscription.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the {{site.data.keyword.cos_short}} subscription.
</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} app in the current project that receives the events from the event producer.</td>
</tr>
<tr>
<td><code>--bucket</code></td>
<td>The name of your {{site.data.keyword.cos_full_notm}} bucket. The bucket must be in the same region as your project.</td>
</tr>
</tbody>
</table>

After your subscription creates, run the `subscription cos get` command.

```
ibmcloud ce subscription cos get --name mycosevent
```
{: pre}

**Example output**

```
Getting COS source 'mycosevent'...
OK

Name:          mycosevent  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13  
Age:           23s  
Created:       2020-10-14 14:14:01 -0500 CDT  

Destination:  http://myapp.abcdabcd-abce.svc.cluster.local  
Bucket:       mybucket  
EventType:    all  
Ready:        true  
Events:
Type     Reason           Age                From                  Messages  
Normal   FinalizerUpdate  30s                cossource-controller  Updated "mycosevent" finalizers  
```
{: screen}

Now every time that you change your bucket, your app receives notification.

## Deleting a ping event

You can delete a subscription by running the [`sub ping delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-delete) or the [`sub cos delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, delete a ping subscription that is called `mypingevent2`,

```
ibmcloud ce subscription ping delete --name mypingevent2`
```
{: pre}

If you delete an app, the subscription is not deleted, but instead moves to ready state of `false`. If you re-create the app (or another app with the same name), your subscription reconnects and the Ready state is `true`.
{: note}
