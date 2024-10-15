---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-15"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps, app instances

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging apps 
{: #troubleshoot-apps}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} applications.
{: shortdesc}

When your app isn't behaving as expected, looking at logs and system events can provide information that might help you debug the problem. 

## App limits to consider 
{: #ts-app-limits}

The maximum number of apps that you can create per project is 40. You are limited to a total of 120 revisions for all apps per project. {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. See [Updating apps](/docs/codeengine?topic=codeengine-update-app).

For more information about limits for apps, including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

With the CLI, you can use the [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to display information about limits and current usage. For example:

```txt
ibmcloud ce project create --name myproject
```
{: pre}

Example output

```txt
Getting project 'myproject'...
OK

Name:                                      myproject
ID:                         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:                                    active
Enabled:                                   true
Application Private Visibility Supported:  true
Selected:                                  true
Region:                                    us-south
Resource Group:             default
Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
Age:                        52d
Created:                                   Tue, 28 Sep 2021 05:12:16 -0500
Updated:                                   Tue, 28 Sep 2021 05:12:19 -0500

Quotas:
Category                                  Used  Limit
App revisions                             2    120
Apps                                      1     40
Build runs                                1     100
Builds                                    2     100
Configmaps                                2     100
CPU                                       0     128
Ephemeral storage                         0     512G
Functions                                 0     20
Instances (active)                        0     250
Instances (total)                         0     2500
Job runs                                 13     100
Jobs                                      2     100
Memory                                    0     512G
Secrets                                   6     100
Subscriptions (cron)                      0     100
Subscriptions (IBM Cloud Object Storage)  0     100
Subscriptions (Kafka)                     0     100
```
{: screen}


## Confirm port value 
{: #ts-app-port}

{{site.data.keyword.codeengineshort}} requires that you have an HTTP endpoint that {{site.data.keyword.codeengineshort}} uses to check the health of your app.

By default, {{site.data.keyword.codeengineshort}} assumes that apps listen for incoming connections on port `8080`. In addition, Code Engine sets the `PORT` environment variable to the port value that the application is expected to be listening on. If your app needs to listen on a port other than port `8080`, either deploy your app from the console and specify the correct port or use the `--port` option on the **`app create`** command. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars). The following ports are reserved by {{site.data.keyword.codeengineshort}}:  `8022`, `8008`, `8012`, `9090`, `9091`, and `15090`. Only one port can be exposed as the listening port.



## Getting logs for my apps 
{: #ts-app-gettinglogs}

Logs can be helpful to troubleshoot problems when you run apps. You can view app logs from the console or with the CLI. 
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.logs_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} app. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your apps. You can view app logs after you add logging capabilities. For more information, see [viewing app logs from the console](/docs/codeengine?topic=codeengine-codeengine-logging&interface=ui#view-appjobfunctionlogs-ui).

When you work with the CLI, you can display logs for all the instances of an app or display logs of a specific instance of an app. 

1. Use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all your defined apps in your project; for example,

    ```txt
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,

    ```txt
    ibmcloud ce app get --name myapp  
    ```
    {: pre}

    Example output 

    ```txt
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    Name:          myapp
    [...]

    Created:       2021-02-23T07:32:16-05:00
    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Status Summary:  Application deployed successfully

    Image:                icr.io/codeengine/hello
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
        myapp-atfte-2:
        Age:                51s
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to e69c88)
        Running Instances:  2

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  2
        Timeout:        300

    Conditions:
        Type                 OK    Age  Reason
        ConfigurationsReady  true  36s
        Ready                true  10s
        RoutesReady          true  10s

    Instances:
        Name                                       Revision       Running  Status   Restarts  Age
        myapp-atfte-2-deployment-7cb45cdf67-qc7sb  myapp-atfte-2  2/2      Running  0         52s
        myapp-atfte-2-deployment-7cb45cdf67-sp9fr  myapp-atfte-2  2/2      Running  0         52s
    ```
    {: screen}

    If you want more fine-grained details about your app, use the `--o yaml` option with the **`app get`** command; for example, `ibmcloud ce app get --name myapp --o yaml`. This option is useful to show more detailed information in the CLI for the app.
    {: tip}

3. Display the logs of instances of your app. 

    * To display the logs of a specific instance of your app, use the [**`ibmcloud ce app logs --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,

        ```txt
        ibmcloud ce app logs --instance myapp-atfte-2-deployment-7cb45cdf67-qc7sb
        ```
        {: pre} 

        Example output 

        ```txt
        Getting logs for application instance 'myapp-atfte-2-deployment-7cb45cdf67-qc7sb'...
        OK

        myapp-atfte-2-deployment-7cb45cdf67-qc7sb/user-container:
        Server running at http://0.0.0.0:8080/
        ```
        {: screen}

    * To display the logs for all the instances of your app, use the [**`app logs --application APP_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,

        ```txt
        ibmcloud ce app logs --app myapp 
        ```
        {: pre} 

        Example output 

        ```txt
        Getting logs for all instances of application 'myapp'...
        OK

        myapp-atfte-2-deployment-7cb45cdf67-qc7sb/user-container:
        Server running at http://0.0.0.0:8080/

        myapp-atfte-2-deployment-7cb45cdf67-sp9fr/user-container:
        Server running at http://0.0.0.0:8080/
        ```
        {: screen}

For more information, see [Viewing application logs with the CLI](/docs/codeengine?topic=codeengine-codeengine-logging&interface=cli#view-applog-cli).


## Getting details about app instances 
{: #ts-app-instancedetails}

With the {{site.data.keyword.codeengineshort}} console, you can view details of all your app instances. Details of your app instances are useful if you receive a warning message about instances of your app. Or, perhaps your app is in a ready status but the app is not working correctly as it is not serving requests.

For details of app instances, go to the application page. From the application page, you can go to the **Instances** tab and review current instances of the application. The set of instances changes as your application is scaled up and down, based on the [scaling configuration](/docs/codeengine?topic=codeengine-app-scale). Use the information about the app instances to help with troubleshooting your app.

The restart count is the number of times that the user container was restarted since the specific instance was created. The restart rate value is considered high if the average number of user container restarts since the instance was created is 3 or more times per day. 

As needed, use filters to help you narrow the results for your app instances. You can choose to filter on the name of the app revision or the status of the app instance.

You can review details of a specific app instance for a deeper look. To open the instance details page for a specific instance, take one of the following actions.

* Click in the row of the instance that you want.
* Click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **Instance details** to view details of the specified instance.

Use the additional information on the instance details page to help you troubleshoot your app. You can use the information about start and restart times, exit code and reason code information, container status, and the last log messages to help you in debugging your app. A user container includes your running code (the image you specified when you created the app). Whereas a system container handles system tasks such as forwarding requests to the user container or collecting metrics. 

The following scenarios are examples for when you might use details of the specific app instance to help you troubleshoot your app.

* If the app is in ready status but the app is not serving HTTP requests, then view details of specific app instances to learn about reasons why the app instance is not serving HTTP requests.
* If you have an instance that is in `failed` status, perhaps the image for the application is not valid or not available. 
* If the restart count for an instance is high, perhaps your application failed because of a programming error, the ephemeral storage limit was reached, or an out of memory condition occurs. When this scenario happens, the instance is continually stopped and restarted. The last restart time information might help you determine whether the app instance has an ongoing problem that causes restarts, or if the problem is infrequent.


## Getting system event information for my apps 
{: #ts-app-gettingevent}

System event information can be helpful to troubleshoot problems when you run apps. You can view system event information with the CLI.  
{: shortdesc}

You can display system events for all the instances of an app or display system events of a specific instance of an app. 

1. Use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all your defined apps; for example,

    ```txt
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,

    ```txt
    ibmcloud ce app get --name myapp  
    ```
    {: pre}

    Example output 

    ```txt
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    Name:          myapp
    [...]

    Created:       2021-02-23T07:32:16-05:00
    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Status Summary:  Application deployed successfully

    Image:                icr.io/codeengine/hello
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
        myapp-atfte-2:
        Age:                51s
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to e69c88)
        Running Instances:  2

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  2
        Timeout:        300

    Conditions:
        Type                 OK    Age  Reason
        ConfigurationsReady  true  36s
        Ready                true  10s
        RoutesReady          true  10s

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  3m55s  service-controller  Created Configuration "myapp"
        Normal  Created  3m54s  service-controller  Created Route "myapp"

    Instances:
        Name                                       Revision       Running  Status   Restarts  Age
        myapp-atfte-2-deployment-7cb45cdf67-qc7sb  myapp-atfte-2  2/2      Running  0         52s
        myapp-atfte-2-deployment-7cb45cdf67-sp9fr  myapp-atfte-2  2/2      Running  0         52s
    ```
    {: screen}

    If you want more fine-grained details about your app, use the `--o yaml` option with the **`app get`** command; for example, `ibmcloud ce app get --name myapp --o yaml`. This option is useful to show more detailed information in the CLI for the app.
    {: tip}

3. Display the system events of instances of your app. 

    * To display the events of a specific instance of your app, use the [**`ibmcloud ce app events --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,

        ```txt
        ibmcloud ce app events --instance myapp-atfte-2-deployment-7cb45cdf67-qc7sb
        ```
        {: pre} 

        Example output 

        ```txt
        Getting events for application instance 'myapp-atfte-2-deployment-7cb45cdf67-qc7sb'...
        OK

        myapp-atfte-2-deployment-7cb45cdf67-qc7sb:
        Type    Reason     Age  Source                 Messages
        Normal  Scheduled  46m  default-scheduler      Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-qc7sb to 10.240.64.20
        Normal  Pulling    45m  kubelet, 10.240.64.20  Pulling image "index.icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
        Normal  Pulled     45m  kubelet, 10.240.64.20  Successfully pulled image "index.icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.64261536s
        Normal  Created    45m  kubelet, 10.240.64.20  Created container user-container
        [...]
        ```
        {: screen}

    * To display events for all the instances of your app, use the [**`ibmcloud ce app events --application APP_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,

        ```txt
        ibmcloud ce app events --app myapp 
        ```
        {: pre} 

        Example output 

        ```txt
        Getting events for all instances of application 'myapp'...
        OK

        myapp-atfte-2-deployment-7cb45cdf67-qc7sb:
        Type    Reason     Age  Source                 Messages
        Normal  Scheduled  47m  default-scheduler      Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-qc7sb to 10.240.64.20
        Normal  Pulling    47m  kubelet, 10.240.64.20  Pulling image "icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
        Normal  Pulled     47m  kubelet, 10.240.64.20  Successfully pulled image "icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.64261536s
        Normal  Created    46m  kubelet, 10.240.64.20  Created container user-container
        Normal  Started    46m  kubelet, 10.240.64.20  Started container user-container
        [...]

        myapp-atfte-2-deployment-7cb45cdf67-sp9fr:
        Type    Reason     Age  Source                Messages
        Normal  Scheduled  47m  default-scheduler     Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-sp9fr to 10.240.0.24
        Normal  Pulling    47m  kubelet, 10.240.0.24  Pulling image "icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
        Normal  Pulled     47m  kubelet, 10.240.0.24  Successfully pulled image "icr.io/codeengine/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.682464554s
        Normal  Created    46m  kubelet, 10.240.0.24  Created container user-container
        Normal  Started    46m  kubelet, 10.240.0.24  Started container user-container
        [...] 
        ```
        {: screen}

## Verifying the container image reference for my app 
{: #ts-app-verifyimage}

When you work with {{site.data.keyword.codeengineshort}} apps, you must specify a container image reference and a registry secret to access the image. For the app to work correctly, the image reference and its access properties must remain valid for the life of the app. 

See [How can I verify my image reference](/docs/codeengine?topic=codeengine-ts-build-verify-image)?
