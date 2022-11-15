---

copyright:
  years: 2022
lastupdated: "2022-11-15"

keywords: subscription tutorial for code engine, eventing and code engine, subscriptions, tutorial for code engine, eventing tutorial for code engine, subscription, ping, cron, app, event, cron event, ping event

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Subscribing to cron events
{: #subscribe-cron-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, you can learn how to subscribe to cron events by using the {{site.data.keyword.codeenginefull}} CLI.
{: shortdesc}

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Determine your cron interval
{: #determine-cron-interval}
{: step}

The cron event producer generates events at regular intervals. This interval can be scheduled by minute, hour, day, or month or a combination of several different time intervals.
{: shortdesc}

Cron uses a standard crontab to specify interval details, in the format `* * * * *`, which stands for minute, hour, day of month, month, and day of week. For example, to schedule an event for midnight, specify `0 0 * * *`.  To schedule an event for every Friday at midnight, specify `0 0 * * FRI`.

For more information about crontab, see [CRONTAB](http://crontab.org/){: external}.

You can set your cron interval by using the `--schedule` option with the **`subscription cron`** command, as shown in Step 3. If you do not specify the `--schedule` option, then by default, the cron event is sent every minute of every day.

## Create your app (or job)
{: #create-app}
{: step}

While events can be used to trigger apps or jobs, this tutorial uses an app. 
{: shortdesc}

Create your application called `cron-app` with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. This app pulls an image that is called `icr.io/codeengine/cron`. This app logs each event as it arrives, showing the full set of HTTP Headers and HTTP Body payload. For more information about the code that is used for this example, see [`cron`](https://github.com/IBM/CodeEngine/tree/main/cron){: external}.

```txt
ibmcloud ce app create --name cron-app --image icr.io/codeengine/cron 
```
{: pre}

Run `ibmcloud ce application get --name cron-app` to verify that your app is in a `Ready` state.

You can find more information about this app at [cron readme file](https://github.com/IBM/CodeEngine/tree/main/cron){: external}.

## Create a subscription
{: #create-subscription}
{: step}

After your app is ready, create a subscription to the cron event producer and connect it to your app with the [**`ibmcloud ce sub cron create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create) command.
{: shortdesc}

The following example creates a cron subscription that is called `cron-sub` and specifies the `cron-app` application as its destination. The subscription uses the `--data` option to include a JSON string in the cron event. It also specifies the cron schedule by using the `--schedule` option with a value of `* * * * *` to send an event every minute of every day to the `cron-app` application.

```txt
ibmcloud ce sub cron create --name cron-sub --destination cron-app --data '{"mydata":"hello world"}' --schedule '* * * * *'
```
{: pre}

Run `ibmcloud ce sub cron get -n cron-sub` to find information about your subscription.

Example output

In this output, you can see that the subscription name, destination, schedule, and data are correct.

```txt
Getting cron event subscription 'cron-sub'...
OK

Name:          cron-sub  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           2m18s  
Created:       2021-03-14T13:21:13-05:00   

Destination Type:  app  
Destination:       cron-app  
Schedule:          * * * * *  
Time Zone:         UTC  
Data:              {"mydata":"hello world"}  
Ready:             true  

Events:    
    Type     Reason                 Age                Source                 Messages   
    Normal   FinalizerUpdate        65s                pingsource-controller  Updated "cron-sub" finalizers 

```
{: screen}

## Testing your subscription
{: #test-subscription}
{: step}

After you successfully subscribed your app to your cron event, look at the logs to see whether it works.
{: shortdesc}

Get the logs for the app with the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command. 

```txt
ibmcloud ce app logs --name cron-app
```
{: pre}

Example output

In the following output, you can see that the date and time that the event was received as well as the HTTP Headers and the HTTP Body JSON that was passed in when the subscription was created.

```txt
2021-01-21 20:15:00 - Received:  
Header: Accept-Encoding=[gzip]  
Header: Ce-Id=[7de01e8e-84dc-4409-ad56-90d6e391397c]  
Header: Ce-Source=[/apis/v1/namespaces/50d38123af5/pingsources/cron-sub]  
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
Header: X-Envoy-Decorator-Operation=[cron-app-snva7-1.50d38123af5.svc.cluster.local:80/*]  
Header: X-Envoy-Internal=[true]  
Header: X-Envoy-Peer-Metadata=[ChoKCkNMVVNURVJfSUQSDBoKS3ViZXJuZXRlcwo5CgxJTlNUQU5DRV9JUFMSKRonMTcyLjMwLjk1LjIwNCxmZTgwOjplODBiOjFkZmY6ZmVmMjo1ZjkxCpQCCgZMQUJFTFMSiQIqhgIKHQoDYXBwEhYaFGlzdGlvLWluZ3Jlc3NnYXRld2F5ChMKBWNoYXJ0EgoaCGdhdGV3YXlzChQKCGhlcml0YWdlEggaBlRpbGxlcgoZCgVpc3RpbxIQGg5pbmdyZXNzZ2F0ZXdheQofChFwb2QtdGVtcGxhdGUtaGFzaBIKGghkNzY1NjljOQoSCgdyZWxlYXNlEgcaBWlzdGlvCjkKH3NlcnZpY2UuaXN0aW8uaW8vY2Fub25pY2FsLW5hbWUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXkKLwojc2VydmljZS5pc3Rpby5pby9jYW5vbmljYWwtcmV2aXNpb24SCBoGbGF0ZXN0ChoKB01FU0hfSUQSDxoNY2x1c3Rlci5sb2NhbAotCgROQU1FEiUaI2lzdGlvLWluZ3Jlc3NnYXRld2F5LWQ3NjU2OWM5LWw5cHZoChsKCU5BTUVTUEFDRRIOGgxpc3Rpby1zeXN0ZW0KXQoFT1dORVISVBpSa3ViZXJuZXRlczovL2FwaXMvYXBwcy92MS9uYW1lc3BhY2VzL2lzdGlvLXN5c3RlbS9kZXBsb3ltZW50cy9pc3Rpby1pbmdyZXNzZ2F0ZXdheQo5Cg9TRVJWSUNFX0FDQ09VTlQSJhokaXN0aW8taW5ncmVzc2dhdGV3YXktc2VydmljZS1hY2NvdW50CicKDVdPUktMT0FEX05BTUUSFhoUaXN0aW8taW5ncmVzc2dhdGV3YXk=]  
Header: X-Envoy-Peer-Metadata-Id=[router~172.30.95.204~istio-ingressgateway-d76569c9-l9pvh.istio-system~istio-system.svc.cluster.local]  
Header: X-Forwarded-For=[172.30.118.174, 172.30.95.204, 172.30.163.42]  
Header: X-Forwarded-Proto=[http]  
Header: X-Request-Id=[ce502e5e-dd89-401e-a4cd-b72a6822f689]  

Body: {"mydata":"hello world"}  
```
{: screen}

For more information about headers and body, see [HTTP headers and body information for cron events](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron).

For more information about viewing logs with the CLI, see [Viewing logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-logs-cli).

Note that subscriptions can affect how an application scales. For more information, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

## Update your subscription
{: #update-subscription}
{: step}

Now that you know that your cron subscription is successful, you can update the cron event to run on a different schedule with the [**`ibmcloud ce sub cron update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-update) command. For example, update the subscription to run every day at midnight.
{: shortdesc}

```txt
ibmcloud ce sub cron update -n cron-sub -d cron-app --data '{"mydata":"hello world again"}' -s '0 0 * * *'
```
{: pre}

Run the `ibmcloud ce sub cron get -n cron-sub` command to find information about your subscription.

Example output

In this output, you can see that the schedule and data are updated.

```txt
Getting cron event subscription 'cron-sub'...
OK

Name:          cron-sub  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           5m7s  
Created:       2021-03-14T13:21:13-05:00   

Destination:  App:cron-app  
Schedule:     0 0 * * *  
Data:         {"mydata":"hello world again"}  
Ready:        true

Events:    
    Type     Reason                 Age                Source                 Messages   
    Normal   FinalizerUpdate        65s                pingsource-controller  Updated "cron-sub" finalizers 

```
{: screen}

## Clean up for cron subscription tutorial
{: #clean-subscription}
{: step}

Ready to delete your cron subscription and your app? You can use the [**`ibmcloud ce app delete`**](/docs/codeengine?topic=codeengine-cli#cli-application-delete) and the [**`ibmcloud ce sub cron delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-delete) commands.

To remove your subscription,

```txt
ibmcloud ce sub cron delete --name cron-sub
```
{: pre}

To remove your application,

```txt
ibmcloud ce app delete --name cron-app
```
{: pre}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


