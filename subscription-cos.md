---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-03"

keywords: cos event, object storage event, event producers, code engine, events, header, environment variables, subscription, subscribing

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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

The {{site.data.keyword.cos_short}} subscription event producer is not available in the `ca-tor` region. See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions) for more information about regions where {{site.data.keyword.codeengineshort}} is available.
{: important} 

## Set up the {{site.data.keyword.cos_full_notm}} event producer
{: #setup-cosevent-producer}

Your {{site.data.keyword.cos_short}} bucket must be a regional bucket located in the same region as your project. Cross-region and single-site buckets are not supported. For more information about setting up buckets, see [Getting started with {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

To see the buckets and their associated regions by using the CLI,

1. Download the {{site.data.keyword.cos_short}} plug-in CLI.

    ```
    ibmcloud plugin install cloud-object-storage
    ```
    {: pre}

2. Get the CRN (Cloud Resource Name) number from your {{site.data.keyword.cos_short}} instance. The CRN number identifies which {{site.data.keyword.cos_short}} instance that you want to use. The CRN number is the value of the `ID` field in the output of the **`ibmcloud resource service-instance COS_INSTANCE_NAME`** command. 

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

4. Identify a bucket to subscribe to. To see a list of buckets that are associated with your {{site.data.keyword.cos_short}} instance.

    ```
    ibmcloud cos buckets
    ```
    {: pre}

5. Identify the location and plan of the {{site.data.keyword.cos_short}} bucket.

    ```
    ibmcloud cos bucket-location-get --bucket BUCKET_NAME
    ```
    {: pre}

    **Example output**

    ```
    Details about bucket mybucket:
    Region: us-south
    Class: Standard
    ```
    {: screen}

Note that if you have a global bucket, the value for `Region` is not specified. 

## Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #notify-mgr-cos}

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

You can also assign the Notifications Manager role to your project by using the [**`ibmcloud iam authorization-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.
{: note}

## Creating an {{site.data.keyword.cos_full_notm}} subscription for an application
{: #obstorage_ev_app}

By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /event`, the event is sent to `https://<base application URL>/events`.

Events are sent to applications as HTTP POST requests. For more information, see [HTTP headers and body information for events](#sub-header-body-cos).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create an application.

    For example, [create an application that is called `myapp` that uses the [`cos-listen` image](https://hub.docker.com/r/ibmcom/cos-listen){: external}. This image is built from `cos-listen.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cos-event){: external}.

    ```
    ibmcloud ce application create -name myapp --image ibmcom/cos-listen
    ```
    {: pre}

You can connect your application to the {{site.data.keyword.cos_full_notm}} event producer by using the **`subscription cos create`** command. For a complete listing of options, see the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

```
ibmcloud ce subscription cos create --name mycosevent --destination-type app --destination myapp --bucket mybucket
```
{: pre}

The following table summarizes the options that are used with the **`subscription cos create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.

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
<td>The type of the <code>destination</code>, in this case, <code>app</code>.</td>
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

After your subscription creates, run the **`subscription cos get`** command.

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

If your application prints information to log files, as the `cos-listen` application does, then use the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) CLI command to view the information that was sent. 

Before you can view event information for your application, you must first create an {{site.data.keyword.cos_short}} event. Make a change to your bucket.

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

### {{site.data.keyword.cos_full_notm}} header and body information for events delivered to applications
{: #sub-header-body-cos}

All events that are delivered to applications are received as HTTP messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` specification](https://cloudevents.io){: external}.
{: shortdesc}

**Headers**

The following table describes the headers for {{site.data.keyword.cos_short}} events.

| Header   | Description      | 
|----------|------------------|
| `ce-id` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `ce-source` | A URI-reference that indicates where this event originated from within the event producer. For {{site.data.keyword.cos_short}} events, this is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object.  |
| `ce-specversion` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `ce-subject` | Indicates the resource about which the event is related. For {{site.data.keyword.cos_short}} events, this is the name of the object (or key) that was acted upon. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For {{site.data.keyword.cos_short}} events, this is `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`. When an event create or update is occurs, a `write` action is used for `ce-type`.  |
{: caption="Table 1. Header files for events" caption-side="top"}

**Example** 

```
ce-id:  3fb2c04e-a660-4640-8899-b82efb8169b6
ce-source: https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket
ce-specversion: 1.0
ce-subject: object-69-144
ce-time: 2021-08-17T20:22:02.917Z
ce-type: com.ibm.cloud.cos.document.delete
```
{: screen}

**HTTP body**

The HTTP body for an {{site.data.keyword.cos_full_notm}} event is in the following format,

```
{
  "bucket": "mybucket",
  "endpoint": "",
  "key": "object-69-144",
  "notification": {
    "bucket_name": "mybucket",
    "content_type": "image/svg+xml",
    "event_type": "Object:Delete",
    "format": "2.0",
    "object_etag": "f3a9dbde30fdf48abc23e5f8b485d6e5",
    "object_length": "1064391",
    "object_name": "object-69-144",
    "request_id": "67a2048a-abcd-abcd-9e0c-968744094b85",
    "request_time": "2021-08-17T20:22:02.917Z"
  },
  "operation": "Object:Delete"
}
```
{: screen}

The following table describes the body field.

| Body field | Description      | 
|------------|------------------|
| `bucket` | The bucket name for the object that is related to the event. | 
| `endpoint` | This value is always an empty string. |
| `key` | The name of the object in the bucket. |
| `operation` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.bucket_name` | The bucket name for the object that is related to the event.  |
| `Notification.content_type` | The MIME type of the object, for example, `text/html`. |
| `Notification.event_type` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.format` | This value is always `2.0`. |
| `Notification.object_etag` | A unique value that changes each time that the object is modified. This value does not display for an `Object:Delete` operation. |
| `Notification.object_length` | The size of the object, in bytes. |
| `Notification.request_id` | The unique ID that is related to the object change. |
| `Notification.request_time` | The time that the object change occurred. |
{: caption="Table 2. Body fields for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

## Creating an {{site.data.keyword.cos_full_notm}} subscription for a job
{: #obstorage_ev_job}

Events are sent to jobs as environment variables. For more information about the environment variables that are sent by {{site.data.keyword.cos_full_notm}}, see [Environment variables for events](#sub-envir-variables-cos).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create a job.

    For example, [create a job that is called `myjob` that uses the [`codeengine` image](https://hub.docker.com/r/ibmcom/codeengine){: external}. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.

    ```
    ibmcloud ce job create -name myjob --image ibmcom/codeengine
    ```
    {: pre}

You can connect your job to the {{site.data.keyword.cos_full_notm}} event producer by using the **`subscription cos create`** command. For a complete listing of options, see the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

```
ibmcloud ce subscription cos create --name mycosevent --destination-type job --destination myjob --bucket mybucket
```
{: pre}

The following table summarizes the options that are used with the **`subscription cos create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.

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
<td>The type of the <code>destination</code>, in this case, <code>job</code>.</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} job in the current project that receives the events from the event producer.</td>
</tr>
<tr>
<td><code>--bucket</code></td>
<td>The name of your {{site.data.keyword.cos_full_notm}} bucket. The bucket must be in the same region as your project.</td>
</tr>
</tbody>
</table>

After your subscription creates, run the **`subscription cos get`** command.

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

Job runs that are created by subscriptions are deleted after 10 minutes.
{: note}

Want to try a tutorial? See [Subscribing to Object Storage events](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Viewing event information for a job
{: #viewing-info-job}

If your job prints information to log files, as the `cos-listen` job does, then use the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) CLI command to view the information that was sent.

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

### Environment variables for events delivered to jobs
{: #sub-envir-variables-cos}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

Each event contains some common environment variables that appear every time the event is delivered to a job. The actual set of variables in each event can include more options. For more information and more environment variable options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

The following table describes the environment variables that are specific to {{site.data.keyword.cos_full_notm}} events.

| Variable   | Description      | 
|----------|------------------|
| `CE_DATA` | The data (body) for the event. See [`CE_DATA` for {{site.data.keyword.cos_short}} events](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#subcos-envvar-cedata). |
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `CE_SOURCE` | A URI-reference that indicates where this event originated from within the event producer. For {{site.data.keyword.cos_short}} events, this is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object. |
| `CE_SPECVERSION` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `CE_TIME` | The time that the event was generated. |
| `CE_TYPE` | The type of the event. For {{site.data.keyword.cos_short}} events, this is `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`. |
{: caption="Table 3. Environment variables for events" caption-side="top"}

#### `CE_DATA` environment variable 
{: #subcos-envvar-cedata}

Notice that the following example for `CE_DATA` is formatted for readability. 

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

The following table describes the `CE_DATA` environment attribute. 

| Attribute | Description      | 
|------------|------------------|
| `bucket` | The bucket name for the object that is related to the event. | 
| `endpont` | This value is always an empty string. |
| `key` | The name of the object in the bucket. |
| `operaton` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.bucket_name` | The bucket name for the object that is related to the event.  |
| `Notification.content_type` | The MIME type of the object, for example, `text/rtf`. |
| `Notification.event_type` | The event type or operation, either type `Object:Write` or `Object:Delete`. Create or upload events are tagged as `Object:Write` operations. |
| `Notification.format` | This value is always `2.0`. |
| `Notification.object_etag` | A unique value that changes each time that the object is modified. This value does not display for an `Object:Delete` operation. |
| `Notification.object_length` | The size of the object, in bytes. |
| `Notification.request_id` | The unique ID that is related to the object change. |
| `Notification.request_time` | The time that the object change occurred. |
{: caption="Table 4. Environment variables for {{site.data.keyword.cos_full_notm}}" caption-side="top"}

**Example**

``` 
CE_DATA={"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Delete","format":"2.0","object_length":"4642","object_name":"Notes.rtf","request_id":"b59727ee-9c4e-446a-9261-5616f6d1283b","request_time":"2021-04-13T20:10:37.631Z"},"operation":"Object:Delete"}  
CE_ID=b59727ee-9c4e-446a-9261-5616f6d1283b  
CE_SOURCE=https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket  
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T20:10:37.631Z  
CE_TYPE=com.ibm.cloud.cos.document.delete 
```
{: screen}


## Defining `CloudEvent` attributes
{: #additional-attributes-cos}

When you create a subscription, you can define additional `CloudEvent` attributes to be included in any events that are generated. These attributes appear similar to any other `CloudEvent` attribute in the event delivery. If you choose to specify the name of an existing `CloudEvent` attribute, then it overrides the original value that was included in the event.

To define addition attributes, use the `--extension` options with the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) CLI command.

For more information, see [Can I use other `CloudEvents` specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)

## Deleting a subscription
{: #subscription-delete-cos}

You can delete a subscription by running the [**`ibmcloud ce subscription cos delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, delete a cos subscription that is called `mycosevent2`,

```
ibmcloud ce subscription cos delete --name mycosevent2
```
{: pre}

If you delete an application, the subscription is not deleted. Instead, it moves to ready state of `false` because the subscription depends on the availability of the application. If you re-create the application (or another application with the same name), your subscription reconnects and the Ready state is `true`.
{: note}



