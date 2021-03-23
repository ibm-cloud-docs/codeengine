---

copyright:
  years: 2021
lastupdated: "2021-03-23"

keywords: subscription tutorial for code engine, eventing and code engine, subscriptions, tutorial for code engine, eventing tutorial for code engine, subscription, ping

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


# Subscribing to ping events
{: #subscribe-ping-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, subscribe to ping events by using the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

Oftentimes in distributed environments you want your applications to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications can receive events of interest as HTTP POST requests by subscribing to event producers.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports two types of event producers. The first is a ping (cron) event producer that generates an event at regular intervals. This type of event producer is used when an action needs to be taken at well-defined intervals or specific times. The second is an {{site.data.keyword.cos_full_notm}} event producer. This type of event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform some action based on that change, perhaps consuming that new object.

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

## Determine your ping interval
{: #determine-ping-interval}
{: step}

The ping (cron) event producer generates an event at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals.
{: shortdesc}

Ping uses a standard crontab to specify interval details, in the format `* * * * *`, which stands for minute, hour, day of month, month, and day of week. For example, to schedule an event for midnight, specify `0 0 * * *`.  To schedule an event for every Friday at midnight, specify `0 0 * * FRI`.

For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

You can set your ping interval by using the `--schedule` option with the `subscription ping` command, as shown in Step 3. By default, the ping event is sent every minute of every day. 

## Create your app
{: #create-app}
{: step}

Create your application called `ping-app` with the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. This app pulls an image that is called `ping` that is available from public Docker Hub and always has an instance that is running (`--min-scale=1`). This app logs each event as it arrives, showing the full set of HTTP Headers and HTTP Body payload.
{: shortdesc}

```
ibmcloud ce app create --name ping-app --image ibmcom/ping --min-scale=1
```
{: pre}

Run `ibmcloud ce application get --name ping-app` to verify that your app is in a `Ready` state.

You can find more information about this app at [Ping readme file](https://github.com/IBM/CodeEngine/tree/main/ping){: external}.

## Create a subscription
{: #create-subscription}
{: step}

After your app is ready, create a subscription to the ping event producer and connect it to your app with the [`ibmcloud ce sub ping create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-create) command.
{: shortdesc}

For example, create a subscription called `ping-sub` with `ping-app` as its destination. This example also includes the `--data` option to include some JSON in the ping event. Finally, specify the ping schedule. In this case, the example uses `* * * * *`, sending an event every minute of every hour of every day of every month for every day of the week, which is a useful schedule for testing your app subscription. 

```
ibmcloud ce sub ping create --name ping-sub --destination ping-app --data '{"mydata":"hello world"}' --schedule '* * * * *'
```
{: pre}

Run `ibmcloud ce sub ping get -n ping-sub` to find information about your subscription.

**Example output**

In this output, you can see that the subscription name, destination, schedule, and data are correct.

```
Getting ping event subscription 'ping-sub'...
OK

Name:          ping-sub  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           2m18s  
Created:       2021-03-14T13:21:13-05:00   

Destination:  App:ping-app  
Schedule:     * * * * *  
Data:         {"mydata":"hello world"}  
Ready:        true

Events:    
  Type     Reason                 Age                Source                 Messages   
  Normal   FinalizerUpdate        65s                pingsource-controller  Updated "ping-sub" finalizers 
 
```
{: screen}

## Testing your subscription
{: #test-subscription}
{: step}

After you successfully subscribed your app to your ping event, look at the logs to see whether it works.
{: shortdesc}

Get the logs for the app with the [`ibmcloud ce app logs`](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command. 

```
ibmcloud ce app logs --name ping-app
```
{: pre}

**Example output**

In the following output, you can see that the data and time that the event was received as well as the HTTP Headers and the HTTP Body JSON that was passed in when the subscription was created.

```
2021-01-21 20:15:00 - Received:  
Header: Accept-Encoding=[gzip]  
Header: Ce-Id=[7de01e8e-84dc-4409-ad56-90d6e391397c]  
Header: Ce-Source=[/apis/v1/namespaces/50d38123af5/pingsources/ping-sub]  
Header: Ce-Specversion=[1.0]  
Header: Ce-Time=[2021-01-21T20:15:00.392503458Z]  
Header: Ce-Type=[dev.knative.sources.ping]  
Header: Content-Length=[24]  
Header: Content-Type=[application/json]  
Header: Forwarded=[for=172.30.118.174;proto=http, for=172.30.95.204]  
Header: K-Proxy-Request=[activator]  
Header: Traceparent=[00-1bf4b6b1d67f278a4b827e4e00f0cf7c-cbce9df0faedd812-00]  
Header: User-Agent=[Go-http-client/1.1]  
Header: X-B3-Sampled=[0]  
Header: X-B3-Spanid=[fb208eaa6af15ede]  
Header: X-B3-Traceid=[6db074fdaf6a6411fb208eaa6af15ede]  
Header: X-Envoy-Attempt-Count=[1]  
Header: X-Envoy-Decorator-Operation=[ping-app-snva7-1.50d38123af5.svc.cluster.local:80/*]  
Header: X-Envoy-Internal=[true]  
Header: X-Envoy-Peer-Metadata=[ChoKCkNMVVNURVJfSUQSDBoKS3ViZXJuZXRlcwo5CgxJTlNUQU5DRV9JUFMSKRonMTcyLjMwLjk1LjIwNCxmZTgwOjplODBiOjFkZmY6ZmVmMjo1ZjkxCpQCCgZMQUJFTFMSiQIqhgIKHQoDYXBwEhYaFGlzdGlvLWluZ3Jlc3NnYXRld2F5ChMKBWNoYXJ0EgoaCGdhdGV3YXlzChQKCGhlcml0YWdlEggaBlRpbGxlcgoZCgVpc3RpbxIQGg5pbmdyZXNzZ2F0ZXdheQofChFwb2QtdGVtcGxhdGUtaGFzaBIKGghkNzY1NjljOQoSCgdyZWxlYXNlEgcaBWlzdGlvCjkKH3NlcnZpY2UuaXN0aW8uaW8vY2Fub25pY2FsLW5hbWUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXkKLwojc2VydmljZS5pc3Rpby5pby9jYW5vbmljYWwtcmV2aXNpb24SCBoGbGF0ZXN0ChoKB01FU0hfSUQSDxoNY2x1c3Rlci5sb2NhbAotCgROQU1FEiUaI2lzdGlvLWluZ3Jlc3NnYXRld2F5LWQ3NjU2OWM5LWw5cHZoChsKCU5BTUVTUEFDRRIOGgxpc3Rpby1zeXN0ZW0KXQoFT1dORVISVBpSa3ViZXJuZXRlczovL2FwaXMvYXBwcy92MS9uYW1lc3BhY2VzL2lzdGlvLXN5c3RlbS9kZXBsb3ltZW50cy9pc3Rpby1pbmdyZXNzZ2F0ZXdheQo5Cg9TRVJWSUNFX0FDQ09VTlQSJhokaXN0aW8taW5ncmVzc2dhdGV3YXktc2VydmljZS1hY2NvdW50CicKDVdPUktMT0FEX05BTUUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXk=]  
Header: X-Envoy-Peer-Metadata-Id=[router~172.30.95.204~istio-ingressgateway-d76569c9-l9pvh.istio-system~istio-system.svc.cluster.local]  
Header: X-Forwarded-For=[172.30.118.174, 172.30.95.204, 172.30.163.42]  
Header: X-Forwarded-Proto=[http]  
Header: X-Request-Id=[ce502e5e-dd89-401e-a4cd-b72a6822f689]  
  
Body: {"mydata":"hello world"}  
```
{: screen}

For more information about headers and body, see [HTTP headers and body information for events](/docs/codeengine?topic=codeengine-subscribing-events#sub-header-body).

## Update your subscription
{: #update-subscription}
{: step}

Now that you know that your ping subscription is successful, you can update the ping event to run on a different schedule with the [`ibmcloud ce sub ping update`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-update) command. For example, update the subscription to run every day at midnight.
{: shortdesc}

```
ibmcloud ce sub ping update -n ping-sub -d ping-app --data '{"mydata":"hello world again"}' -s '0 0 * * *'
```
{: pre}

Run `ibmcloud ce sub ping get -n ping-sub` to find information about your subscription.

**Example output**

In this output, you can see the schedule and data are updated.

```
Getting ping event subscription 'ping-sub'...
OK

Name:          ping-sub  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           5m7s  
Created:       2021-03-14T13:21:13-05:00   

Destination:  App:ping-app  
Schedule:     0 0 * * *  
Data:         {"mydata":"hello world again"}  
Ready:        true

Events:    
  Type     Reason                 Age                Source                 Messages   
  Normal   FinalizerUpdate        65s                pingsource-controller  Updated "ping-sub" finalizers 
 
```
{: screen}

## Clean up
{: #clean-subscription}
{: step}

Ready to delete your ping subscription and your app? You can use the [`ibmcloud ce app delete`](/docs/codeengine?topic=codeengine-cli#cli-application-delete) and the [`ibmcloud ce sub ping delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-delete) commands.

To remove your subscription,

```
ibmcloud ce sub ping delete --name ping-sub
```
{: pre}

To remove your application,

```
ibmcloud ce app delete --name ping-app
```
{: pre}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
