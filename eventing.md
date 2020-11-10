---

copyright:
  years: 2020
lastupdated: "2020-11-10"

keywords: event, code engine, ping, cos, Cloud object storage, object storage, trigger

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Eventing for {{site.data.keyword.codeenginefull_notm}}
{: #eventing}

You can extend the functionality of your applications by including messages (events) from event producers. Your application can then react to these events and perform actions based on them.
{: shortdesc}

While many event producers are available, {{site.data.keyword.codeengineshort}} includes two built-in commonly used ones: a [ping event producer](#eventing-ping) and [events from {{site.data.keyword.cos_full}}](#eventing-cos). The ping event producer generates an event at regular intervals, while the Object Storage producer monitors your buckets and send events based on changes to those buckets.

## Adding a ping event to your application
{: #eventing-ping}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

### Creating a ping event to an existing app
{: #eventing-ping-existing-app}

You can add a ping event to your application through the CLI by using the `subscription ping create` command. 

```
ibmcloud ce subscription ping create --name NAME --destination APPLICATION --schedule CRON
```
{: pre}
<table>
<caption><code>subscription ping create</code> components</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>subscription ping create</code></td>
<td>The command to create the ping event producer.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the Ping event source.
</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The addressable destination to where events are sent. This destination is a {{site.data.keyword.codeengineshort}} application.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Schedule specification in crontab format; for example, `*/2 * * * *` for every two minutes. By default, the Ping event is triggered every minute.</td>
</tr>
</tbody>
</table>

For example, to create a ping subscription that is called `mypingevent` that attaches to an existing app called `myapp` that fires every day at midnight,

```
ibmcloud ce subscription ping create --name mypingevent --destination myapp --schedule '0 0 * * *'
```
{: pre}

To verify that your ping subscription was successful, run `ibmcloud ce subscription ping get --name mypingevent`. 

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

Destination:  http://myapp.abcdabcd-abce.svc.cluster.local  
Schedule:     0 0 * * *  
Ready:        true   
Events:
Type    Reason                Age                    From                   Messages  
Normal  PingSourceReconciled  5m45s (x3 over 5m46s)  pingsource-controller  PingSource reconciled: "abcdefgh-abcd/mypingevent"  
Normal  FinalizerUpdate       5m45s                  pingsource-controller  Updated "mypingevent" finalizers 
```
{: screen}

From this output, you can see that the destination application is `http://myapp.74c96c5f-f73a.svc.cluster.local`, the schedule is `0 0 * * *` (midnight), and the Ready state is `true`.

### Creating a ping event for an app that doesn't exist yet
{: #eventing-ping-new-app}

You can also create a ping subscription to an application that is not yet created by using the `--force` option. Try creating a ping event for an app that doesn't exist yet, for example, called `myapp2`.

```
ibmcloud ce subscription ping create --name mypingevent2 --destination myapp2 --force
```
{: pre}

Run `subscription ping get`

```
ibmcloud ce subscription ping get --name mypingevent2
```
{: pre}

**Example output**

```
Getting Ping source 'mypingevent2'...
OK

Name:          mypingevent2  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13  
Age:           43s  
Created:       2020-10-14 14:00:15 -0500 CDT  

Destination:    
Schedule:     * * * * *  
Ready:        false  
Events:
Type     Reason           Age                 From                   Messages  
Normal   FinalizerUpdate  52s                 pingsource-controller  Updated "mypingevent2" finalizers  
```
{: screen}

Note that the destination field is empty and the Ready state is `false`. Now create an app called `myapp2` and run `subscription ping get` command again.

**Example output**

```
Name:          mypingevent2  
ID:            abcdefgh-abcd-abcd-abcd-93eea6632d59  
Project Name:  myproj  
Project ID:    abcdabcd-abce-abcd-abcd-876b6e70cd13 
Age:           2m35s  
Created:       2020-10-14 14:00:15 -0500 CDT  

Destination:  http://myapp2.abcdabcd-abce.svc.cluster.local  
Schedule:     * * * * *  
Ready:        true
Events:
Type     Reason                Age                  From                   Messages  
Normal   FinalizerUpdate       3m1s                 pingsource-controller  Updated "mypingevent2" finalizers  
```
{: screen}

This time, the destination lists `myapp2` and the Ready state is `true`.

## Deleting a ping event

You can delete a ping event by running the `subscription ping delete` command. For example,

```
ibmcloud ce subscription ping delete --name mypingevent2`
```
{: pre}

If you delete an application, the ping event is not deleted, but instead moves to ready state `false`. If you re-create the app (or another application with the same name), your event reconnects and the ready state is `true`.
{: note}

## Add an {{site.data.keyword.cos_full_notm}} event to your application
{: #eventing-cos}

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket.

**How does Cloud Object Storage eventing work?**

After you set up Cloud Object Storage subscription, your application can listen for changes to a bucket. When you create the subscription, you can specify a parameter that filters events based on the bucket change event type, such as `write` events,`delete` events, or `all` events. You can also filter the trigger events by object `prefix`, `suffix`, or both.

Each successful change to a bucket for which you have created a subscription received a separate event. As each object change in a bulk request is handled as a separate COS action, each of these changes also generates a separate event. For example, a bulk request to delete 200 objects results in 200 individual delete events and 200 event fires.

In order to use the {{site.data.keyword.cos_full_notm}} eventing,

* Your {{site.data.keyword.cos_short}} bucket must be a regional bucket and must be in the same region as your project. Cross-region and single-site buckets are not supported.
* You must [assign the Notifications Manager](#obstorage_auth) role to your project for your {{site.data.keyword.cos_short}}.

### 1. Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #obstorage_auth}

Before you can create a subscription to listen for bucket change events, you must assign the Notifications Manager role to {{site.data.keyword.codeengineshort}}. As a Notifications Manager, {{site.data.keyword.codeengineshort}} can view, modify, and delete notifications for an {{site.data.keyword.cos_short}} bucket. You can assign the Notifications Manager role from either the console or the CLI.
{: shortdesc}

Only account administrators can assign the Notifications Manager role.
{: note}

**What happens when I assign the Notifications Manager role?**

When you assign the Notifications Manager role to your project, you can then create event subscriptions for any regional buckets in your {{site.data.keyword.cos_short}} instance that are in the same region as your project.

#### Assigning the Notifications Manager role with the console

1. Navigate to the **Grant a Service Authorization** page in the [IAM dashboard](https://cloud.ibm.com/iam/authorizations/grant){: external}.
2. From **Source service**, select **Code engine**. Then, from **Source service instance**, select a {{site.data.keyword.codeengineshort}} project.
3. In **Target service**, select **Cloud Object Storage**, then from **Target service instance**, select your {{site.data.keyword.cos_full_notm}} instance.
4. Assign the **Notifications Manager** role and click **Authorize**.

#### Assigning the Notifications Manager role with the CLI

Copy the following command to assign the Notifications Manager role to your {{site.data.keyword.codeengineshort}} project.

Replace the `source_service_instance_name` variable with the name of your {{site.data.keyword.codeengineshort}} project.
Replace the `target_service_instance name` variable with the name of your {{site.data.keyword.cos_full_notm}} instance.

```
ibmcloud iam authorization-policy-create codeengine cloud-object-storage "Notifications Manager" --source-service-instance-name <source_service_instance_name> --target-service-instance-name <target_service_instance_name>
```
{: pre}

Verify that the Notifications Manager role is set.

```
ibmcloud iam authorization-policies
```
{: pre}

**Example output**

```                           
ID:                        58426335-e8e6-4228-8cd3-d371d3792f07   
Source service name:       codeengine   
Source service instance:   64c85c5f-f73a-4f08-9a3f-1be90471acea   
Target service name:       cloud-object-storage   
Target service instance:   All instances   
Roles:                     Notifications Manager 
```
{: screen}

### 2. Determining your event parameters
{: #obstorage_ev_param}

The {{site.data.keyword.cos_full_notm}} event subscription includes multiple parameters that can be set to filter which bucket change events recorded. For example, you can configure the trigger to fire on all bucket change events.
{: shortdesc}

| Parameter | Description |
| --- | --- |
| `bucket` | (Required) The name of your {{site.data.keyword.cos_full_notm}} bucket. This parameter is required to configure the `changes` event. The bucket must be in the same region as your project. The bucket must also be configured for regional resiliency. |
| `destination` | The addressable destination for events, usually an application name. |
| `prefix` | (Optional). The `prefix` parameter is the prefix of the {{site.data.keyword.cos_full_notm}} objects. You can specify this flag when you create your trigger to filter trigger events by object name prefix. |
| `suffix` | (Optional). The `suffix` parameter is the suffix of your {{site.data.keyword.cos_full_notm}} objects. You can specify this flag when you create your trigger to filter trigger events by object name suffix. |
| `event_type` | (Optional). The `event_types` is the type of bucket change that fires the event. You can specify `write` or `delete` or `all`. The default value is `all`. |
{: caption="{{site.data.keyword.cos_full_notm}} event parameters" caption-side="top"}

### 3. Creating an event subscription to listen for bucket changes
{: #obstorage_ev}

Set up your {{site.data.keyword.cos_full_notm}} event subscription by using the `subscription cos create` command.
{: shortdesc}

For example, create an {{site.data.keyword.cos_short}} subscription event that is called `mycosevent` for a bucket that is called `mybucket` that is attached to an app called `myapp`.

```
ibmcloud ce subscription cos create --name mycosevent --destination myapp --bucket mybucket
```
{: pre}

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
