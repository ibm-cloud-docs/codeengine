---

copyright:
  years: 2021
lastupdated: "2021-04-14"

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

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. When you create a subscription to a bucket, your app or job receives a separate event for each successful change to that bucket. You can subscribe to different events such as `write` events, `delete` events, or `all` events. You can create at most 100 {{site.data.keyword.cos_short}} subscriptions per project.
{: shortdesc}

By default, the [`subscription cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command first checks to see whether the destination application exists. If the destination check fails because the app name that you provided does not exist in your project, the `subscription cos create` command returns an error. If you want to create a subscription without first creating the application, use the `--force` option. By using the `--force` option, the command bypasses the destination check. Note that the `Ready` field of the subscription shows false until the destination app is created. Then, the subscription moves to a `Ready: true` state automatically.

After the subscription is created, but before the `subscription cos create` command reports any results, the `subscription cos create` command repeatedly polls the subscription for its status to verify its readiness. This continuous polling for status lasts for 15 seconds by default before it times out. If the subscription status returns as `Ready:true`, it reports success, otherwise it reports an error. You can change the amount of time that the `subscription ping create` command waits before it times out by using the `--wait-timeout` option. You can also bypass the status polling by setting the `--no-wait` option to `false`.

## Set up the {{site.data.keyword.cos_full_notm}} event producer
{: #setup-cosevent-producer}

Your {{site.data.keyword.cos_short}} bucket must be a regional bucket in the same region as your project. Cross-region and single-site buckets are not supported. For more information about setting up buckets, see [Getting started with {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

To see the buckets and their associated regions by using the CLI,

1. Download the {{site.data.keyword.cos_short}} plug-in CLI.
   
   ```
   ibmcloud plugin install cloud-object-storage
   ```
   {: pre}

2. Get the CRN (Cloud Resource Name) number from your {{site.data.keyword.cos_short}} instance. The CRN number identifies which {{site.data.keyword.cos_short}} instance that you want to use. The CRN number is the value of the `ID` field in the output of the `ibmcloud resource service-instance COS_INSTANCE_NAME` command. 

   ```
   ibmcloud resource service-instance my-cloud-object-storage
   ```
   {: pre}
   
   **Example output**
   
   ```
   Name:                  my-cloud-object-storage  
   ID:                    crn:v1:bluemix:public:cloud-object-storage:global:a/ab9d57f699655f028880abcd2ccdb524:123b456b-abcd-4a73-abcd-77c68bfeabcd::   
   GUID:                  123b456b-abcd-4a73-abcd-77c68bfeabcd   
   Location:              global   
   Service Name:          cloud-object-storage   
   Service Plan Name:     lite   
   Resource Group Name:   Default   
   State:                 active   
   Type:                  service_instance   
   Sub Type:                 
   Created at:            2020-10-14T19:09:22Z   
   Created by:            <user@us.ibm.com>  
   Updated at:            2020-10-14T19:09:22Z   
   ```
   {: screen}
   
   If you do not know your {{site.data.keyword.cos_short}} instance name, run `ibmcloud resource service-instances --service-name cloud-object-storage` to see a list of {{site.data.keyword.cos_short}} instances.
   
   If you do not have an {{site.data.keyword.cos_short}} instance, [create one](/docs/cloud-object-storage).
   
3. Configure your {{site.data.keyword.cos_short}} CRN that you found with the previous step to specify an {{site.data.keyword.cos_short}} instance to work with. Be sure to copy the entire number, starting with `crn:`.

   ```
   ibmcloud cos config crn --crn CRN_NUMBER
   ```
   {: pre}
   
   **Example output**
   
   ```
   Saving new Service Instance ID...
   OK
   Successfully stored your service instance ID.
   ```
   {: screen}

4. Identify a bucket to subscribe to. To see a list of buckets that are associated with your {{site.data.keyword.cos_short}} instance,

   ```
   ibmcloud cos buckets
   ```
   {: pre}

5. Identify the location and plan of the {{site.data.keyword.cos_short}} bucket,
   
   ```
   ibmcloud cos bucket-location-get --bucket BUCKET_NAME
   ```
   {: pre}
   
   **Example output**
   
   ```
   Details about bucket mybucket:
   Region: 
   Class: Standard
   ```
   {: screen}

Note that if you have a global bucket, the value for `Region` is not specified. 

## Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #notify_mgr}

Before you can create an {{site.data.keyword.cos_short}} subscription, you must assign the Notifications Manager role to {{site.data.keyword.codeengineshort}}. As a Notifications Manager, {{site.data.keyword.codeengineshort}} can view, modify, and delete notifications for an {{site.data.keyword.cos_short}} bucket.
{: shortdesc}

Only account administrators can assign the Notifications Manager role.
{: note}

When you assign the Notifications Manager role to your project, you can then create event subscriptions for any regional buckets in your {{site.data.keyword.cos_short}} instance that are in the same region as your project.

1. Navigate to the **Grant a Service Authorization** page in the [IAM dashboard](https://cloud.ibm.com/iam/authorizations/grant){: external}.
2. From **Source service**, select **Code engine**. 
3. Select **Resources based on selected attributes** and **Source service instance**. Then, select a {{site.data.keyword.codeengineshort}} project.
4. In **Target service**, select **Cloud Object Storage**.
5. Select **Services based on attributes** and **Service instance**. Then, select your {{site.data.keyword.cos_full_notm}} instance.
6. Assign the **Notifications Manager** role and click **Authorize**.

You can also assign the Notifications Manager role to your project by using the [`ibmcloud iam authorization-policy-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.
{: note}

## Creating an {{site.data.keyword.cos_full_notm}} subscription for an application
{: #obstorage_ev}

When you subscribe to an {{site.data.keyword.cos_full_notm}} event, you must provide a destination (app) and a destination type for the subscription.  Events are sent to applications as HTTP POST requests. For more information, see [HTTP headers and body information for events](#sub-header-body).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create an application.

  For example, [create an application](/docs/codeengine?topic=codeengine-cli#cli-application-create) called `myapp` that uses the `cos-listen` image from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
  
  ```
  ibmcloud ce application create -name myapp --image ibmcom/cos-listen
  ```
  {: pre}

You can connect your application to the {{site.data.keyword.cos_full_notm}} event producer by using the `sub cos create` command. For a complete listing of options, see the [`ibmcloud ce sub cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

```
ibmcloud ce sub cos create --name mycosevent --destination-type app --destination myapp --bucket mybucket
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
<td><code>--destination-type</code></td>
<td>The type of the `destination`. Valid values are `app` and `job`. The default value is `app`.</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} app or job in the current project that receives the events from the event producer.</td>
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

Destination:  App:myapp  
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

### Viewing event information for an application
{: #viewing-info-app}

If your application prints information to log files, as the `ping` application does, then use the [app logs](/docs/codeengine?topic=codeengine-cli#cli-application-logs) CLI command to view the information that was sent. 

Before you can view event information for your application, you must first create an {{site.data.keyword.cos_short}} event.  Make a change to your bucket.

To view the logs for the application that you created in the previous example, 

```
ibmcloud ce application logs --application myapp 
```
{: pre}

**Example output**

```
Getting logs for all instances of application 'myapp'...
OK

myapp-a2mvv-1-deployment-d97dcd6cf-zc9lg/user-container:    
Listening on port 8080  
2021-04-13 19:43:45 - Received:  
  
Body: {"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Write","format":"2.0","object_etag":"2944035e54ee1bdc423848c8eaf05e86","object_length":"4642","object_name":"NOtes.rtf","request_id":"6abc7123-382d-4115-98e8-7568b2cc03f8","request_time":"2021-04-13T19:43:36.610Z"},"operation":"Object:Write"} 
```
{: screen}

Note that log information lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Creating an {{site.data.keyword.cos_full_notm}} subscription for a job
{: #obstorage_ev}

When you subscribe to an {{site.data.keyword.cos_full_notm}} event, you must provide a destination (job) and a destination type for the subscription.  Events are sent to jobs as environment variables. For more information, see [Environment variables for events](#sub-envir-variables).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create a job.

  For example, [create a job](/docs/codeengine?topic=codeengine-cli#cli-application-create) called `myjob` that uses the `codeengine` image from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
  
  ```
  ibmcloud ce job create -name myjob --image ibmcom/codeengine
  ```
  {: pre}

You can connect your job to the {{site.data.keyword.cos_full_notm}} event producer by using the `sub cos create` command. For a complete listing of options, see the [`ibmcloud ce sub cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

```
ibmcloud ce sub cos create --name mycosevent --destination-type job --destination myjob --bucket mybucket
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
<td><code>--destination-type</code></td>
<td>The type of the `destination`. Valid values are `app` and `job`. The default value is `app`.</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} app or job in the current project that receives the events from the event producer.</td>
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

Destination Type:  job  
Destination:       myjob  
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

Now every time that you change your bucket, your job receives notification. 

Want to try a tutorial? See [Subscribing to Object Storage events](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Viewing event information for a job
{: #viewing-info-job}

If your job prints information to log files, as the `ping` job does, then use the [job logs](/docs/codeengine?topic=codeengine-cli#cli-job-logs) CLI command to view the information that was sent.

Before you can view event information for your job, you must first create an {{site.data.keyword.cos_short}} event. Make a change to your bucket.

To find the job run for the job in the previous example, 

```
ibmcloud ce jobrun list
```
{: pre}

**Example output**

```
Listing job runs...
OK

Name         Failed  Pending  Requested  Running  Succeeded  Unknown  Age  
myjob-pnz6m  0       0        0          0        1          0        39s  
```
{: screen}

View the logs for the job run by specifying the jobrun name.

```
ibmcloud ce jobrun logs --jobrun myjob-pnz6m
```
{: pre}

**Example output**

```
Getting logs for all instances of job run 'myjob-pnz6m'...
Getting jobrun 'myjob-pnz6m'...
Getting instances of jobrun 'myjob-pnz6m'...
OK

myjob-pnz6m-0-0/myjob:    
Hello from helloworld! I'm a batch job! Index: 0  
  
Hello World from:  
. ___  __  ____  ____  
./ __)/  \(    \(  __)  
( (__(  O )) D ( ) _)  
.\___)\__/(____/(____)  
.____  __ _   ___  __  __ _  ____  
(  __)(  ( \ / __)(  )(  ( \(  __)  
.) _) /    /( (_ \ )( /    / ) _)  
(____)\_)__) \___/(__)\_)__)(____)  
  
Some Env Vars:  
--------------  
CE_DATA={"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Delete","format":"2.0","object_length":"4642","object_name":"Notes.rtf","request_id":"b59727ee-9c4e-446a-9261-5616f6d1283b","request_time":"2021-04-13T20:10:37.631Z"},"operation":"Object:Delete"}  
CE_ID=b59727ee-9c4e-446a-9261-5616f6d1283b  
CE_SOURCE=https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket  
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T20:10:37.631Z  
CE_TYPE=com.ibm.cloud.cos.document.delete  
CONTENT_TYPE=application/json  
HOME=/root  
HOSTNAME=myjob-pnz6m-0-0  
JOB_INDEX=0  
KUBERNETES_PORT=tcp://172.21.0.1:443  
KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443  
KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1  
KUBERNETES_PORT_443_TCP_PORT=443  
KUBERNETES_PORT_443_TCP_PROTO=tcp  
KUBERNETES_SERVICE_HOST=172.21.0.1  
KUBERNETES_SERVICE_PORT=443  
KUBERNETES_SERVICE_PORT_HTTPS=443  
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin  
PWD=/  
SHLVL=1 
```
{: screen}

Note that log information lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
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
  "bucket": "mybucket",
  "endpoint": "",
  "key": "CodeEngine Splash.svg",
  "notification": {
    "bucket_name": "mybucket",
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

The following table describes the body field.

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

## Environment variables for events
{: #sub-envir-variables}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

### Common environment variables
{: #sub-envir-variables-common}

Each event contains some common environment variables that appear every time the event is delivered. The actual set of variables in each event may include more options. For more information and more environment variable options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

``` 
CE_ID=c329ed76-5004-4383-a3cc-c7a9b82e3ac6 
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T20:10:37.631Z  
```
{: screen}

The following table describes the common environment variable values.

| Variable   | Description      | 
|----------|------------------|
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `CE_SPECVERSION` | The version of the Cloud Events spec. This value is always `1.0`. |
| `CE_TIME` | The time that the event was generated. |
{: caption="Table 3. Environment variables for events" caption-side="top"}

### {{site.data.keyword.cos_full_notm}} environment variables
{: #sub-cos-environment-variable}

The following environment variable values are specific to {{site.data.keyword.cos_full_notm}} events.

- `CE_SOURCE` is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object. 
- `CE_TYPE` is  `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`.
- `CE_DATA`:

```
{
"bucket":"mybucket",
"endpoint":"",
"key":"Notes.rtf",
"notification"{
  "bucket_name":"mybucket",
  "content_type":"text/rtf",
  "event_type":"Object:Delete",
  "format":"2.0",
  "object_length":"4642",
  "object_name":"Notes.rtf",
  "request_id":"b59727ee-9c4e-446a-9261-5616f6d1283b",
  "request_time":"2021-04-13T20:10:37.631Z"
},
"operation":"Object:Delete"}  
```
{: screen}

The following table describes the `CE_DATA` environment variable.

| Variable | Description      | 
|------------|------------------|
| `bucket` | The bucket name for the object that is related to the event. | 
| `endpont` | This value is always an empty string. |
| `key` | The name of the object in the bucket. |
| `operaton` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.bucket_name` | The bucket name for the object that is related to the event.  |
| `Notification.content_type` | The MIME type of the object, for example, `text/rtf`. |
| `Notification.event_type` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.format` | This value is always `2.0`. |
| `Notification.object_etag` | A unique value that changes each time the object is modified. This value does not display for an `Object:Delete` operation. |
| `Notification.object_length` | The size of the object, in bytes. |
| `Notification.request_id` | The unique ID that is related to the object change. |
| `Notification.request_time` | The time that the object change occurred. |
{: caption="Table 4. Environment variables for {{site.data.keyword.cos_full_notm}}" caption-side="top"}
