---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-11"

keywords: eventing, cron event, ping event, event producers, subscription, header, environment variables, subscription, subscribing, events

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
{:note .note}
{:note: .note}
{:note:.deprecated}
{:objectc data-hd-programlang="objectc"}
{:objectc: .ph data-hd-programlang='Objective C'}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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


# Working with the cron event producer
{: #subscribe-cron}

The cron event producer generates an event at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals.
{: shortdesc}

The cron event producer uses standard crontab syntax to specify interval details, in the format `* * * * *`, where the fields are minute, hour, day of month, month, and day of week. For example, to schedule an event for midnight, specify `0 0 * * *`. To schedule an event for every Friday at midnight, specify `0 0 * * FRI`. For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

You can create at most 100 cron subscriptions per project. In addition, when you use the `--data` or `--data-base64` option, you can send only 4096 bytes. For more information, see [Limits and quotas for Code Engine](/docs/codeengine?topic=codeengine-limits).

Cron subscriptions use the `UTC` time zone by default. You can change the time zone by specifying the `--time-zone` option with the **`sub cron create`** or the **`sub cron update`** commands. For valid time zone values, see the [TZ database name](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones){: external}. Note that if you create a subscription by using `kubectl` and do not specify a time zone, then the `UTC` time zone is assigned.

When you subscribe to a cron event, you must provide a destination (app or job) and a destination type for the subscription. If you do not provide a schedule, then the default of `* * * * *` (every minute) is used. For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

## Subscribing to cron events for an application
{: #eventing-cron-existing-app}

By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /event`, the event is sent to `https://<base application URL>/events`.

Events are sent to applications as HTTP POST requests. For more information about the information that is included with the event, see [HTTP headers and body information for events](#sub-header-body-cron).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create an application.
  
  For example, [create an application](/docs/codeengine?topic=codeengine-cli#cli-application-create) that is called `myapp` that uses the [`ping` image](https://hub.docker.com/r/ibmcom/ping){: external}. This image is built from `ping.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/ping){: external}.
  
  ```
  ibmcloud ce application create -name myapp --image ibmcom/ping
  ```
  {: pre}

You can connect your application to the cron event producer with the CLI by using the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command. 

```
ibmcloud ce sub cron create --name NAME --destination-type APP --destination APPLICATION_NAME --schedule CRON
```
{: pre}

For example, to create a cron subscription that sends an event to an app called `myapp` every day at midnight,

```
ibmcloud ce sub cron create --name mycronevent --destination-type app --destination myapp --schedule '0 0 * * *'
```
{: pre}

You must wrap the schedule value in single quotation marks to ensure that it is treated as a single string.
{: note}

The following table summarizes the options that are used with the **`sub cron create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command.

<table>
<caption><code>subscription cron create</code> options</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's options</th>
</thead>
<tbody>
<tr>
<td><code>--name</code></td>
<td>The name of the cron event source.
</td>
</tr>
<tr>
<td><code>--destination-type</code></td>
<td>The type of the `destination`, in this case, `app`. The default value is `app`.</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} application in the current project to receive the events from the event producer.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Schedule how often the event is triggered, in crontab format. For example, specify `*/2 * * * *` (in string format) for every two minutes. By default, the cron event is triggered every minute and is set to the UTC time zone. To modify the time zone, use the `--time-zone` option. For more information about crontab, see [CRONTAB](http://crontab.org/). This value is optional.</td>
</tr>
</tbody>
</table>

To verify that your cron subscription was successfully created, run the `ibmcloud ce sub cron get --name mycronevent` command. 

**Example output**

```
Getting cron source 'mycronevent'...
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           2m21s  
Created:       2021-03-14T13:37:51-05:00  

Destination:  App:myapp 
Schedule:     0 0 * * *  
Time Zone:    UTC  
Ready:        true 

Events: 
  Type     Reason            Age        Source                 Messages  
  Normal   FinalizerUpdate   12s        pingsource-controller  Updated "mycronevent" finalizers
```
{: screen}

From this output, you can see that the destination application is `myapp`, the schedule is `0 0 * * *` (midnight), and the Ready state is `true`.

Want to try a tutorial? See [Subscribing to cron events](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


### Viewing event information for an application
{: #view-eventing-cron-app}

If your application prints information to log files, as the `ping` application does, then view the application log files with the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) CLI command. For example, to view the logs for the application that you created in the previous example, 

```
ibmcloud ce application logs --application myapp
```
{: pre}

**Example output**

```
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

If you set your cron schedule to `0 0 * * *` (midnight), then you must wait until after midnight for the event to be sent. To update your cron event to run on a different schedule, for example, every 2 minutes, use the [**`ibmcloud ce sub cron update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-update) command, `ibmcloud ce sub cron update --name mycronevent --destination-type job --destination myjob --schedule '*/2 * * * *'`.
{: tip}

Note that log information lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


## HTTP headers and body information for events
{: #sub-header-body-cron}

All events that are delivered to applications are received as HTTP messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

### Common HTTP header
{: #sub-common-header-cron}

The following table shows the common HTTP headers that appear in each event that is delivered. The actual set of headers for each event can include more options. For more information and more header file options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

```
ce-id:  c329ed76-5004-4383-a3cc-c7a9b82e3ac6
ce-source: /apis/v1/namespaces/<namespace>/pingsources/mycronevent
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
| `ce-specversion` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For example, did a `write` or `delete` action occur. |
{: caption="Table 1. Header files for events" caption-side="top"}

### Cron header and body information
{: #sub-cron-header}

The following header and body information is specific to cron events.

**Header**

- `ce-source` is a URI-reference with the ID of the project (namespace) and the name of the cron subscription, for example, `/apis/v1/namespaces/6b0v3x9xek5/pingsources/mycronevent`.  
- `ce-type` is always `dev.knative.sources.ping`.

**HTTP body**

The HTTP body contains the event itself. The HTTP body for cron events is one of the following formats,

1. If the `data` on the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command is `JSON` format, then the HTTP body is that JSON output.
2. If the `data` is not JSON, then the HTTP body is in the format `{ "body": "xxx" }`, where `xxx` is the `data` string.


## Subscribing to cron events for a job
{: #eventing-cron-job}

Your job receives events as environment variables. For more information about the environment variables that are sent by cron, see [Environment variables for events](#sub-envir-variables-cron).

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create a job.
  
  For example, [create a job](/docs/codeengine?topic=codeengine-cli#cli-job-create) that is called `myjob` that uses the [`codeengine` image](https://hub.docker.com/r/ibmcom/codeengine){: external}. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
  
  ```
  ibmcloud ce job create -name myjob --image ibmcom/codeengine
  ```
  {: pre}

You can connect your job to the cron event producer with the CLI by using the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command. 

```
ibmcloud ce sub cron create --name NAME --destination-type job --destination JOB_NAME --schedule CRON
```
{: pre}

For example, to create a cron subscription that sends an event to a job called `myjob` every 5 minutes,

```
ibmcloud ce sub cron create --name mycronevent --destination-type job --destination myjob --schedule '*/5 * * * *' --data '{ "message": "Hello world!" }' --content-type application/json
```
{: pre}

You must wrap the schedule value in single quotation marks to ensure that it is treated as a single string.
{: note}

The following table summarizes the options that are used with the **`sub cron create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce subscription cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command.

<table>
<caption><code>subscription cron create</code> options</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's options</th>
</thead>
<tbody>
<tr>
<td><code>--name</code></td>
<td>The name of the cron event source.
</td>
</tr>
<tr>
<td><code>--destination-type</code></td>
<td>The type of the `destination`, in this case, `job`.</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} job in the current project to receive the events from the event producer.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Schedule how often the event is triggered, in crontab format. For example, specify `*/2 * * * *` (in string format) for every two minutes. By default, the cron event is triggered every minute and is set to the UTC time zone. To modify the time zone, use the `--time-zone` option. For more information about crontab, see [CRONTAB](http://crontab.org/). This value is optional.</td>
</tr>
</tbody>
</table>

To verify that your cron subscription was successfully created, run `ibmcloud ce sub cron get --name mycronevent`. 

**Example output**

```
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



### Viewing event information for a job
{: #view-eventing-cron-job}

If your job prints information to log files, as the `codeengine` job does, you can find the job run that was created from the cron event and then view the job run logs. For example, to find the job run for the job in the previous example, 

```
ibmcloud ce jobrun list
```
{: pre}

**Example output**

```
Listing job runs...
OK

Name         Failed  Pending  Requested  Running  Succeeded  Unknown  Age  
myjob-kd829  0       0        0          0        1          0        43s  
```
{: screen}

View the logs for the job run by specifying the jobrun name.

```
ibmcloud ce jobrun logs --jobrun myjob-kd829
```
{: pre}

**Example output**

```
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

Note that log information lasts for only one hour. For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

For more information about the environment variables that are sent by cron, see [Environment variables for events](#sub-envir-variables-cron).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}



## Environment variables for events
{: #sub-envir-variables-cron}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

### Common environment variables
{: #sub-envir-variables-common-cron}

Each event contains some common environment variables that appear every time the event is delivered. The actual set of variables in each event can include more options. For more information and more environment variable options, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}. 

``` 
CE_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
CE_SPECVERSION=1.0  
CE_TIME=2021-04-13T17:41:00.429658447Z  
```
{: screen}

The following table describes the common environment variables values.

| Variable   | Description      | 
|----------|------------------|
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. | 
| `CE_SPECVERSION` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `CE_TIME` | The time that the event was generated. |
{: caption="Table 3. Environment variables for events" caption-side="top"}

### Cron environment variables
{: #sub-cron-environment-variable-cron}

The following environment variables values are specific to cron events.

- `CE_SOURCE` is a URI-reference with the ID of the project (namespace) and the name of the cron subscription, for example, `/apis/v1/namespaces/6b0v3x9xek5/pingsources/mycronevent`.  
- `CE_TYPE` is always `dev.knative.sources.ping`.
- `CE_DATA` is one of the following:
   1. If the `data` on the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command is `JSON` format, then the environment variable is that JSON output.
   2. If the `data` is not JSON, then the HTTP body is in the format `{ "body": "xxx" }`, where `xxx` is the `data` string.


## Defining additional `CloudEvent` attributes
{: #additional-attributes}

When you create a subscription, you can define additional `CloudEvent` attributes to be included in any events that are generated. These attributes appear similar to any other `CloudEvent` attribute in the event delivery. If you choose to specify the name of an existing `CloudEvent` attribute, then it overrides the original value that was included in the event.

To define addition attributes, use the `--extension` options with the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) CLI command.

For more information, see [Can I use other `CloudEvents` specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)


## Deleting a subscription
{: #subscription-delete-cron}

You can delete a subscription by running the [**`ibmcloud ce sub cron delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-delete) or the [**`ibmcloud ce sub cos delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) command.

For example, delete a cron subscription that is called `mycronevent2`,

```
ibmcloud ce subscription cron delete --name mycronevent2
```
{: pre}

If you delete an app or a job, the subscription is not deleted. Instead, the subscription moves to ready state of `false` because the subscription depends on the availability of the application or job. If you re-create the app or job (or another app or job with the same name), your subscription reconnects and the Ready state is `true`.
{: note}


