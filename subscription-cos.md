---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-16"

keywords: cos event, object storage event, event producers, code engine, events, header, environment variables, subscription, subscribing

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with the {{site.data.keyword.cos_full_notm}} event producer
{: #eventing-cosevent-producer}

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. When you create a subscription to a bucket, your app or job receives a separate event for each successful change to that bucket. You can subscribe to different events such as `write` events, `delete` events, or `all` events. You can create at most 100 {{site.data.keyword.cos_short}} subscriptions per project.
{: shortdesc}


## Setting up the {{site.data.keyword.cos_full_notm}} event producer
{: #setup-cosevent-producer}

To get started, you must [create an {{site.data.keyword.cos_full_notm}} service instance](/docs/cloud-object-storage?topic=cloud-object-storage-gs-dev#gs-dev-provision) and [create a regional bucket](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets) in one of the supported regions for {{site.data.keyword.codeengineshort}}. 

Your {{site.data.keyword.cos_short}} bucket must be a regional bucket that is located in the same region as your {{site.data.keyword.codeengineshort}} project. Cross-region and single-site buckets are not supported. For more information about setting up the {{site.data.keyword.cos_full_notm}} event producer, see [Getting started with {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

If your application or job that is receiving events wants to talk to a service by using private networking and the service has both `private` and `direct` endpoints (such as {{site.data.keyword.cos_full_notm}}), then the `direct` endpoints must be used.
{: important}



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
5. Select **Resources based on selected attributes** and **Service instance**. Then, select your {{site.data.keyword.cos_full_notm}} instance.
6. Assign the **Notifications Manager** role and click **Authorize**.

You can also assign the Notifications Manager role to your project by using the [**`ibmcloud iam authorization-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.
{: note}

## Subscribing to {{site.data.keyword.cos_full_notm}} events for an application
{: #obstorage_ev_app}

You can work with {{site.data.keyword.cos_full_notm}} subscriptions from the console or with the CLI so events are sent to a {{site.data.keyword.codeengineshort}} application.
{: shortdesc}

By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /event`, the event is sent to `https://<base application URL>/events`.

Events are sent to applications as HTTP POST requests. For more information, see [HTTP headers and body information for events](#sub-header-body-cos).

### Subscribing to {{site.data.keyword.cos_full_notm}} events for an application from the console
{: #eventing-cos-app-ui}

You can create and update {{site.data.keyword.cos_full_notm}} event subscriptions for an application from the console.
{: shortdesc}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an application](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console). For example, create an application that is called `myapp` that uses the `icr.io/codeengine/cos-event` image. This image is built from `cos-listen.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cos-event){: external}.

Complete the following steps to create and update an {{site.data.keyword.cos_full_notm}} event subscription for an application from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create an event subscription page, complete the following steps. 
   1. For **Event type**, select the Cloud Object Storage tile. Click **Next**. 
   2. For **General**, provide a name for the {{site.data.keyword.cos_short}} subscription, for example, `mycos`. You can optionally provide event attributes. Note that if the {{site.data.keyword.cos_short}} event consumer is an application, event attributes are available as HTTP headers. If the event consumer is a job, event attributes are available as environment variables. Click **Next** to proceed. 
   3. For **Bucket event details**, select or type the name of an existing {{site.data.keyword.cos_short}} bucket. Specify the types of changes for your object and optionally provide an object name prefix or suffix to filter objects in the bucket that to trigger events for the subscription. Click **Next** to proceed. 
   4. For **Event consumer**, specify the application to receive events. Notice that you can choose from a list of defined applications and jobs. For this example, use the `myapp` application that references the `icr.io/codeengine/cos-listen` image. If your app does not exist, you can provide the name of your application and [create your application](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) after you create the {{site.data.keyword.cos_short}} subscription. For applications only, you can optionally specify a path. By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by specifying a path. For example, if your subscription path specifies `/events`, the events are sent to `https://<base application URL>/events`. Click **Next** to proceed.
   5. For **Summary**, review the settings for your {{site.data.keyword.cos_short}} event subscription and make changes if needed. When ready, click **Create** to create the {{site.data.keyword.cos_short}} subscription. 

5. Now that your {{site.data.keyword.cos_short}} subscription is created, go to the Event subscriptions page to [view a listing of defined subscriptions](#view-eventing-cos-app-ui). 
6. To update a subscription, navigate to your {{site.data.keyword.cos_short}} subscription page. From the Event subscriptions page, click the name of the subscription that you want to update. 
7. From your {{site.data.keyword.cos_short}} subscription page, let's change the type of object change to only `delete` object changes. From the **Bucket event details** tab, select only the `delete` type of object change. Click **Save** to save your changes. 
8. Because the `myapp` application references the sample `cos-listen` application, which prints information to log files, you can view the logs. After an object is deleted from the bucket, you can see an event for the delete in the app logs. See [Viewing application logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui). 

After you define an {{site.data.keyword.cos_full_notm}} event subscription that references a specific bucket, you cannot update this subscription to use a different bucket. You must create a new subscription to reference the bucket that you want.
{: important}

### Subscribing to {{site.data.keyword.cos_full_notm}} events for an application with the CLI
{: #eventing-cos-app-cli}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create an application. For example, create an application that is called `myapp` that uses the `icr.io/codeengine/cos-listen` image. This image is built from `cos-listen.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cos-event){: external}. For example,

    ```txt
    ibmcloud ce application create --name myapp --image icr.io/codeengine/cos-listen
    ```
    {: pre}

1. Connect your application to the {{site.data.keyword.cos_full_notm}} event producer by using the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command. For example, 

    ```txt
    ibmcloud ce subscription cos create --name mycosevent --destination-type app --destination myapp --bucket mybucket
    ```
    {: pre}

2. After your subscription creates, run the **`subscription cos get`** command for details about your subscription.

    ```txt
    ibmcloud ce subscription cos get --name mycosevent
    ```
    {: pre}

    Example output

    ```txt
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

### Viewing event information for an application from the console
{: #view-eventing-cos-app-ui}

To view information about your event subscriptions, 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions. 

If your application prints information to log files, as the sample `cos-listen` application does, then view the log files for your event consumer application. See [Viewing application logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui).


### Viewing event information for an application with the CLI
{: #view-eventing-cos-app-cli}

If your application prints information to log files, as the `cos-listen` application does, then use the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) CLI command to view the information that was sent. 

Before you can view event information for your application, you must first create an {{site.data.keyword.cos_short}} event. Make a change to your bucket.

To view the logs for the application that you created in the previous example, 

```txt
ibmcloud ce application logs --application myapp 
```
{: pre}

Example output

```txt
Getting logs for all instances of application 'myapp'...
OK

myapp-a2mvv-1-deployment-d97dcd6cf-zc9lg/user-container:    
Listening on port 8080  
2021-04-13 19:43:45 - Received:  

Body: {"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Write","format":"2.0","object_etag":"2944035e54ee1bdc423848c8eaf05e86","object_length":"4642","object_name":"NOtes.rtf","request_id":"6abc7123-382d-4115-98e8-7568b2cc03f8","request_time":"2021-04-13T19:43:36.610Z"},"operation":"Object:Write"} 
```
{: screen}

Note that log information for apps lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### {{site.data.keyword.cos_full_notm}} header and body information for events delivered to applications
{: #sub-header-body-cos}

All events that are delivered to applications are received as HTTP messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` specification](https://cloudevents.io){: external}.
{: shortdesc}

#### Headers
{: #sub-header-cos-headers}

The following table describes the headers for {{site.data.keyword.cos_short}} events.

| Header   | Description      | 
|----------|------------------|
| `ce-id` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `ce-source` | A URI-reference that indicates where this event originated from within the event producer. For {{site.data.keyword.cos_short}} events, this value is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object.  |
| `ce-specversion` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `ce-subject` | Indicates the resource about which the event is related. For {{site.data.keyword.cos_short}} events, this is the name of the object (or key) that was acted upon. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For {{site.data.keyword.cos_short}} events, this is `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`. When a create or update for an event occurs, a `write` action is used for `ce-type`.  |
{: caption="Table 1. Header files for events" caption-side="top"}

Example

```txt
ce-id:  3fb2c04e-a660-4640-8899-b82efb8169b6
ce-source: https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket
ce-specversion: 1.0
ce-subject: object-69-144
ce-time: 2021-08-17T20:22:02.917Z
ce-type: com.ibm.cloud.cos.document.delete
```
{: screen}

#### HTTP body
{: #sub-header-cos-httpbody}

The HTTP body for an {{site.data.keyword.cos_full_notm}} event is in the following format,

```txt
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

## Subscribing to {{site.data.keyword.cos_full_notm}} events for a job
{: #obstorage_ev_job}

You can work with {{site.data.keyword.cos_full_notm}} subscriptions from the console or with the CLI so events are sent to a {{site.data.keyword.codeengineshort}} job.
{: shortdesc}

When you create an event subscription for a job, a job run is created for each event that is triggered, and this job run has the environment variables that are related to the job. For more information about the environment variables that are sent by {{site.data.keyword.cos_full_notm}}, see [Environment variables for events](#sub-envir-variables-cos). 

### Subscribing to {{site.data.keyword.cos_full_notm}} events for a job from the console
{: #eventing-cos-job-ui}

You can create and update {{site.data.keyword.cos_full_notm}} event subscriptions for a job from the console.
{: shortdesc}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create a job](/docs/codeengine?topic=codeengine-create-job#create-job-ui). For example, create a job that is called `myjob` that uses the `icr.io/codeengine/codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.


Complete the following steps to create and update an {{site.data.keyword.cos_full_notm}} event subscription for a job from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create an event subscription page, complete the following steps. 
   1. For **Event type**, select the Cloud Object Storage tile. Click **Next**. 
   2. For **General**, provide a name for the {{site.data.keyword.cos_short}} subscription, for example, `mycos-job`. You can optionally provide event attributes. When the event consumer is a job, event attributes are available as environment variables. Click **Next** to proceed. 
   3. For **Bucket event details**, select or type the name of an existing {{site.data.keyword.cos_short}} bucket. Specify the types of changes for your object and optionally provide an object name prefix or suffix to filter objects in the bucket to trigger events for the subscription. Click **Next** to proceed. 
   4. For **Event consumer**, specify the job to receive events. Notice that you can choose from a list of defined jobs. For this example, use the `myjob` job that references the `icr.io/codeengine/codeengine` image. If your job does not exist, you can specify the name of your job and [create your job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) after you create the {{site.data.keyword.cos_short}} subscription. Click **Next** to proceed.
   5. For **Summary**, review the settings for your {{site.data.keyword.cos_short}} event subscription and make changes if needed. When ready, click **Create** to create the {{site.data.keyword.cos_short}} subscription. 

5. Now that your {{site.data.keyword.cos_short}} subscription is created, go to the Event subscriptions page to [view a listing of defined subscriptions](#view-eventing-cos-job-ui). 
6. To update a subscription, navigate to your {{site.data.keyword.cos_short}} subscription page. From the Event subscriptions page, click the name of the subscription that you want to update. 
7. From your {{site.data.keyword.cos_short}} subscription page, let's change the type of object change to only `delete` object changes. From the **Bucket event details** tab, only select the `delete` type of object change. Click **Save** to save your changes. 
8. Because the `myjob` job references the sample `icr.io/codeengine/codeengine` job, which prints information to log files, you can view the logs. After an object is deleted from the bucket, you can see an event for the delete in the logs for the job run. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui).

Job runs that are created by subscriptions are deleted after 10 minutes.
{: note}

After you define an {{site.data.keyword.cos_full_notm}} event subscription that references a specific bucket, you cannot update this subscription to use a different bucket. You must create a new subscription to reference the bucket that you want.
{: important}

### Subscribing to {{site.data.keyword.cos_full_notm}} events for a job with the CLI
{: #eventing-cos-job-cli}

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create a job. For example, create a job that is called `myjob` that uses the `icr.io/codeengine/codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}. 

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine
    ```
    {: pre}

1. Connect your job to the {{site.data.keyword.cos_full_notm}} event producer by using the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.

    ```txt
    ibmcloud ce subscription cos create --name mycosevent --destination-type job --destination myjob --bucket mybucket
    ```
    {: pre}


2. After your subscription creates, run the **`subscription cos get`** command for details about your subscription.

    ```txt
    ibmcloud ce subscription cos get --name mycosevent
    ```
    {: pre}

    Example output

    ```txt
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

### Viewing event information for a job from the console
{: #view-eventing-cos-job-ui}

To view information about your event subscriptions, 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions. 

If your job prints information to log files, as the sample `codeengine` job does, then view the log files for your event consumer application. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblog-cli).

### Viewing event information for a job with the CLI
{: #view-eventing-cos-job-cli}

If your job prints information to log files, as the `codeengine` job does, then use the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) CLI command to view the information that was sent. 

Before you can view event information for your job, you must first create an {{site.data.keyword.cos_short}} event. Make a change to your bucket.

To find the job run for the job in the previous example, 

```txt
ibmcloud ce jobrun list
```
{: pre}

Example output

```txt
Listing job runs...
OK

Name         Failed  Pending  Requested  Running  Succeeded  Unknown  Age  
myjob-pnz6m  0       0        0          0        1          0        39s  
```
{: screen}

View the logs for the job run by specifying the job run name.

```txt
ibmcloud ce jobrun logs --jobrun myjob-pnz6m
```
{: pre}

Example output

```txt
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

Note that log information for job runs lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Environment variables for events delivered to jobs
{: #sub-envir-variables-cos}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

Each event contains some common environment variables that appear every time that the event is delivered to a job. The actual set of variables in each event can include more options. For more information and more environment variable options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

The following table describes the environment variables that are specific to {{site.data.keyword.cos_full_notm}} events.

| Variable   | Description      | 
|----------|------------------|
| `CE_DATA` | The data (body) for the event. See [`CE_DATA` for {{site.data.keyword.cos_short}} events](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#subcos-envvar-cedata). |
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `CE_SOURCE` | A URI-reference that indicates where this event originated from within the event producer. For {{site.data.keyword.cos_short}} events, this value is `https://cloud.ibm.com/catalog/services/cloud-object-storage/[BUCKET_NAME]`  where `[BUCKET_NAME]` is the name of the bucket that contains the object. |
| `CE_SPECVERSION` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `CE_TIME` | The time that the event was generated. |
| `CE_TYPE` | The type of the event. For {{site.data.keyword.cos_short}} events, this is `com.ibm.cloud.cos.document.[ACTION]` where `[ACTION]` is either `write` or `delete`. |
{: caption="Table 3. Environment variables for events" caption-side="top"}

#### `CE_DATA` environment variable 
{: #subcos-envvar-cedata}

Notice that the following example for `CE_DATA` is formatted for readability. 

```txt
{
"bucket":"mybucket",
"endpoint":"",
"key":"Notes.rtf",
"notification": {
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

Example output 

```txt 
CE_DATA={"bucket":"mybucket","endpoint":"","key":"Notes.rtf","notification":{"bucket_name":"mybucket","content_type":"text/rtf","event_type":"Object:Delete","format":"2.0","object_length":"4642","object_name":"Notes.rtf","request_id":"b59727ee-9c4e-446a-9261-5616f6d1283b","request_time":"2021-04-13T20:10:37.631Z"},"operation":"Object:Delete"}  
CE_ID=b59727ee-9c4e-446a-9261-5616f6d1283b  
CE_SOURCE=https://cloud.ibm.com/catalog/services/cloud-object-storage/mybucket  
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T20:10:37.631Z  
CE_TYPE=com.ibm.cloud.cos.document.delete 
```
{: screen}


## Defining additional event attributes
{: #additional-attributes-cos}

When you create a subscription, you can define additional `CloudEvent` attributes to be included in any events that are generated. These attributes appear similar to any other `CloudEvent` attribute in the event delivery. If you choose to specify the name of an existing `CloudEvent` attribute, then it overrides the original value that was included in the event.

To define addition attributes, use the `--extension` options with the [**`ibmcloud ce subscription cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) CLI command.

For more information, see [Can I use other `CloudEvents` specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)

## Deleting a subscription
{: #subscription-delete-cos}

When you no longer need an {{site.data.keyword.cos_full_notm}} subscription, you can delete it.  
{: shortdesc}

### Deleting a subscription from the console
{: #subscription-delete-cos-ui}

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions.
3. From the list of subscriptions, delete the subscription that you want to remove from your application or job.

If you delete an app or a job that is associated with the subscription, the subscription is not deleted. If you re-create the application or job (or another app or job  with the same name), your subscription reconnects with the app or job. 
{: note}

### Deleting a subscription with the CLI
{: #subscription-delete-cos-cli}

You can delete an {{site.data.keyword.cos_full_notm}} subscription by running the [**`ibmcloud ce subscription cos delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, use the following command to delete an {{site.data.keyword.cos_full_notm}} subscription that is called `mycosevent`,

```txt
ibmcloud ce subscription cos delete --name mycosevent
```
{: pre}

If you delete an app or a job that is associated with the subscription, the subscription is not deleted. Instead, it moves to ready state of `false` because the subscription depends on the availability of the app or job. If you re-create the application or job (or another app or job  with the same name), your subscription reconnects and the Ready state is `true`. 
{: note}




