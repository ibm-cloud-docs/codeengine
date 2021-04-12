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


# Working with the Ping event producer
{: #subscribe-ping}

The Ping (cron) event producer generates an event at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals.
{: shortdesc}

Ping uses standard crontab syntax to specify interval details, in the format `* * * * *`, where the fields are minute, hour, day of month, month, and day of week. For example, to schedule an event for midnight, specify `0 0 * * *`.  To schedule an event for every Friday at midnight, specify `0 0 * * FRI`. For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

You can create at most 100 Ping subscriptions per project. In addition, when you use the `--data` or `--data-base64` option, you can send only 4096 bytes.

Ping subscriptions use the `UTC` time zone by default. You can change the time zone by specifying the `--time-zone` option with the `sub ping create` or the `sub ping update` commands. For valid time zone values, see the [TZ database name](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones){: external}. Note that if you create a subscription by using `kubectl` and do not specify a time zone, then the `UTC` time zone is assigned.

## Subscribing to Ping events
{: #eventing-ping-existing-app}

When you subscribe to a Ping event, you must provide a destination (app) for the subscription. If you do not provide a schedule, then the default of `* * * * *` (every minute) is used.

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Create an application.
  
  For example, [create an application](/docs/codeengine?topic=codeengine-cli#cli-application-create) called `myapp` that uses the `ping` image from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
  
  ```
  ibmcloud ce application create -name myapp --image ibmcom/ping
  ```
  {: pre}

You can connect your application to the Ping event producer with the CLI by using the [`sub ping create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-create) command. 

```
ibmcloud ce sub ping create --name NAME --destination APPLICATION --schedule CRON
```
{: pre}

For example, to create a Ping subscription that sends an event to an app called `myapp` every day at midnight,

```
ibmcloud ce sub ping create --name mypingevent --destination myapp --schedule '0 0 * * *'
```
{: pre}

You must wrap the schedule value in single quotes to ensure that it is treated as a single string.
{: note}

The following table summarizes the options used with the `sub ping create` command in this example. For more information about the command and its options, see the [`ibmcloud ce subscription ping create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-create) command.

<table>
<caption><code>subscription ping create</code> options</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's options</th>
</thead>
<tbody>
<tr>
<td><code>--name</code></td>
<td>The name of the Ping event source.
</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The name of a {{site.data.keyword.codeengineshort}} application in the current project to receive the events from the event producer.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Schedule how often the event is triggered, in crontab format. For example, specify `*/2 * * * *` (in string format) for every two minutes. By default, the Ping event is triggered every minute and is set to the UTC time zone. To modify the time zone, use the `--time-zone` option. This value is optional.</td>
</tr>
</tbody>
</table>

To verify that your Ping subscription was successfully created, run `ibmcloud ce sub ping get --name mypingevent`. 

**Example output**

```
Getting Ping source 'mypingevent'...
OK

Name:          mypingevent  
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
  Normal   FinalizerUpdate   12s        pingsource-controller  Updated "mypingevent" finalizers
```
{: screen}

From this output, you can see that the destination application is `myapp`, the schedule is `0 0 * * *` (midnight), and the Ready state is `true`.

You can also use the `—force` option to bypass the destination check during the `ping subscription create` process and create a Ping subscription that forwards events to a non-existent destination application. Your Ping subscription displays `false` as a Ready state until the application is created.

Want to try a tutorial? See [Subscribing to ping events](/docs/codeengine?topic=codeengine-subscribe-ping-tutorial). Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
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

### Ping header and body information
{: #sub-ping-header}

The following header and body information is specific to Ping events.

**Header**

- `ce-source` is a URI-reference with the ID of the project (namespace) and the name of the Ping subscription, for example, `/apis/v1/namespaces/6b0v3x9xek5/pingsources/myping`.  
- `ce-type` is always `dev.knative.sources.ping`.

**HTTP body**

The HTTP body contains the event itself. The HTTP body for Ping events is one of the following formats,

1. If the `data` on the `ibmcloud ce sub ping create` is `JSON` format, then the HTTP body is that JSON output.
2. If the `data` is not JSON, then the HTTP body is in the format `{ "body": "xxx" }`, where `xxx` is the `data` string.
