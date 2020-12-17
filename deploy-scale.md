---

copyright:
  years: 2020
lastupdated: "2020-12-15"

keywords: code engine, application, app, http requests

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


# Configuring application scaling
{: #app-scale}

With {{site.data.keyword.codeengineshort}}, you don't need to think about scaling because the number of running instances of an application is automatically scaled up or down (to zero) based on incoming workloads. With automatic scaling, you don't pay for resources that are not used. 
{: shortdesc} 

To observe application scaling from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview), navigate to your running application and click **Instances**. While the application is running, the number of running instances is `1` or greater based on the maximum number of instances setting that you specified. When the application is finished running, the number of running instances scales down the minimum number of instances setting. If the minimum number of instances is set to `0`, the application scales to zero. 

## Concurrency values
{: #app-concurrency}

To control the concurrency-per-application revision, you can set the concurrency value in the **Runtime** section when you create or update an application. In the CLI, you can configure the concurrency using the `--concurrency` option when you create or update applications with the `ibmcloud ce app create` or `ibmcloud ce app update` commands. The API specification allows you to set the `containerConcurrency` on the revision template. For more information, see the [revision specification documentation](https://github.com/knative/docs/blob/master/docs/serving/spec/knative-api-specification-1.0.md#revision-2){: external}.
{: shortdesc} 

Setting the container concurrency (cc) configuration enforces an upper bound of requests to be processed within an application instance. If concurrency reaches this limit, subsequent requests will be buffered and must wait until enough capacity is free to execute the requests. Additional capacity might get freed up through the completion of requests or the scaling up of additional application instances.

## How scaling works
{: #app-how-scale}

The autoscaler (powered by Knative) monitors the number of requests in the system and scales the application instances up and down in order to meet the application's concurrency setting. The autoscaler can scale applications to zero when no requests are reaching the application. In this case, no instance are running and no costs are incurred. If the application is scaled to zero and a request is routed to the application, the autoscaler scales the application up from zero and routes the request to the newly created application instance. The system uses an internal buffer to queue the requests until the application instance is ready to serve the requests.
{: shortdesc} 

Internally, the autoscaler introduces a `60` second sliding window and scales the application to meet the concurrency on average over that sliding window. As the request rate can be very dynamic and can change significantly, for example, a burst of requests, the autoscaler begins to scale up when 70% of the container concurrency is observed. If you specify a container concurrency of `10`, the autoscaler adds an additional application instance when 7 requests on average are observed over the period of `60` seconds.

In case of a very significant increase in the request rate, the autoscaler's feedback loop is reduced to `6` seconds, and the scaling policy is much more aggressive. When 200% of the container concurrency is observed, the autoscaler scales up more quickly in order to meet the 70% of container concurrency within the `6` second window. If you configure a container concurrency of `10`, the `6` second scaling policy begins when 20 requests are observed in the system.

For more information about how the autoscaler works, see [IBM Cloud Code Engine: Optimising Application Scaling, Latency, and Throughput](https://www.ibm.com/cloud/blog/ibm-cloud-code-engine-optimising-application-scaling-latency-and-throughput){: external}.

## Scaling boundaries
{: #app-scale-boundaries}

You can configure scaling boundaries for the autoscaler, by using `--min-scale` and `--max-scale` options when you create or update applications.
{: shortdesc} 

- `--min-scale`: The minimum number of application instances to keep running. When set to `0` (default) the autoscaler removes all instances when no traffic is reaching the application. 
- `--max-scale`: The maximum number of application instances that can run. The autoscaler does not scale up beyond that value.

## Optimize latency and throughput
{: #app-optimize-latency}

In order to optimize your application latency and throughput, understand the pros and cons of some common models and best practices to configure the container concurrency (cc).
{: shortdesc} 

| Model | Pros | Cons |
| --------- | -------- | -------- |	
| Single-concurrency, `--cn=1` | Choose the single concurrency configuration when the application serves a memory-intensive or CPU-intensive workload because only one request enters the application instance at a time and therefore gets the full amount of CPU and memory configured for the instance. | Applications that use the single-concurrency model scale out quickly. The scale-out might introduce additional latency and lower throughput, because it's more expensive to create a new application instance than to reuse an existing one. Do not choose this model if requests can be processed concurrently and latency is a critical aspect of the application. |
| High-concurrency, `--cn=100` (default) or higher | Choose this configuration if your application serves a high volume of HTTP request or response workloads that are not CPU-intensive or memory-intensive and can wait for resources. You might choose this concurrency configuration for an API back end that reads and writes data on CRUD operations to a remote database. While some requests wait on I/O, other requests can be processed without impacting overall latency and throughput. | This setting is not optimal when concurrent requests compete for CPU, memory, or I/O because competition for resources can delay execution and impact latency and throughput negatively. |
| Optimal concurrency, `--cn=N` | Choose the optimal concurrency configuration if you know the amount of resources that are required for a single request to meet the response time that you want for your application. You might choose this configuration if your app is a natural language translation application, where the machine learning model for the language translation is `32` GB, and a single translation computation needs about `0.7` vCPU per request. You can choose a configuration of `9` vCPUs and `32` GB of memory per instance. The optimal container concurrency is about `13` (`9 vCPU/0.7 vCPU`). | Do not choose the optimal concurrency configuration if you do not know the resource requirements for your application. Setting the wrong container concurrency can lead to either too aggressive or too lazy scaling, which may impact the latency, error rate, and costs of your application. For more information, see [Determine concurrency for your application container](#app-determine-concurrency). |
| Infinite concurrency, `--cn=0` (disabled) | Disabled | The infinite concurrency configuration is not supported in {{site.data.keyword.codeengineshort}}. The infinite concurrency configuration forwards as many requests as possible to a single application instance, which can delay the scaling of additional application instances. |
{: caption="Examples concurrency in {{site.data.keyword.codeengineshort}} applications" caption-side="top"}

### Determining concurrency of your application container
{: #app-determine-concurrency}

The optimal container concurrency value is determined by the maximum number of concurrent requests the application can handle with an acceptable request latency.
{: shortdesc} 

The container concurrency (cc) has a direct impact on the success rate, latency, and throughput of the application. When the container concurrency value is too high for the application to handle, the latency and throughput is impacted negatively and you might observe `502` and `503` error responses. 

When the container concurrency value is too low for the application, the system scales out the application more quickly and spreads the request across many application instances, introducing additional costs and latency. During a burst of load, a low concurrency value can also lead to temporary `502` responses when the internal buffers of the system run over.

To determine the container concurrency configuration for your application, examine requests and latency.

1. Create an application and set its concurrency to `1000` (max) and both `minScale` and `maxScale` to `1`.

   ```
   ibmcloud ce application create -name APPNAME --image APPIMAGE --min-scale=1 --max-scale=1 --concurrency=1000
   ```
   {: pre}
   
2. Start by sending a high rate of requests. If there are `502` errors, then decrease the rate until the result shows a 100% success rate.
3. Find the request latency of the output of Step 2. If the request latency is not acceptable, further decrease the request rate until the request latency looks acceptable. Note that the request duration is also important as it makes a difference if the computation of the request takes `2` seconds or `100` milliseconds. 

   Your acceptable request rate and latency varies according to your application characteristics and your scaling configuration. For example, if the computation within your application takes about 100 ms and your concurrency setting is 10 one application instance is able to process around 100 requests per second with a latency of about 100 ms (ignoring network latency).
4. To calculate the container concurrency value for your application, take the *rate* from Step 2 (in `req/s`) and divide by the *latency* of Step 3 (in seconds): `CC = RATE/LATENCY`. For example, if the rate is `80` requests per second and the latency is `2` seconds, the resulting concurrency is concurrency = `80 req/s / 2 s = 40`.
5. Update the application to set the container concurrency to the value that you found in the previous step and rerun the workload to check whether the success rate and latency are acceptable.
6. Experiment with the application by increasing the container concurrency value and observing the success rate and latency.
7. Update your application with the optimal container concurrency value and remove the `minScale` and `maxScale` boundaries to allow the application to scale automatically.
  
## Scaling your application with the CLI
{: #scale-app-cli}

You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options by using the `application create` or `application update` command.
{: shortdesc} 

To observe application scaling from the {{site.data.keyword.codeengineshort}} CLI,

1. Create an application with the `app create` command.

   ```
   ibmcloud ce application create -name myapp --image docker.io/ibmcom/helloworld
   ```
   {: pre}

2. Call the application. 

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

3. Run the `application get` command to display the status of your application. Look for the value for `Running instances`. In this example, the app has `1` running instance. For example,

    ```
    ibmcloud ce application get -name myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
      Age:                46s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  30s
      Ready                true  27s
      RoutesReady          true  27s

   Instances:
   Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-1-deployment-75b46dcf64-jp8fp  2/2      Running  0         80s
      myapp-a5yp2-2-deployment-65766594d4-qp8sv  2/2      Running  0         47s
   ```
   {: screen}

  Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
  {: note}

4. Run the `application get` command again and notice that the value for `Running instances` scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value. For example,

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
    Age:                12m
    Traffic:            100%
    Image:              ibmcom/hello (pinned to 548d5c)
    Running Instances:  0

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  10m
      Ready                true  10m
      RoutesReady          true  10m

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-2-deployment-65766594d4-lnpgk  1/2      Running  0         5m38s
   ```
   {: screen}

5. Call the application again to scale from zero:

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

6. Run the `application get` command again and notice that the value for `Running instances` scaled up from zero. For example,

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]
 
   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
      Age:                13m
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  13m
      Ready                true  13m
      RoutesReady          true  13m

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-2-deployment-65766594d4-hj6c5  2/2      Running  0         22s
   ```
   {: screen}
