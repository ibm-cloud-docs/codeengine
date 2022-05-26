---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-26"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps

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

The maximum number of apps that you can create per project is 20. You are limited to a total of 60 revisions for all apps per project. {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. See [Updating apps](/docs/codeengine?topic=codeengine-update-app).

For more information about limits for apps including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Getting logs for my apps 
{: #ts-app-gettinglogs}

Logs can be helpful to troubleshoot problems when you run apps. You can view app logs from the console or with the CLI. 
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} app. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your apps. You can view app logs after you add logging capabilities. For more information, see [viewing app logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui).

When working with the CLI, you can display logs for all the instances of an app or display logs of a specific instance of an app. 

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

For more information, see [Viewing application logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-applog-cli).

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



