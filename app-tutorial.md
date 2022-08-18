---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: app tutorial for code engine, application, apps, images, tutorial for code engine, deploying

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Deploying and scaling applications
{: #deploy-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, deploy an application with the {{site.data.keyword.codeengineshort}} CLI. The application scales to zero when not in use.
{: shortdesc}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Select an image file
{: #deploy-app-image-file}
{: step}

This tutorial uses a sample image, `icr.io/codeengine/hello`, which is a simple `Hello World` program. The program includes an environment variable `TARGET`, and prints `Hello ${TARGET}`. If the environment variable is empty, `Hello World` is returned. For more information about the code that is used for this example, see [`hello`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.

If you have a container image that you want to use, you can replace the image reference in the next step with your own Docker repository, image name, and version.

## Creating and deploying an application
{: #app-creating-deploying}
{: step}

1. Create your application by using the [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. In the following example, use `myapp` as the name of the application and specify `icr.io/codeengine/hello` as the image to reference. 

    ```txt
    ibmcloud ce application create --name myapp --image icr.io/codeengine/hello
    ```
    {: pre}

    Example output

    ```txt
    Creating application 'myapp'...
    [...]
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce application get -n myapp' to check the application status.
    OK
    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

2. Run the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display details about the application, including the URL for the `myapp` application. 

    ```txt
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    Example output

    ```txt 
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

    Image:                icr.io/codeengine/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

    Revisions:
    myapp-huv70-1:
        Age:                3m6s
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to f0dc03)
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

    ```txt 
    ibmcloud ce application get -n myapp -output url
    ```
    {: pre}

    Example output

    ```txt 
    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}


4. Copy the URL from the previous output and call the application with `curl`.

    ```txt 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    Example output

     ```txt 
     Hello World
     ```
     {: screen}

You successfully deployed and started a {{site.data.keyword.codeengineshort}} application!

## Updating your application
{: #app-updating}
{: step}

1. Update your newly created application by adding an environment variable to return `Hello Stranger` with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command.

    ```txt 
    ibmcloud ce application update --name myapp --env TARGET=Stranger
    ```
    {: pre}

    Example output

    ```txt 
    Updating application 'myapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myapp' to check the application status.
    OK

    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

2. Use the **`application get`** command to display details about your app, including the latest revision information. 

    ```txt 
    ibmcloud ce application get --name myapp 
    ```
    {: pre}

    Example output

    ```txt 
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
    Image:                icr.io/codeengine/hello

     Status Summary:  Application deployed successfully

     Environment Variables:
         Type     Name    Value
         Literal  TARGET  Stranger
     Image:                  icr.io/codeengine/hello
     Resource Allocation:
         CPU:                1
         Ephemeral Storage:  400M
         Memory:             4G

     Revisions:
     myapp-00002:
         Age:                54m
         Traffic:            100%
         Image:              icr.io/codeengine/hello (pinned to f0dc03)
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

    ```txt 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    Example output

    ```txt 
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

    ```txt 
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

2. Run the **`application get`** command to display the status of your application. Notice the value for `Running instances`. In this example, the app has `1` running instance.

    ```txt 
    ibmcloud ce application get -name myapp
    ```
    {: pre}

    Example output

    ```txt 
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
    Image:                  icr.io/codeengine/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
    myapp-00002:
        Age:                58m
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to f0dc03)
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

    ```txt 
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    Example output

    ```txt 
    [...]
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                  icr.io/codeengine/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
    myapp-huv70-2
        Age:                13m
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to 548d5c)
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

    ```txt 
    ibmcloud ce application get -n myapp
    ```
    {: pre}

    Example output

    ```txt 
    Name:          myapp
    [...]
    URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
    Status Summary:  Application deployed successfully

    Environment Variables:
        Type     Name          Value
        Literal  TARGET        Stranger
    Image:                  icr.io/codeengine/hello

    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Revisions:
    myapp-huv70-2:
        Age:                3h11m
        Traffic:            100%
        Image:              icr.io/codeengine/hello (pinned to f0dc03)
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

## Next steps
{: #nextsteps-deployapptut}

* After your app deploys, [access your app](/docs/codeengine?topic=codeengine-access-service) through a URL. 
    * You can create a custom domain and assign it to your app. For information about deploying an app with a custom domain through Cloudflare, see the [Configuring a Custom Domain for Your {{site.data.keyword.codeengineshort}} Application](https://www.ibm.com/cloud/blog/configuring-a-custom-domain-for-your-ibm-cloud-code-engine-application){: external}  blog. For more information about deploying apps across multiple regions with a custom domain name, see [Deploying an application across multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions). 

* Now that you app is deployed, consider making your apps event-driven. By using event subscriptions, you can trigger your apps by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) or set your app to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).

* After your app is deployed, you can [update your deployed app](/docs/codeengine?topic=codeengine-update-app) and its referenced code by using *any* of the following ways, independent of how you created or previously updated your app:

    - If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you deploy your app. You can deploy your app with an image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private).

        If you created your app by using the **`app create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your app to point to a different container image, you must first remove the association of the build from your app. For example, run `ibmcloud ce application update -n APP_NAME --build-clear`. After you remove the association of the build from your app, you can update the app to reference a different image. 
        {: important}

    - If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

    - If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

    For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the app. Then, after the image is matured, you can update the deployed app to reference the specific image that you want. You can repeat this process as needed.

    When you deploy your updated app, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment. 




Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

