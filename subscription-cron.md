---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-16"

keywords: eventing, cron event, periodic timer event, ping event, event producers, subscription, header, environment variables, subscription, subscribing, events

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Periodic timer (cron) event producer
{: #subscribe-cron}

The Periodic timer (cron) event producer generates an event at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals. You can subscribe {{site.data.keyword.codeengineshort}} apps and jobs to receive cron events. 
{: shortdesc}

The Periodic timer (cron) event subscription uses standard crontab syntax to specify interval details, in the format `* * * * *`, where the fields are minute, hour, day of month, month, and day of week. For example, to schedule an event for midnight, specify `0 0 * * *`. To schedule an event for every Friday at midnight, specify `0 0 * * 5`. For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

When you subscribe to a Periodic timer (cron) event producer, you must provide a destination (app or job) and a destination type for the subscription. If you do not provide a schedule, then the default of `* * * * *` (every minute) is used. 

{{site.data.keyword.codeengineshort}} has quotas for Periodic timer (cron) subscriptions within a project and subscription limits. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Subscribing to Periodic timer (cron) events for an application
{: #eventing-cron-existing-app}

You can work with Periodic timer (cron) subscriptions from the console or with the CLI. 
{: shortdesc}

Events are sent to applications as HTTP POST requests. For more information about the information that is included with the event, see [HTTP headers and body information for events](#sub-header-body-cron).

### Subscribing to Periodic timer (cron) events for an application from the console
{: #eventing-cron-existing-app-ui}

You can create and update Periodic timer (cron) event subscriptions for an application from the console.
{: shortdesc}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an application](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console). For example, create an application that is called `myapp` that uses the `icr.io/codeengine/cron` image. This image is built from `cron.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cron){: external}.

Complete the following steps to create and update a Periodic timer (cron) event subscription for an application from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create event subscription page, complete the following steps.
   1. For **Event type**, select the Periodic timer tile. Click **Next**. 
   2. For **General**, provide a name for the Periodic timer subscription, for example, `myptimer`. You can optionally provide event attributes. Note that if the Periodic timer event consumer is an application, event attributes are available as HTTP headers. If the event consumer is a job, event attributes are available as environment variables. Click **Next** to proceed.
   3. For **Schedule**, provide information about the timing of the events. The Periodic timer (cron) event producer uses standard crontab syntax to specify interval details. Choose your interval from the provided patterns or provide your own custom cron expression, such as `0 0 * * *`, which specifies for the event to occur every day at midnight. For this example, select the schedule pattern for every day, every hour, every minute. Notice that the cron expression is generated for you. The day, hour, and minute patterns and the **Cron expression** are in Coordinated Universal Time (UTC). If you do not specify a schedule, then this event subscription sends an event every minute. A list of upcoming scheduled events is displayed. Notice that these upcoming scheduled events are displayed in your time zone. Click **Next** to proceed. 
   4. For **Custom event data**, provide data to include in the body of your event message. You can specify the message as plain text or in base64 format. For this example, specify the text, `hello stranger` as the body of the event message. If the message is in base64 format, you can choose to have the message decoded when the event is sent. You can also specify the content type for your custom event data. Click **Next** to proceed.
   5. For **Event consumer**, specify the application or job to receive events. Notice that you can choose from a list of defined applications and jobs. For this example, use the `myapp` application that references the `icr.io/codeengine/cron` image. If you have not yet created your app or job, you can specify the name of your application or job and [create your application](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [create your job](/docs/codeengine?topic=codeengine-job-plan) after you create the Periodic timer (cron) subscription. For applications only, you can optionally specify a path. By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by specifying a path. For example, if your subscription path specifies `/events`, the events are sent to `https://<base application URL>/events`. Click **Next** to proceed.
   6. For **Summary**, review the settings for your Periodic timer event subscription and make changes if needed. When ready, click **Create** to create the Periodic timer (cron) subscription. 

5. Now that your Periodic timer (cron) subscription is created, go to the Event subscriptions page to [view a listing of defined subscriptions](#view-eventing-cron-app-ui). 
6. To update a subscription, navigate to your Periodic timer (cron) subscription page. From the Event subscriptions page, click the name of the subscription that you want to update. 
7. From your Periodic timer (cron) subscription page, let's change the data in the event message. From the **Custom event data** tab, change the event data to `hello sunshine`. Click **Save** to save your changes. 
8. Because the `myapp` application references the sample `cron` application, which prints information to log files, you can view the logs. View the application logs for the `myapp` event consumer application and see that the event message is `hello sunshine`. See [Viewing application logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui).

### Subscribing to Periodic timer (cron) events for an application with the CLI
{: #eventing-cron-existing-app-cli}

Before you begin

* [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an application](/docs/codeengine?topic=codeengine-cli#cli-application-create). For example, create an application that is called `myapp` that uses the `icr.io/codeengine/cron` image. This image is built from `cron.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cron){: external}

```txt
ibmcloud ce application create -name myapp --image icr.io/codeengine/cron
```
{: pre}

To connect your application to the Periodic timer (cron) subscription with the CLI, use the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command. 

```txt
ibmcloud ce sub cron create --name NAME --destination-type APP --destination APPLICATION_NAME --schedule CRON
```
{: pre}

For example, to create a cron subscription that sends an event to an app called `myapp` every day at midnight,

```txt
ibmcloud ce sub cron create --name mycronevent --destination-type app --destination myapp --schedule '0 0 * * *'
```
{: pre}

You must wrap the schedule value in quotation marks to ensure that it is treated as a single string.
{: note}

The following table summarizes the options that are used in the previous example with the **`sub cron create`** command. For more information about the command and its options, see the [**`ibmcloud ce subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command.

| Option | Description |
| --- | --- |
| `--name` | The name of the cron event source. This value is required. |
| `--destination` | The name of a {{site.data.keyword.codeengineshort}} application or job in the current project to receive the events from the event producer. This value is required. |
| `--destination-type` | The type of the `destination`, in this case, `app`. The default value is `app`. |
| `--schedule` | Schedule how often the event is triggered, in crontab format. For example, specify `*/2 * * * *` (in string format) for every 2 minutes. By default, the cron event is triggered every minute and is set to the UTC time zone. To modify the time zone, use the `--time-zone` option. This value is optional. |
{: caption="Table 1. Command options" caption-side="bottom"}

Tips for using the **`sub cron`** commands
:    - By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /events`, the events are sent to `https://<base application URL>/events`.
     - The size of data for Periodic timer (cron) events is limited to a maximum of 4096 bytes. Thus, if you use the `--data` option or the `--data-base64` option, you can send a maximum of 4096 bytes. For more information, see [Limits and quotas for Code Engine](/docs/codeengine?topic=codeengine-limits).
     - Cron subscriptions use the `UTC` time zone by default. You can change the time zone by specifying the `--time-zone` option with the **`sub cron create`** or the **`sub cron update`** commands. For valid time zone values, see the [TZ database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones){: external}. Note that if you create a subscription by using `kubectl` and do not specify a time zone, then the `UTC` time zone is assigned.
     - If you have not yet created your app or job event consumer, use the `--force` option with the **`sub cron create`**  command to force the create of the cron event subscription. You can specify the name of your application or job and [create your application](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [create your job](/docs/codeengine?topic=codeengine-job-plan) after you create the cron subscription.

To verify that your cron subscription was successfully created, run the `ibmcloud ce sub cron get --name mycronevent` command. 

Example output

```txt
Getting cron source 'mycronevent'...
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m21s  
Created:       2021-03-14T13:37:51-05:00  

Destination Type:  app
Destination:       myapp
Schedule:          0 0 * * *  
Time Zone:         UTC  
Ready:             true 

Events: 
    Type     Reason            Age        Source                 Messages  
    Normal   FinalizerUpdate   12s        pingsource-controller  Updated "mycronevent" finalizers
```
{: screen}

From this output, you can see that the destination application is `myapp`, the schedule is `0 0 * * *` (every day at midnight), and the Ready state is `true`.

### Updating your cron subscription with the CLI
{: #update-cron-sub-cli}

To update the cron subscription with the CLI, use the [**`ibmcloud ce subscription cron update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-update) command. For example, update the `mycronevent` subscription to change the schedule to sends an event to an app called `myapp` every 2 minutes.

```txt
ibmcloud ce sub cron update --name mycronevent --schedule '*/2 * * * *'
```
{: pre}

To verify that your cron subscription was successfully updated, run the `ibmcloud ce sub cron get --name mycronevent` command. The schedule for the subscription is updated.

Example output

```txt
Getting cron source 'mycronevent'...
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m21s  
Created:       2021-08-31T16:00:49-04:00

Destination Type:  app
Destination:       myapp
Schedule:          */2 * * * *
Time Zone:         UTC
Ready:             true

Events:
  Type    Reason                       Age               Source                 Messages
  Normal  PingSourceSynchronized       7s (x3 over 13m)  pingsource-controller  PingSource adapter is synchronized
```
{: screen}

Want to try a tutorial? See [Subscribing to Periodic timer (cron) events](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Viewing event information for an application from the console
{: #view-eventing-cron-app-ui}

To view information about your event subscriptions, 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions. 

If your application prints information to log files, as the sample `cron` application does, then view the log files for your event consumer application. See [Viewing application logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui).

### Viewing event information for an application with the CLI
{: #view-eventing-cron-app-cli}

If your application prints information to log files, as the sample `cron` application does, then view the log files for your event consumer application with the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) CLI command. For example, to view the logs for the application that you created in the previous example, 

```txt
ibmcloud ce application logs --application myapp
```
{: pre}

Example output

```txt
Getting logs for all instances of application 'myapp'...
OK

myapp-mw25y-1-deployment-8579d868f4-ssfnr/user-container:    
Listening on port 8080  
2021-04-13 17:22:08 - Received:  
URL: /  
Header: Accept-Encoding=[gzip]  
Header: Ce-Id=[d2faa29c-8088-410f-bb30-416085c52a0b]  
Header: Ce-Source=[/apis/v1/namespaces/81fvkfqi3n6/pingsources/mycronevent]  
Header: Ce-Specversion=[1.0]  
Header: Ce-Time=[2021-04-13T17:22:00.059682656Z]  
Header: Ce-Type=[dev.knative.sources.ping]  
Header: Content-Length=[0]  
Header: Forwarded=[for=172.30.136.209;proto=http, for=172.30.48.203]  
Header: K-Proxy-Request=[activator]  
Header: Traceparent=[00-b13196fe439b6d7d67f3205b2f655788-e9fee441cd41158c-00]  
Header: User-Agent=[Go-http-client/1.1]  
Header: X-B3-Sampled=[0]  
Header: X-B3-Spanid=[1dd2d76079811204]  
Header: X-B3-Traceid=[710b7c383682d0cd1dd2d76079811204]  
Header: X-Envoy-Attempt-Count=[1]  
Header: X-Envoy-Decorator-Operation=[myapp-mw25y-1.81fvkfqi3n6.svc.cluster.local:80/*]  
Header: X-Envoy-Internal=[true]  
Header: X-Envoy-Peer-Metadata=[ChQKDkFQUF9DT05UQUlORVJTEgIaAAoaCgpDTFVTVEVSX0lEEgwaCkt1YmVybmV0ZXMKGAoNSVNUSU9fVkVSU0lPThIHGgUxLjkuMQq+AwoGTEFCRUxTErMDKrADCh0KA2FwcBIWGhRpc3Rpby1pbmdyZXNzZ2F0ZXdheQoTCgVjaGFydBIKGghnYXRld2F5cwoUCghoZXJpdGFnZRIIGgZUaWxsZXIKNgopaW5zdGFsbC5vcGVyYXRvci5pc3Rpby5pby9vd25pbmctcmVzb3VyY2USCRoHdW5rbm93bgoZCgVpc3RpbxIQGg5pbmdyZXNzZ2F0ZXdheQoZCgxpc3Rpby5pby9yZXYSCRoHZGVmYXVsdAowChtvcGVyYXRvci5pc3Rpby5pby9jb21wb25lbnQSERoPSW5ncmVzc0dhdGV3YXlzCiAKEXBvZC10ZW1wbGF0ZS1oYXNoEgsaCTU1YjU0N2Y0ZgoSCgdyZWxlYXNlEgcaBWlzdGlvCjkKH3NlcnZpY2UuaXN0aW8uaW8vY2Fub25pY2FsLW5hbWUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXkKLwojc2VydmljZS5pc3Rpby5pby9jYW5vbmljYWwtcmV2aXNpb24SCBoGbGF0ZXN0CiIKF3NpZGVjYXIuaXN0aW8uaW8vaW5qZWN0EgcaBWZhbHNlChoKB01FU0hfSUQSDxoNY2x1c3Rlci5sb2NhbAouCgROQU1FEiYaJGlzdGlvLWluZ3Jlc3NnYXRld2F5LTU1YjU0N2Y0Zi10aHN4cAobCglOQU1FU1BBQ0USDhoMaXN0aW8tc3lzdGVtCl0KBU9XTkVSElQaUmt1YmVybmV0ZXM6Ly9hcGlzL2FwcHMvdjEvbmFtZXNwYWNlcy9pc3Rpby1zeXN0ZW0vZGVwbG95bWVudHMvaXN0aW8taW5ncmVzc2dhdGV3YXkKFwoRUExBVEZPUk1fTUVUQURBVEESAioACicKDVdPUktMT0FEX05BTUUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXk=]  
Header: X-Envoy-Peer-Metadata-Id=[router~172.30.48.203~istio-ingressgateway-55b547f4f-thsxp.istio-system~istio-system.svc.cluster.local]  
Header: X-Forwarded-For=[172.30.136.209, 172.30.48.203, 172.30.167.171]  
Header: X-Forwarded-Proto=[http]  
Header: X-Request-Id=[fe8d6cec-f0e4-47c2-b9ae-81764cb377bc]  
```
{: screen}

For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Cron header and body information for events delivered to applications
{: #sub-header-body-cron}

All events that are delivered to applications are received as HTTP POST messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

#### Headers
{: #sub-header-cron}

The following table describes the headers for Periodic timer (cron) events.

| Header   | Description      | 
|----------|------------------|
| `ce-id` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `ce-source` | A URI-reference that indicates where this event originated from within the event producer. For cron events, this header is a URI-reference with sub-domain for the project and the name of the cron subscription, in the following format: `/apis/v1/namespaces/[PROJECT_SUBDOMAIN]/pingsources/[SUBSCRIPTION_NAME]`. |
| `ce-specversion` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For cron events, this is `dev.knative.sources.ping`. |
{: caption="Table 1. Header files for events" caption-side="top"}

Example output 

```txt
ce-id: c329ed76-5004-4383-a3cc-c7a9b82e3ac6
ce-source: /apis/v1/namespaces/6b0v3x9xek5/pingsources/mycronevent
ce-specversion: 1.0
ce-time: 2021-02-26T19:19:00.497637287Z
ce-type: dev.knative.sources.ping
```
{: screen}

#### HTTP body
{: #sub-body-cron}

The HTTP body contains the event itself and is in the format that you specify when you create or update the subscription. 

## Subscribing to Periodic timer (cron) events for a job
{: #eventing-cron-job}

You can work with Periodic timer (cron) subscriptions from the console or with the CLI. 
{: shortdesc}

Your job receives events as environment variables. For more information about the environment variables that are sent by cron, see [Environment variables for events](#sub-envir-variables-cron).

### Subscribing to Periodic timer (cron) events for a job from the console
{: #eventing-cron-job-ui}

You can create and update Periodic timer (cron) event subscriptions for a job from the console. 
{: shortdesc}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create a job](/docs/codeengine?topic=codeengine-cli#cli-job-create). For example, create a job that is called `myjob` that uses the `codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.

Complete the following steps to create and update a Periodic timer (cron) event subscription for a job from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create event subscription page, complete the following steps.
   1. For **General**, provide a name for the Periodic timer subscription, for example, `myptimer2`. You can optionally provide event attributes. Note that if the Periodic timer event consumer is an application, event attributes are available as HTTP headers. If the event consumer is a job, event attributes are available as environment variables. Click **Next** to proceed.
   2. For **Schedule**, provide information about the timing of the events. The Periodic timer (cron) event producer uses standard crontab syntax to specify interval details. Choose your interval from the provided patterns or provide your own custom cron expression, such as `0 0 * * *`, which specifies for the event to occur every day at midnight. For this example, select the schedule pattern for every day, every hour, every minute. Notice that the cron expression is generated for you. The day, hour, and minute patterns and the **Cron expression** are in Coordinated Universal Time (UTC). If you do not specify a schedule, then this event subscription sends an event every minute. A list of upcoming scheduled events is displayed. Notice that these upcoming scheduled events are displayed in your time zone. Click **Next** to proceed. 
   3. For **Custom event data**, provide data to include in the body of your event message. You can specify the message as plain text or in base64 format. For this example, specify the text, `hello stranger` as the body of the event message. If the message is in base64 format, you can choose to have the message decoded when the event is sent. You can also specify the content type for your custom event data. Click **Next** to proceed.
   4. For **Event consumer**, specify the application or job to receive events. Notice that you can choose from a list of defined applications and jobs. For this example, use the `myjob` job that references the `icr.io/codeengine/codeengine` image. If you have not yet created your job, you can specify the name of your job and [create your job](/docs/codeengine?topic=codeengine-job-plan) after you create the Periodic timer (cron) subscription. Click **Next** to proceed.
   5. For **Summary**, review the settings for your Periodic timer event subscription and make changes if needed. When ready, click **Create** to create the Periodic timer (cron) subscription. 

5. Now that your Periodic timer (cron) subscription is created, go to the Event subscriptions page to [view a listing of defined subscriptions](#view-eventing-cron-app-ui). 
6. To update a subscription, navigate to your Periodic timer (cron) subscription page. From the Event subscriptions page, click the name of the subscription that you want to update. 
7. From your Periodic timer (cron) subscription page, let's change the data in the event message. From the **Custom event data** tab, change the event data to `hello sunshine`. Click **Save** to save your changes. 
8. Because the `myjob` job references the sample `codeengine` application, which prints information to log files, you can view the logs. View the job logs for the `myjob` event consumer job and see that the event message is `hello sunshine`. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui).


### Subscribing to Periodic timer (cron) events for a job with the CLI
{: #eventing-cron-job-cli}

Before you begin

* [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create a job](/docs/codeengine?topic=codeengine-cli#cli-job-create). For example, create a job that is called `myjob` that uses the `icr.io/codeengine/codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.

```txt
ibmcloud ce job create -name myjob --image icr.io/codeengine/codeengine
```
{: pre}


To connect your job to the Periodic timer (cron) subscription with the CLI by using the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command. 

```txt
ibmcloud ce sub cron create --name NAME --destination-type job --destination JOB_NAME --schedule CRON
```
{: pre}

For example, to create a cron subscription that sends an event to a job called `myjob` every 5 minutes,

```txt
ibmcloud ce sub cron create --name mycronevent --destination-type job --destination myjob --schedule '*/5 * * * *' --data '{ "message": "Hello world!" }' --content-type application/json
```
{: pre}

You must wrap the schedule value in quotation marks to ensure that it is treated as a single string.
{: note}

The following table summarizes the options that are used with the **`sub cron create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command.

| Option | Description |
| --- | --- |
| `--name` | The name of the cron event source. |
| `--destination-type` | The type of the `destination`, in this case, `job`. |
| `--destination` | The name of a {{site.data.keyword.codeengineshort}} job in the current project to receive the events from the event producer. |
| `--schedule` | Schedule how often the event is triggered, in crontab format. For example, specify `*/2 * * * *` (in string format) for every 2 minutes. By default, the cron event is triggered every minute and is set to the UTC time zone. To modify the time zone, use the `--time-zone` option. This value is optional. |
{: caption="Table 1. Command options" caption-side="bottom"}

Tips for using the **`sub cron`** commands
:    - The size of data for Periodic timer (cron) events is limited to a maximum of 4096 bytes. Thus, if you use the `--data` option or the `--data-base64` option, you can send a maximum of 4096 bytes. For more information, see [Limits and quotas for Code Engine](/docs/codeengine?topic=codeengine-limits).
     - Cron subscriptions use the `UTC` time zone by default. You can change the time zone by specifying the `--time-zone` option with the **`sub cron create`** or the **`sub cron update`** commands. For valid time zone values, see the [TZ database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones){: external}. Note that if you create a subscription by using `kubectl` and do not specify a time zone, then the `UTC` time zone is assigned.
     - If you have not yet created your app or job event consumer, use the `--force` option with the **`sub cron create`**  command to force the create of the cron event subscription. You can specify the name of your application or job and [create your application](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [create your job](/docs/codeengine?topic=codeengine-job-plan) after you create the cron subscription.

To verify that your cron subscription was successfully created, run `ibmcloud ce sub cron get --name mycronevent`. 

Example output

```txt
Getting cron source 'mycronevent'... 
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           54s  
Created:       2021-04-13T11:38:50-05:00  

Destination Type:  job  
Destination:       myjob  
Schedule:          */5 * * * *  
Time Zone:         UTC  
Content Type:      application/json  
Data:              { "message": "Hello world!" }  
Ready:             true  

Events: 
    Type     Reason            Age        Source                 Messages  
    Normal   FinalizerUpdate   12s        pingsource-controller  Updated "mycronevent" finalizers
```
{: screen}

From this output, you can see that the destination job is `myjob`, the schedule is `*/5 * * * *` (every 5 minutes), and the Ready state is `true`.

Job runs that are created by subscriptions are deleted after 10 minutes.
{: note}

#### Updating the cron subscription with the CLI (job)
{: #update-cron-sub-job}

To update the cron subscription with the CLI, use the [**`ibmcloud ce subscription cron update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-update) command. For example, update the `mycronevent` subscription to change the schedule to sends an event to an app called `myapp` every 2 minutes.

```txt
ibmcloud ce sub cron update --name mycronevent --schedule '*/2 * * * *'
```
{: pre}

To verify that your cron subscription was successfully updated, run the `ibmcloud ce sub cron get --name mycronevent` command. The schedule for the subscription is updated.

Example output

```txt
Getting cron source 'mycronevent'...
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m21s  
Created:       2021-08-31T16:00:49-04:00

Destination Type:  job
Destination:       myjob
Schedule:          */2 * * * *
Time Zone:         UTC  
Content Type:      application/json  
Data:              { "message": "Hello world!" }  
Ready:             true  

Events:
  Type    Reason                       Age               Source                 Messages
  Normal  PingSourceSynchronized       7s (x3 over 13m)  pingsource-controller  PingSource adapter is synchronized
```
{: screen}

### Viewing event information for a job from the console
{: #view-eventing-cron-job-ui}

To view information about your event subscriptions, 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions. 

If your job prints information to log files, as the sample `codeengine` job does, then view the log files for your event consumer job. See [Viewing job logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui). 

### Viewing event information for a job with the CLI
{: #view-eventing-cron-job-cli}

If your job prints information to log files, as the sample `codeengine` job does, you can find the job run that was created from the Periodic timer (cron) event and then view the job run logs. For example, to find the job run for the job in the previous example, 

```txt
ibmcloud ce jobrun list
```
{: pre}

Example output

```txt
Listing job runs...
OK

Name         Failed  Pending  Requested  Running  Succeeded  Unknown  Age  
myjob-kd829  0       0        0          0        1          0        43s  
```
{: screen}

View the logs for the job run by specifying the job run name.

```txt
ibmcloud ce jobrun logs --jobrun myjob-kd829
```
{: pre}

Example output

```txt
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
CE_DATA={ "message": "Hello world!" } 
CE_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
CE_SOURCE=/apis/v1/namespaces/1234abcd1a2/pingsources/mycroneventjob  
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T17:41:00.429658447Z  
CE_TYPE=dev.knative.sources.ping 
CONTENT_TYPE=application/json 
HOME=/root  
HOSTNAME=myjob-mpps4-0-0  
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

For more information about the environment variables that are sent by cron, see [Environment variables for events](#sub-envir-variables-cron).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Environment variables for events that are delivered to jobs
{: #sub-envir-variables-cron}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

Each event contains some common environment variables that appear every time that the event is delivered to a job. The actual set of variables in each event can include more options. For more information, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

The following table describes the environment variables that are specific to cron events. 

| Variable   | Description      | 
|----------|------------------|
| `CE_DATA` | The data (body) for the event. See [`CE_DATA` for cron events](/docs/codeengine?topic=codeengine-subscribe-cron#subcron-envvar-cedata). |
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `CE_SOURCE` | A URI-reference that indicates where this event originated from within the event producer. For cron events, this is a URI-reference with sub-domain for the project and the name of the cron subscription, in the following format: `/apis/v1/namespaces/[PROJECT_SUBDOMAIN]/pingsources/[SUBSCRIPTION_NAME]`. |
| `CE_SPECVERSION` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `CE_TIME` | The time that the event was generated. |
| `CE_TYPE` | The type of the event. For cron events, this is `dev.knative.sources.ping`.  |
{: caption="Table 3. Environment variables for events" caption-side="top"}

#### `CE_DATA` environment variable 
{: #subcron-envvar-cedata}

For Periodic timer (cron) events, the `CE_DATA` environment variable contains the event itself and is in the format that you specify when you create or update the subscription. 

Example output 

```txt
CE_DATA={ "message": "Hello world!" } 
CE_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
CE_SOURCE=/apis/v1/namespaces/1234abcd1a2/pingsources/mycroneventjob  
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T17:41:00.429658447Z  
CE_TYPE=dev.knative.sources.ping 
```
{: screen}

## Defining additional event attributes
{: #additional-attributes-cron}

When you create a subscription, you can define additional event attributes to be included in any events that are generated. These event attributes appear similar to any other `CloudEvent` attribute in the event delivery. If you choose to specify the name of an existing `CloudEvent` attribute, then it overrides the original value that was included in the event. For more information, see [Can I use other `CloudEvents` specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)

From the console, you can specify event attributes as key-value pairs from the **General** tab for your Periodic timer (cron) event subscription.

With the CLI, to define additional attributes, use the `--extension` options with the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) CLI command.

## Deleting a subscription
{: #subscription-delete-cron}

When you no longer need a Periodic timer (cron) subscription, you can delete it. 
{: shortdesc}

### Deleting a subscription from the console
{: #subscription-delete-cron-ui}

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions.
3. From the list of subscriptions, delete the subscription that you want to remove from your application or job.

If you delete an app or a job, the subscription is not deleted.
{: note}

### Deleting a subscription with the CLI
{: #subscription-delete-cron-cli}

You can delete a subscription by running the [**`ibmcloud ce sub cron delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-delete) or the [**`ibmcloud ce sub cos delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, delete a cron subscription that is called `mycronevent2`,

```txt
ibmcloud ce subscription cron delete --name mycronevent2
```
{: pre}

If you delete an app or a job, the subscription is not deleted. Instead, in the CLI, the subscription moves to ready state of `false` because the subscription depends on the availability of the application or job. If you re-create the app or job (or another app or job with the same name), your subscription reconnects and the Ready state is `true`.
{: note}


