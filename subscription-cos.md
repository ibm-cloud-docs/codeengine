---

copyright:
  years: 2021
lastupdated: "2021-04-12"

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


# Working with the {{site.data.keyword.cos_full_notm}} event producer
{: #eventing-cosevent-producer}

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. When you create a subscription to a bucket, your app receives a separate event for each successful change to that bucket. You can subscribe to different events such as `write` events, `delete` events, or `all` events. You can create at most 100 {{site.data.keyword.cos_short}} subscriptions per project.
{: shortdesc}

In order to use the {{site.data.keyword.cos_full_notm}} subscription,

* Your {{site.data.keyword.cos_short}} bucket must be a regional bucket in the same region as your project. Cross-region and single-site buckets are not supported. For more information about setting up buckets, see [Getting started with {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
* You must [assign the Notifications Manager](#notify_mgr) role for your {{site.data.keyword.cos_short}} to your project.

## Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #notify_mgr}

Before you can create an {{site.data.keyword.cos_short}} subscription, you must assign the Notifications Manager role to {{site.data.keyword.codeengineshort}}. As a Notifications Manager, {{site.data.keyword.codeengineshort}} can view, modify, and delete notifications for an {{site.data.keyword.cos_short}} bucket.
{: shortdesc}

Only account administrators can assign the Notifications Manager role.
{: note}

When you assign the Notifications Manager role to your project, you can then create event subscriptions for any regional buckets in your {{site.data.keyword.cos_short}} instance that are in the same region as your project.

1. Navigate to the **Grant a Service Authorization** page in the [IAM dashboard](https://cloud.ibm.com/iam/authorizations/grant){: external}.
2. From **Source service**, select **Code engine**. 
3. Select **Services based on attributes** and **Source service instance**. Then, select a {{site.data.keyword.codeengineshort}} project.
4. In **Target service**, select **Cloud Object Storage**.
5. Select **Services based on attributes** and **Service instance**. Then, select your {{site.data.keyword.cos_full_notm}} instance.
6. Assign the **Notifications Manager** role and click **Authorize**.

You can also assign the Notifications Manager role to your project by using the [`ibmcloud iam authorization-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.
{: note}

## Creating an {{site.data.keyword.cos_full_notm}} subscription
{: #obstorage_ev}

Set up your {{site.data.keyword.cos_full_notm}} event subscription by using the `sub cos create` command. For a complete listing of options, see the [`ibmcloud ce sub cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

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
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           59s  
Created:       2021-03-01T20:08:36-06:00  

Destination:  App:my-application  
Bucket:       mybucket 
Event Type:   all  
Ready:        true  

Conditions:    
  Type            OK    Age  Reason  
  CosConfigured   true  55s    
  Ready           true  55s    
  ReadyForEvents  true  55s    
  SinkProvided    true  55s    

Events:        
  Type     Reason           Age      Source                Messages  
  Normal   FinalizerUpdate  61s      cossource-controller  Updated "mycosevent" finalizers 
```
{: screen}

Now every time that you change your bucket, your app receives notification. 

Want to try a tutorial? See [Subscribing to Object Storage events](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deleting a subscription
{: #subscription-delete}

You can delete a subscription by running the [`sub ping delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-delete) or the [`sub cos delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, delete a ping subscription that is called `mypingevent2`,

```
ibmcloud ce subscription ping delete --name mypingevent2
```
{: pre}

If you delete an app, the subscription is not deleted. Instead, it moves to ready state of `false` because the subscription depends on the availability of the application. If you re-create the app (or another app with the same name), your subscription reconnects and the Ready state is `true`.
{: note}

## HTTP headers and body information for events
{: #sub-header-body}

All events that are delivered to applications are received as HTTP messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

### Common HTTP header
{: #sub-common-header}

The following table shows the common HTTP headers that appear in each event that is delivered. The actual set of headers included in each event may include more options. For more information and more header file options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

```
ce-id:  c329ed76-5004-4383-a3cc-c7a9b82e3ac6
ce-source: /apis/v1/namespaces/<namespace>/pingsources/myping
ce-specversion: 1.0
ce-time: 2021-02-26T19:19:00.497637287Z
ce-type: dev.knative.sources.ping
```
{: screen}

The following table describes the common headers.

| Header   | Description      | 
|----------|------------------|
| `ce-id` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `ce-source` | A URI-reference that indicates where this event originated from within the event producer. |
| `ce-specversion` | The version of the Cloud Events spec. This value is always `1.0`. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For example, did a `write` or `delete` action occur. |
{: caption="Table 1. Header files for events" caption-side="top"}

### {{site.data.keyword.cos_full_notm}} header and body information
{: #sub-cos-header}

The following header and body information is specific to {{site.data.keyword.cos_full_notm}} events.

**Header**

- `ce-source` is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object. 
- `ce-type` is  `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`.

**HTTP body**

The HTTP body for {{site.data.keyword.cos_full_notm}} is in the following format,

```
{
  "bucket": "cetestbucket2",
  "endpoint": "",
  "key": "CodeEngine Splash.svg",
  "notification": {
    "bucket_name": "cetestbucket2",
    "content_type": "image/svg+xml",
    "event_type": "Object:Write",
    "format": "2.0",
    "object_etag": "f3a9dbde30fdf48abc23e5f8b485d6e5",
    "object_length": "1064391",
    "object_name": "CodeEngine Splash.svg",
    "request_id": "67a2048a-abcd-abcd-9e0c-968744094b85",
    "request_time": "2021-02-26T19:18:30.963Z"
  },
  "operation": "Object:Write"
}
```
{: screen}

| Body field | Description      | 
|------------|------------------|
| `bucket` | The bucket name for the object that is related to the event. | 
| `endpont` | This value is always an empty string. |
| `key` | The name of the object in the bucket. |
| `operaton` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.bucket_name` | The bucket name for the object that is related to the event.  |
| `Notification.content_type` | The MIME type of the object, for example, `text/html`. |
| `Notification.event_type` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.format` | This value is always `2.0`. |
| `Notification.object_etag` | A unique value that changes each time the object is modified. This value does not display for an `Object:Delete` operation. |
| `Notification.object_length` | The size of the object, in bytes. |
| `Notification.request_id` | The unique ID that is related to the object change. |
| `Notification.request_time` | The time that the object change occurred. |
{: caption="Table 2. Body fields for {{site.data.keyword.cos_full_notm}}" caption-side="top"}
