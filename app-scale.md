---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-17"

keywords: application scaling in code engine, scaling http requests in code engine, concurrency in code engine applications, latency in code engine applications, throughput in code engine applications, scaling, latency, concurrency, app

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring application scaling 
{: #app-scale}

With {{site.data.keyword.codeenginefull}}, you don't need to think about scaling your application because the number of running instances of an application is automatically scaled up or down (to zero) based on incoming workloads. With automatic scaling, you don't pay for resources that are not used. 
{: shortdesc}

{{site.data.keyword.codeengineshort}} monitors the number of requests in the system and scales the application instances up and down to meet the load of incoming requests, including any HTTP connections to your application. These HTTP connections can be requests that come from outside of your project, from other workloads that are running in your project, or from event producers that you might be subscribed to, regardless of where those producers are located. {{site.data.keyword.codeengineshort}} automatically replicates application instances and configures the network infrastructure to load balance the requests across all instances.


## How scaling works
{: #app-how-scale}

{{site.data.keyword.codeengineshort}} monitors the number of requests in the system and scales the application instances, within the constraints of the application's concurrency settings.
{: shortdesc} 

To observe application scaling from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview), navigate to your specific application page. While the application is running, the number of running instances is `1` or greater based on the maximum number of instances that you specified. 
When the application handles fewer requests than its configured target concurrency, the application scales the number of running instances down to the configured minimum number of instances. If the minimum number of instances is set to `0` (default value), the application scales down to zero and the number of instances for the app reflects `0` instances. When the application is scaled down, and a request is routed to the application, {{site.data.keyword.codeengineshort}} scales up the application and routes the request to the newly created application instance.


For applications to be able to scale down cleanly, your application code must handle a SIGTERM signal. When {{site.data.keyword.codeengineshort}} automatically scales down, a SIGTERM signal is sent to your application. If your application does not handle the SIGTERM signal, then your app instances stay in `Terminating` status for the time that is configured by the request timeout value (default value is 300 seconds). After the duration of the request timeout, {{site.data.keyword.codeengineshort}} sends a SIGKILL signal to forcefully stop the app instances in `Terminating` status. 
{: important}

### Scaling boundaries
{: #app-scale-boundaries}

You can configure scaling boundaries by setting a range of values for the minimum and maximum number of instances within which {{site.data.keyword.codeengineshort}} autoscales the number of running instances of your application. Configure this range when you create or update applications. 
{: shortdesc} 


- Minimum number of instances -  The minimum number of instances of the app that are always running, even if no requests are processed. When set to `0` (default) {{site.data.keyword.codeengineshort}} removes all instances when no traffic is reaching the application. To always keep a running instance of your application, set this value greater than `0`. When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the minimum number of instances value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--min-scale` option on the **`app create`** and **`app update`** commands. 

- Maximum number of instances -  The maximum number of instances that can be running for the app. Autoscaling occurs up to this limit. If you set this value to `0`, the application scales as needed, and the app scaling is limited only by the instances per the resource quota for the project of your app. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the maximum number of instances value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--max-scale` option on the **`app create`** and **`app update`** commands. The default value for this option is `10`.

When you connect your applications to event producers, remember to account for the frequency and volume of the events from those producers when you set your scale boundaries. For example, if you expect to receive many events at the same time and the processing of each event can take several minutes, then you might need a higher maximum scale value than if each event can be quickly processed. If you set the value too low, you might experience delays in receiving events, or even dropped events due to timeouts while you wait for processing resources to be free.

### Autoscaling settings for concurrency and timing
{: #app-scale-timeconcurrency}

Use the following configuration settings to control application scaling.

- Concurrency -  This value indicates how many requests each instance of your app can process at one time. For example, a currency value of 100 means that your code can handle 100 concurrent requests at the same time. This value is a "hard limit", meaning that {{site.data.keyword.codeengineshort}} does not allow more than the number of requests (as specified with the concurrency setting) to reach any one instance of your application. Therefore, if your code is single threaded and can process only one request at a time, then consider setting concurrency to `1`. When the specified number of requests are sent to all running instances of your application, {{site.data.keyword.codeengineshort}} then increases the number of instances in preparation for more requests. When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the max concurrency value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--concurrency` option on the **`app create`** and **`app update`** commands.

- Target concurrency -  This value acts as a "soft limit" or number of requests per instance that you want in a loaded system. For example, if you specify `concurrency` as `100`, and you specify `target concurrency` as `70`, then {{site.data.keyword.codeengineshort}} tries to limit the number of requests per instance to 70. Specifying this option doesn't ensure that requests per instance won't go higher than 70 because it most likely will during an increase in traffic. However, the buffer between 70 and 100 enables the system to create new instances to bring the load per instance back down to 70 (or lower) per instance. If `target concurrency` is not specified, the default is the value of `concurrency`. When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the target concurrency value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--concurrency-target` option on the **`app create`** and **`app update`** commands. 

- Request timeout -  The amount of time, in seconds, that the application must respond to requests, or else they fail. When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the request timeout value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--request-timeout` option on the **`app create`** and **`app update`** commands. 

- Scale-down delay -  The amount of time, in seconds, that must pass at reduced concurrency before the application scales down. If you know the pattern of incoming requests to your application, you might choose to specify a value greater than the default of `0` to delay the scaling down of your application. If you use a high value for this option the average number of concurrently running application instances might increase, which incurs additional cost. Even with a scale-down delay setting of `0`, the system waits for a short amount of time before the application scales down the number of instances to ensure that a drop in request concurrency is stable enough to warrant a scale down. When you create or update an application with {{site.data.keyword.codeengineshort}} from the console, set the scale-down delay value in the Autoscaling section of the **Resources & scaling** tab. With the CLI, specify the `--scale-down-delay` option on the **`app create`** and **`app update`** commands. 

For example, if the maximum number of instances value is set to `10` and the concurrency is set to `100`, then an application can process 1000 concurrent requests before potential queuing of requests might occur. If you expect more than 1000 requests concurrently, then you might consider increasing the maximum number of instances value for your app. 

For more information about how {{site.data.keyword.codeengineshort}} works, see [IBM Cloud Code Engine: Optimizing Application Scaling, Latency, and Throughput](https://www.ibm.com/blog/ibm-cloud-code-engine-optimising-application-scaling-latency-and-throughput){: external}, and [Tuning IBM Cloud Code Engine Scale-Down Delay to Reduce Application Response Times](https://community.ibm.com/community/user/cloud/blogs/samuel-matzek1/2023/08/30/tuning-ibm-cloud-code-engine-scale-down-delay){: external}.

If you set the minimum number of instances equal to the maximum number of instances, then scaling does not occur and the target currency and scale-down delay values do not apply. However, the concurrency value is still in effect. 
{: tip}

### Example scenario for autoscaling 
{: #app-scale-example}

Suppose that you have an application that is configured with the following autoscaling settings. 
* Min number of instances = 4
* Max number of instances = 20
* Concurrency = 2 

With these settings, your app can process 2 concurrent requests at the same time. When there is no traffic, your application automatically scales down to 4 instances. The 4 instances can handle only 4 * 2 (currency) = 8 requests. The application can scale up to a maximum of 20 instances, such that the 20 instances can handle 20 * 2(currency) = 40 requests, assuming sufficient CPU and memory settings for the application. 

Suppose that your application is a static web application that requires 6 calls to your application to load a login page. Assume that 10 people log in to your application login page at the same time (10 * 6 = 60 calls). Because 60 calls ares greater than 40 requests that can be handled by your app, users of the application likely observe slowness as the calls are queued.  

After about a minute of no traffic against your app, {{site.data.keyword.codeengineshort}} starts to automatically scale down. When your application scales down, some instances are set in `Terminating` status. {{site.data.keyword.codeengineshort}} sends a SIGTERM signal to your application and your code must handle this signal and shut down. If your application does not handle this signal, your app instances stay in `Terminating` status for the time that is configured by the request timeout value (default value is 300 seconds). After the duration of the request timeout, {{site.data.keyword.codeengineshort}} sends a SIGKILL signal to forcefully stop the app instances in `Terminating` status. 

If you have 8 active instances and 12 instances stay in `Terminating` status for 300 seconds (5 minutes). These 12 instances do not receive any requests. If more than 8 * 2 (currency) = 16 requests come in, then {{site.data.keyword.codeengineshort}} scales up new instances.

In this example, the concurrency value of `2` is low for this static content. You must determine the autoscaling values to set for your app, which depends on what the implementation of your app can handle with its assigned CPU and memory resources. 



## Optimize latency and throughput
{: #app-optimize-latency}

To optimize your application latency and throughput, understand the pros and cons of some common models and best practices to configure the container concurrency.

Use the setting for concurrency to specify the maximum number of requests that can be processed concurrently per instance when you create or update an application. From the {{site.data.keyword.codeengineshort}} console, set the concurrency value in the Runtime section. With the CLI, use the `--concurrency` option (alias `--cn`) with the **`app create`** or **`app update`** command. 
{: shortdesc} 

| Model | Pros | Cons |
| --------- | -------- | -------- |    
| Single-concurrency, `--cn=1` | Choose the single concurrency configuration when the application serves a memory-intensive or CPU-intensive workload because only one request enters the application instance at a time and therefore gets the full amount of CPU and memory that is configured for the instance. | Applications that use the single-concurrency model scale-out quickly. The scale-out might introduce additional latency and lower throughput because it's more expensive to create a new application instance than to reuse an existing one. Do not choose this model if requests can be processed concurrently and latency is a critical aspect of the application. |
| High-concurrency, `--cn=100` (default) or higher | Choose this configuration if your application serves a high volume of HTTP request or response workloads that are not CPU-intensive or memory-intensive and can wait for resources. You might choose this concurrency configuration for an API back end that reads and writes data on create, retrieve, update, and delete operations to a remote database. While some requests wait on I/O, other requests can be processed without impacting overall latency and throughput. | This setting is not optimal when concurrent requests compete for CPU, memory, or I/O because competition for resources can delay execution and impact latency and throughput negatively. |
| Optimal concurrency, `--cn=N` | Choose the optimal concurrency configuration if you know the amount of resources that are required for a single request to meet the response time that you want for your application. You might choose this configuration if your app is a natural language translation application, where the machine learning model for the language conversion is `32` GB, and a single translation computation needs about `0.7` vCPU per request. You can choose a configuration of `9` vCPUs and `32` GB of memory per instance. The optimal container concurrency is about `13` (`9 vCPU/0.7 vCPU`). | Do not choose the optimal concurrency configuration if you do not know the resource requirements for your application. Setting the wrong container concurrency can lead to either too aggressive or too lazy scaling, which might impact the latency, error rate, and costs of your application. For more information, see [Determine concurrency for your application container](#app-determine-concurrency). |
| Infinite concurrency, `--cn=0` (disabled) | Disabled | The infinite concurrency configuration is not supported in {{site.data.keyword.codeengineshort}}. The infinite concurrency configuration forwards as many requests as possible to a single application instance, which can delay the scaling of additional application instances. |
{: caption="Examples concurrency in {{site.data.keyword.codeengineshort}} applications" caption-side="bottom"}

### Determining concurrency of your application container
{: #app-determine-concurrency}

The optimal container concurrency value is determined by the maximum number of concurrent requests that the application can handle with an acceptable request latency.
{: shortdesc} 

The container concurrency has a direct impact on the success rate, latency, and throughput of the application. When the container concurrency value is too high for the application to handle, the latency and throughput is impacted negatively, and you might observe `502` and `503` error responses. 

When the container concurrency value is too low for the application, the system scales out the application more quickly and spreads the request across many application instances, introducing additional costs and latency. During a burst of load, a low concurrency value can also lead to temporary `502` responses when the internal buffers of the system run over.

To determine the container concurrency configuration for your application, examine requests and latency.

1. Create an application and set its concurrency to `1000` (max) and both `min-scale` and `max-scale` to `1`.

    ```txt
    ibmcloud ce application create --name APPNAME --image APPIMAGE --min-scale=1 --max-scale=1 --concurrency=1000
    ```
    {: pre}

2. Start by sending a high rate of requests. If `502` errors occur, then decrease the rate until the result shows a 100% success rate.
3. Find the request latency of the output of Step 2. If the request latency is not acceptable, further decrease the request rate until the request latency looks acceptable. Note that the request duration is also important as it makes a difference if the computation of the request takes `2` seconds or `100` milliseconds. 

    Your acceptable request rate and latency varies according to your application characteristics and your scaling configuration. For example, if the computation within your application takes about 100 ms and your concurrency setting is 10 one application instance is able to process around 100 requests per second with a latency of about 100 ms (ignoring network latency).
4. To calculate the container concurrency value for your application, take the *rate* from Step 2 (in `req/s`) and divide by the *latency* of Step 3 (in seconds): `CC = RATE/LATENCY`. For example, if the rate is `80` requests per second and the latency is `2` seconds, the resulting concurrency is concurrency = `80 req/s / 2 s = 40`.
5. Update the application to set the container concurrency to the value that you found in the previous step and rerun the workload to check whether the success rate and latency are acceptable.
6. Experiment with the application by increasing the container concurrency value and observing the success rate and latency.
7. Update your application with the optimal container concurrency value and remove the `min-Scale` and `max-scale` boundaries to allow the application to scale automatically.

## Observing how your app scales with the CLI
{: #scale-app-cli}

You can observe the number of running instances of your app with the CLI.
{: shortdesc} 


1. Create an application with the **`app create`** command.

    ```txt
    ibmcloud ce application create --name myapp --image icr.io/codeengine/helloworld
    ```
    {: pre}

2. Call the application. You can obtain the URL of your app from the output of the **`app create`** command, or you can run `ibmcloud ce app get --name myapp --output url`.

    ```txt
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

3. Run the **`application get`** command to display the status of your application. Look for the value for `Running instances`. In this example, the app has `1` running instance. For example,

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output

    ```txt
    [...]
    OK

    Name:          myapp
    [...]

    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Status Summary:  Application deployed successfully

    Image:                icr.io/codeengine/helloworld
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
    myapp-ds8fn-1:
        Age:                6m25s
        Traffic:            100%
        Image:              icr.io/codeengine/helloworld (pinned to fe0446)
        Running Instances:  1

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  0
        Timeout:        300

    Conditions:
        Type                 OK    Age    Reason
        ConfigurationsReady  true  6m10s
        Ready                true  5m56s
        RoutesReady          true  5m56s

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  6m28s  service-controller  Created Configuration "myapp"
        Normal  Created  6m28s  service-controller  Created Route "myapp"

    Instances:
        Name                                       Revision       Running  Status   Restarts  Age
        myapp-ds8fn-1-deployment-79bdd76749-khtmw  myapp-ds8fn-1  2/2      Running  0         32s
    ```
    {: screen}

    Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
    {: note}

4. Run the **`application get`** command again and notice that the value for `Running instances` scaled to zero. When the application handles fewer requests than its configured target concurrency, the application scales the number of running instances down to the configured minimum number of instances. In this scenario, the number of running instances automatically scales to zero. When the `--min-scale` option is set to `0` (default value), then the number of running instances automatically scales to zero.

    Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
    {: note}

    ```txt
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    Example output

    ```txt
    OK

    Name:          myapp
    [...]

    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Image:                icr.io/codeengine/helloworld
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
    myapp-ds8fn-1:
        Age:                12m
        Traffic:            100%
        Image:              icr.io/codeengine/helloworld (pinned to 548d5c)
        Running Instances:  0

    Runtime:
        Concurrency:         100
        Maximum Scale:       10
        Minimum Scale:       0
        Timeout:             300

    Conditions:
        Type                 OK    Age    Reason
        ConfigurationsReady  true  3m7s
        Ready                true  2m54s
        RoutesReady          true  2m54s

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  3m21s  service-controller  Created Configuration "myapp"
        Normal  Created  3m20s  service-controller  Created Route "myapp"
    ```
    {: screen}

5. Call the application again to scale from zero.

    ```txt
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

6. Run the **`application get`** command again and notice that the value for `Running instances` scaled up from zero. For example,

    ```txt
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    Example output

    ```txt
    OK

    Name:          myapp
    [...]

    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Status Summary:     Application deployed successfully  

    Environment Variables:    
    Type     Name          Value  
    Literal  CE_APP        myapp  
    Literal  CE_DOMAIN     us-south.codeengine.appdomain.cloud  
    Literal  CE_SUBDOMAIN  glxo4k7nj7d  
    Image:                  icr.io/codeengine/helloworld  
    Resource Allocation:      
    CPU:                1  
    Ephemeral Storage:  400M  
    Memory:             4G  

    Revisions:     
    myapp-00001:    
        Age:                42s  
        Latest:             true  
        Traffic:            100%  
        Image:              icr.io/codeengine/helloworld (pinned to 1cee99)  
        Running Instances:  1  

    Runtime:       
    Concurrency:       100  
    Maximum Scale:     10  
    Minimum Scale:     0  
    Scale Down Delay:  0  
    Timeout:           300  

    Conditions:    
    Type                 OK    Age  Reason  
    ConfigurationsReady  true  25s    
    Ready                true  12s    
    RoutesReady          true  12s    

    Events:        
    Type    Reason   Age  Source              Messages  
    Normal  Created  44s  service-controller  Created Configuration "myapp"  
    Normal  Created  43s  service-controller  Created Route "myapp"  

    Instances:     
    Name                                    Revision     Running  Status   Restarts  Age  
    myapp-00001-deployment-d59b87654-xkqh7  myapp-00001  3/3      Running  0         43s 
    ```
    {: screen}

## Setting the number of minimum and maximum instances for your app
{: #scale-app-min-max}

You can change the number of running instances of your app by updating the minimum and maximum value for the number of app instances.
{: shortdesc}

The default value for the minimum number of instances for your application is `0`. If your app does not receive any traffic, it scales to `0` and no instances of your app are running. In this situation, your application can be slower to respond when it receives traffic again, while it scales back up. You can change this behavior by updating your application and setting the minimum scale to `1` either in the console or from the CLI.

The default value for the maximum number of instances for your app is `0`, which allows your app to scale as needed. For more information, see [Scaling boundaries](#app-scale-boundaries).

### Changing the autoscaling range from the console
{: #set-app-instances-ui}

To change the range within which {{site.data.keyword.codeengineshort}} autoscales the number of running instances for an app from the console, follow these steps.

1. Navigate to your app.
2. Select the **Configuration** tab.
4. Select the **Resources & scaling** tab.
5. Set the number for minimum and maximum instances for your app.
6. (Optional) Review and set the request concurrency and timing settings for autoscaling your app. 
7. Click **Deploy** to save your changes and deploy the app revision.

When you update your application, your app creates a new revision and routes traffic to that instance.

### Changing the autoscaling range with the CLI
{: #set-app-instances-cli}

To change the range within which {{site.data.keyword.codeengineshort}} autoscales the number of running instances for an app with the CLI, run the [**`application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command with the `--min-scale` and `--max-scale` options set to the number of instances that you want for your app. You can optionally set request concurrency and timing settings for your app. These options include `--concurrency`, `--concurrency-target`, `--request-timeout`, and `--scale-down-delay`. For more information about setting these autoscaling values, see [Scaling boundaries](#app-scale-boundaries), and [Autoscaling settings for concurrency and timing](#app-scale-timeconcurrency).

When you update your application, your app creates a new revision and routes traffic to that instance.



