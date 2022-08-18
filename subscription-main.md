---

copyright:
  years: 2022
lastupdated: "2022-08-09"

keywords: eventing, cron event, ping event, cos event, object storage event, event producers, subscribing, subscription, cloudevents

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with subscriptions
{: #subscribing-events}

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


{{site.data.keyword.codeengineshort}} supports the following types of event producers. 

* **Cron**: The cron event producer is based on cron and generates an event at regular intervals. Use a cron event producer when an action needs to be taken at well-defined intervals or at specific times.

* **{{site.data.keyword.cos_full_notm}}**: The {{site.data.keyword.cos_short}} event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform an action based on that change, perhaps consuming that new object.

* **Kafka**: The Kafka event producer watches for new messages to appear in a Kafka instance. When you create a {{site.data.keyword.codeengineshort}} Kafka subscription for a set of topics, your app or job receives a separate event for each new message that appears in one of the topics.

Apps and jobs can subscribe to multiple event producers, but only one app or job can receive events from each subscription. Note that subscriptions can affect how an application scales. For more information, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale). Subscriptions can also affect how many jobs are started. For example, if your job subscribes to delete changes on an {{site.data.keyword.cos_short}} bucket and that bucket is deleted, a job is run for each object that was in that bucket.
{: shortdesc}

For more information about subscription APIs, see [{{site.data.keyword.codeengineshort}} API reference - Subscription CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-subscription).

All events that are delivered to applications are received as HTTP messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event.

## Eventing metadata
{: #subscribing-events-cloudevents}

Events that are managed by {{site.data.keyword.codeengineshort}} when you create a subscription are modified so that they adhere to the
[`CloudEvents` specification](https://cloudevents.io){: external}. This specification defines a set of common attributes that can be included with each event to provide a common set of metadata. By looking at the metadata, you can quickly understand key pieces of the message without parsing and understanding the entirety of the event payload. For example, each event that is delivered to an application includes an HTTP header that is called `ce-type`, which indicates the semantic meaning (or "reason") for the event. An event from a database might include a `ce-type` value of `com.example.row.deleted`, indicating that the event was generated because a row was deleted in the database.

The following table lists some key common attributes. Each attribute indicates whether it is a *required* attribute on the incoming event or whether it is *optional*. 

| Header   | Description      | 
|----------|------------------|
| ID | This *required* attribute is a unique ID for the event. No two events from the same event producer are assigned the same value. | 
| Source | This *required* attribute specifies the context in which the event occurred. For example, for an object storage system, this value might be the bucket in which the object in question resides. |
| Specversion | This *required* attribute indicates the version of the CloudEvents specification that the event uses. |
| Type | This *required* attribute describes the type of the event. For example, the type of event might be that a resource was created or deleted. |
| Subject | This *optional* attribute indicates the resource about which the event is related. For example, in an object storage system, this value might be the object from the bucket that was modified. |
| Time | This *optional* attribute is the timestamp of when the occurrence happened. |
{: caption="Table 1. Common CloudEvent attributes" caption-side="top"}

For more information about the complete list of attributes, see the [`CloudEvents` specification](https://github.com/cloudevents/spec){: external}.

In {{site.data.keyword.codeengineshort}}, when events are delivered to applications, the `CloudEvent` attributes appear as HTTP headers, prefixed with `ce-`. When events are delivered to batch jobs, the attributes appear as environment variables, prefixed with `CE_` and the entire variable name is in uppercase.

### Example HTTP headers for an {{site.data.keyword.cos_full_notm}} event that is sent to an application
{: #subscribing-events-httpheaders-app}

```txt
ce-id: 3fb2c04e-a660-4640-8899-b82efb8169b6
ce-source: https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket
ce-specversion: 1.0
ce-subject: object-69-144
ce-time: 2021-08-17T20:22:02.917Z
ce-type: com.ibm.cloud.cos.document.delete
```
{: screen}

### Example environment variables for an {{site.data.keyword.cos_full_notm}} event that is sent to a job
{: #subscribing-events-envvars-job}

```txt
CE_DATA={"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Delete","format":"2.0","object_length":"4642","object_name":"Notes.rtf","request_id":"b59727ee-9c4e-446a-9261-5616f6d1283b","request_time":"2021-04-13T20:10:37.631Z"},"operation":"Object:Delete"}  
CE_ID=b59727ee-9c4e-446a-9261-5616f6d1283b  
CE_SOURCE=https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket  
CE_SPECVERSION=1.0  
CE_TIME=2021-08-17T20:22:02.917Z  
CE_TYPE=com.ibm.cloud.cos.document.delete  
```
{: screen}

## What happens when I create a subscription?
{: #subscribing-events-what-happens}

By default, the [**`subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create), [**`subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create)  and the [**`subscription kafka create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create) commands first check to see whether the destination application or job exists. If the destination check fails because the application or job does not exist in your project, the commands for the subscription create returns an error. If you want to create a subscription without first creating the application, use the `--force` option. By using the `--force` option, the command bypasses the destination check. Note that the `Ready` field of the subscription shows false until the destination application or job is created. Then, the subscription moves to a `Ready: true` state automatically.

After the subscription is created, the subscription is repeatedly polled for status to verify its readiness. This polling lasts for 15 seconds by default before it times out. You can change the amount of time before the command times out by using the `--wait-timeout` option. You can also bypass the status polling by setting the `--no-wait` option to `false`.

You can display the status of your subscription by using the [**`subscription cron get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-get), [**`subscription cos get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) or the [**`subscription kafka get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-get) CLI commands.



