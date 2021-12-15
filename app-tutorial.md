---

copyright:
  years: 2020, 2021
lastupdated: "2021-12-15"

keywords: app tutorial for code engine, application, apps, images, tutorial for code engine, deploying

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Deploying applications
{: #deploy-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, deploy an application with the {{site.data.keyword.codeengineshort}} CLI. The application scales to zero when not in use.
{: shortdesc}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage.
{: note}

## Select an image file
{: #deploy-app-image-file}
{: step}

This tutorial uses a sample image, `ibmcom/hello`, which is a simple `Hello World` program. The program includes an environment variable `TARGET`, and prints `Hello ${TARGET}`. If the environment variable is empty, `Hello World` is returned.

If you have a container image that you want to use, you can replace the image reference in the next step with your own Docker repository, image name, and version.

You can review the code that is used for this example at [`ibmcom/hello`](https://github.com/IBM/CodeEngine/blob/main/hello/server.js).

## Creating and deploying an application
{: #app-creating-deploying}
{: step}

1. Create your application by using the [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. In the following example, use `myapp` as the name of the application and specify `ibmcom/hello` as the image to reference. 

    ```sh
    ibmcloud ce application create --name myapp --image ibmcom/hello
    ```
    {: pre}

    **Example output**

    ```sh
    Creating application 'myapp'...
    [...]
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce application get -n myapp' to check the application status.
    OK
    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

2. Run the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display details about the application, including the URL for the `myapp` application. 

    ```sh
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    **Example output**

    ```sh 
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                3m6s
    Created:            2021-07-11T06:39:41-05:00
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Image:                ibmcom/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  500Mi
    Memory:             4G

    Revisions:
    myapp-huv70-1:
        Age:                3m6s
        Traffic:            100%
        Image:              ibmcom/hello (pinned to f0dc03)
        Running Instances:  1

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  0
        Timeout:        300

    Conditions:
        Type                 OK    Age  Reason
        ConfigurationsReady  true  52s
        Ready                true  26s
        RoutesReady          true  26s

    Events:
    Type    Reason   Age   Source              Messages
    Normal  Created  3m9s  service-controller  Created Configuration "myapp"
    Normal  Created  3m9s  service-controller  Created Route "myapp"

    Instances:
    Name                                       Revision       Running  Status       Restarts  Age
    myapp-huv70-1-deployment-6656cfc796-7gl27  myapp-huv70-1  1/2      Terminating  0         3m9s
    ```
    {: screen}

3. Obtain the URL of the application from running the **`application get`** command as described in the previous step. To retrieve the URL of the application directly, you can use the `--output` option and specify the URL format on the **`application get`** command. Additionally, you can run the [**`ibmcloud ce application list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to get the application URL.

    ```sh 
    ibmcloud ce application get -n myapp -output url
    ```
    {: pre}

    **Example output**

    ```sh 
    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}


4. Copy the URL from the previous output and call the application with `curl`.

    ```sh 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    **Example output**

     ```sh 
     Hello World
     ```
     {: screen}

You successfully deployed and started a {{site.data.keyword.codeengineshort}} application!

## Updating your application
{: #app-updating}
{: step}

1. Update your newly created application by adding an environment variable to return `Hello Stranger` with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command.

    ```sh 
    ibmcloud ce application update --name myapp --env TARGET=Stranger
    ```
    {: pre}

    **Example output**

    ```sh 
    Updating application 'myapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myapp' to check the application status.
    OK

    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

2. Use the **`application get`** command to display details about your app, including the latest revision information. 

    ```sh 
    ibmcloud ce application get --name myapp 
    ```
    {: pre}

    **Example output**

    ```sh 
    Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
    Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                3m6s
    Created:            2021-07-11T06:39:41-05:00
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                ibmcom/hello

     Status Summary:  Application deployed successfully

     Environment Variables:
         Type     Name    Value
         Literal  TARGET  Stranger
     Image:                  ibmcom/hello
     Resource Allocation:
         CPU:                1
         Ephemeral Storage:  500Mi
         Memory:             4G

     Revisions:
     myapp-00002:
         Age:                54m
         Traffic:            100%
         Image:              ibmcom/hello (pinned to f0dc03)
         Running Instances:  1

     Runtime:
         Concurrency:    100
         Maximum Scale:  10
         Minimum Scale:  0
         Timeout:        300

     Conditions:
         Type                 OK    Age  Reason
         ConfigurationsReady  true  25s
         Ready                true  11s
         RoutesReady          true  11s

     Events:
     Type    Reason   Age    Source              Messages
     Normal  Created  4m17s  service-controller  Created Configuration "myapp"
     Normal  Created  4m17s  service-controller  Created Route "myapp"

     Instances:
        Name                                     Revision     Running  Status       Restarts  Age
        myapp-00001-deployment-bf7559548-mxgvq   myapp-00001  2/3      Terminating  0         4m55s
        myapp-00002-deployment-8495f8ccb9-kmc57  myapp-00002  3/3      Running      0         88s
     ```
     {: screen}

    From the output in the **Revisions** section, you can see the latest application revision of the `myapp` service. Also, notice that 100% of the traffic to the application is running the latest revision of the app. 

3. Call the application. 

    ```sh 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    **Example output**

    ```sh 
    Hello Stranger
    ```
    {: screen}

From the output of this command, you can see the updated app now returns `Hello Stranger`.  

## Scaling your application (scale-to-zero and scale-from-zero)
{: #app-scaling}
{: step}

The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. 

The following example illustrates how to scale your application with the CLI. You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options with the **`application create`** or **`application update`** command.

1. Call the application. 

    ```sh 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

2. Run the **`application get`** command to display the status of your application. Notice the value for `Running instances`. In this example, the app has `1` running instance.

    ```sh 
    ibmcloud ce application get -name myapp
    ```
    {: pre}

    **Example output**

    ```sh 
    [...]

    Name:          myapp
    [...]
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                  ibmcom/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  500Mi
        Memory:             4G

    Revisions:
    myapp-00002:
        Age:                58m
        Traffic:            100%
        Image:              ibmcom/hello (pinned to f0dc03)
        Running Instances:  1

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  0
        Timeout:        300

    Conditions:
        Type                 OK    Age  Reason
        ConfigurationsReady  true  57m
        Ready                true  57m
        RoutesReady          true  57m

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  4m17s  service-controller  Created Configuration "myapp"
        Normal  Created  4m17s  service-controller  Created Route "myapp"

    Instances:
        Name                                     Revision     Running  Status   Restarts  Age
        myapp-00002-deployment-8495f8ccb9-kmc57  myapp-00002  3/3      Running  0         16m
    ```
    {: screen}

3. Run the **`application get`** command again and notice that the value for `Running instances` scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value.

    ```sh 
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    **Example output**

    ```sh 
    [...]
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                  ibmcom/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  500Mi
        Memory:             4G

    Revisions:
    myapp-huv70-2
        Age:                13m
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
        ConfigurationsReady  true  13m
        Ready                true  13m
        RoutesReady          true  13m

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  4m17s  service-controller  Created Configuration "myapp"
        Normal  Created  4m17s  service-controller  Created Route "myapp"

    Instances:
        Name                                       Revision       Running  Status       Restarts  Age
        myapp-00002-deployment-8495f8ccb9-kmc57    myapp-00002    3/3      Running      0         16m
    ```
    {: screen}   

    Your application scaled down to zero.

4. Call the application again to scale from zero.

5. Run the **`application get`** command again and notice that the value for `Running instances` scaled from zero and information about the instance is displayed. 

    ```sh 
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    **Example output**

    ```sh 
    Name:          myapp
    [...]
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                  ibmcom/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  500Mi
        Memory:             4G

    Revisions:
    myapp-huv70-2:
        Age:                3h11m
        Traffic:            100%
        Image:              ibmcom/hello (pinned to f0dc03)
        Running Instances:  1

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  0
        Timeout:        300

    Conditions:
        Type                 OK    Age    Reason
        ConfigurationsReady  true  3h10m
        Ready                true  3h10m
        RoutesReady          true  3h10m

    Events:
        Type    Reason   Age    Source              Messages
        Normal  Created  4m17s  service-controller  Created Configuration "myapp"
        Normal  Created  4m17s  service-controller  Created Route "myapp"

    Instances:
        Name                                     Revision     Running  Status   Restarts  Age
        myapp-00002-deployment-8495f8ccb9-kmc57  myapp-00002  3/3      Running  0         16m
    ```
    {: screen}   

Your application scales back up.

For more information about scaling your app, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

## Next steps for apps
{: #nextsteps-deployapptut}

For more information, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


