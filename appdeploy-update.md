---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-16"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Updating your app
{: #update-app}

An application contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: shortdesc} 

To create a revision, modify the application. If you are modifying your app, you must provide valid vCPU and memory combinations. For more information about these options, see [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy)

{{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas). {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted.
{: important}

You can [update your deployed app](/docs/codeengine?topic=codeengine-update-app) and its referenced code by using *any* of the following ways, independent of how you created or previously updated your app:


- If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you deploy your app. You can deploy your app with an image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private).


    If you created your app by using the **`app create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your app to point to a different container image, you must first remove the association of the build from your app. For example, run `ibmcloud ce application update -n APP_NAME --build-clear`. After you remove the association of the build from your app, you can update the app to reference a different image. 
    {: important}

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

- If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the app. Then, after the image is matured, you can update the deployed app to reference the specific image that you want. You can repeat this process as needed.

When you deploy your updated app, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment. 




## Updating your app from the console
{: #update-app-console}

Update the application that you created in [Deploying an application from a public registry from the console](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) to add an environment variable.

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. From the application page, you can view information about the running instances of your application and its revisions, configuration details, and endpoint settings of the app. Click the name of the application revision that you want to work with to open the configuration summary for that revision. Or, you can click the **Configuration** tab to open the configuration summary for the latest application revision. 
3. Click **Edit and create new revision** to change the app configuration.
4. Click **Environment variables**.
5. Click **Add environment variable**. Define this environment variable as a literal value. Enter `TARGET` for name and `Stranger` for value. Click **Done**.
6. Click **Save and create** to save your change and deploy the application revision.
7. After the application status changes to **Ready**, you can test the application revision. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. For this app, `Hello Stranger` is displayed.

In this example, you updated environment variables for an app. You can also update other configuration settings for your app, including referencing a [different image](#update-app-crimage-console) or [different image build](#update-app-source-console) from the **Code** tab. From the **Runtime** tab, you can update [memory](/docs/codeengine?topic=codeengine-mem-cpu-combo) and [application scaling](/docs/codeengine?topic=codeengine-app-scale) settings for your app. From the **Environment variables** tab, you can add or update [environment variables](/docs/codeengine?topic=codeengine-envvar) for your app. From the **Command** tab, you can add or update [command and arguments](/docs/codeengine?topic=codeengine-cmd-args) to override settings within your container image. 

## Updating your app to use project-only endpoints from the console
{: #update-app-console-projendpt}

By default, when you deploy an app, the app deploys such that it can receive requests from the public internet, from a private network, or from components within the project. Let's change the visibility of this app such that it is accessed only by other {{site.data.keyword.codeengineshort}} resources that are running in the same {{site.data.keyword.codeengineshort}} environment. Use the **Endpoints** tab to change the visibility of an app. 

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. From the application page, you can view information about the running instances of your application and its revisions, configuration details, and endpoint settings of the app. Click the **Endpoints** tab to open the endpoint visibility settings for the application.  
3. From the **Endpoints** tab, notice the available URLs for your application. When `Public` is selected, you can view the public and the cluster-local URL for the application. When `Project-Only` is selected, this application is no longer accessible from the public internet and network access is only possible from components within this project (cluster-local). Click **Project-Only** to change the endpoint visibility of the app. The cluster-local URL is displayed when `Project-Only` is selected.

    By changing the visibility of your app, the change is effective immediately. It is important to consider the impact of the change for your active users or integrations as well as any security implications. You can change the visibility setting as needed. 
    {: important}  

## Updating your app to use private endpoints from the console
{: #update-app-console-privateendpt}

By default, when you deploy an app, the app deploys such that it can receive requests from the public internet, from a private network, or from components within the project. Let's change the visibility of this app such that it is accessed only by other {{site.data.keyword.codeengineshort}} resources that are running in the same project and from the private network by using Virtual Private Endpoints. Use the **Endpoints** tab to change the visibility of an app. 

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. From the application page, you can view information about the running instances of your application and its revisions, configuration details, and endpoint settings of the app. Click the **Endpoints** tab to open the endpoint visibility settings for the application.  
3. From the **Endpoints** tab, notice the available URLs for your application. When `Private` is selected, this application is no longer accessible from the public internet and network access is only possible from components within this project (cluster-local) and from the private network.

    Click **Private** to change the endpoint visibility of the app. The available URLs for your endpoint definition are displayed for the private and project-only URLs.

4. To access your app securely by using a Virtual Private Endpoint (VPE), follow the instructions for [Using your VPE to access an app](/docs/codeengine?topic=codeengine-vpe#using-vpes-app) to set up the VPE to access your app. 

If you set your application for `visibility = private`, then you can only test your application through the [virtual private endpoint from within your Virtual Private Cloud (VPC)](/docs/codeengine?topic=codeengine-vpe).

By changing the visibility of your app, the change is effective immediately. It is important to consider the impact of the change for your active users or integrations as well as any security implications. You can change the visibility setting as needed. 
{: important}  


## Updating your app with the CLI
{: #update-app-cli}

To update your app with the CLI, use the **`app update`** command. This command requires the name of the app that you want to update and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command.
{: shortdesc}

Update the application that you created in [Deploying an application with the CLI](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-cli) to add an environment variable. 

The sample `icr.io/codeengine/hello` image reads the environment variable `TARGET`, and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. The following example updates the app to modify the value of the `TARGET` environment variable to `Stranger`. For more information about the code that is used for this example, see [`hello`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.

1. Run the **`application update`** command. For example,

    ```txt
    ibmcloud ce application update -n myapp --env TARGET=Stranger
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

2. Run the **`application get`** command to display the status of your app, including the latest revision information. 

    ```txt
    ibmcloud ce application get --name myapp  
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myapp
    [...]
    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Environment Variables:
    Type     Name    Value
    Literal  TARGET  Stranger
    Image:                  icr.io/codeengine/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

    Revisions:
    myapp-hc3u8-2:
        Age:                82s
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
    ConfigurationsReady  true  75s
    Ready                true  62s
    RoutesReady          true  62s

    Events:
    Type    Reason   Age    Source              Messages
    Normal  Created  2m11s  service-controller  Created Configuration "myapp"
    Normal  Created  2m11s  service-controller  Created Route "myapp"

    Instances:
    Name                                       Revision       Running  Status       Restarts  Age
    myapp-hc3u8-1-deployment-65cf8cd4f5-jx8b8  myapp-hc3u8-1  1/2      Terminating  0         2m10s
    myapp-hc3u8-2-deployment-7f98b679d5-2hskr  myapp-hc3u8-2  2/2      Terminating  0         85s
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

4. Use the [**`ibmcloud ce revision list`**](/docs/codeengine?topic=codeengine-cli#cli-revision-list) command to display all your app revisions. Use this information to help you manage your app revisions as {{site.data.keyword.codeengineshort}} has a [quota for the number of app revisions in a project](/docs/codeengine?topic=codeengine-limits#project_quotas).

    In the following **`revision list`** output, notice that {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. 

    ```txt
    ibmcloud ce revision list 
    ```
    {: pre}

    Example output

    ```txt
    Listing all application revisions...
    OK

    Name                   Application      Status  URL  Latest  Tag  Traffic  Age    Conditions  Reason
    myapp-hc3u8-4           myapp            Ready                            2d15h    3 OK / 4
    myapp-hc3u8-5           myapp            Ready        true         100%    2d8h    3 OK / 4  
    myapp2-vjfqt-1          myapp2           Ready        true         100%      3d    3 OK / 4
    myhelloapp-tv368-3      myhelloapp       Ready                              16d    3 OK / 4
    myhelloapp-tv368-4      myhelloapp       Ready        true         100%     16d    3 OK / 4
    newapp-mytest-00008     newapp-mytest    Ready                              4d17h  3 OK / 4
    newapp-mytest-00009     newapp-mytest    Ready        true         100%     2d20h  3 OK / 4
    ```
    {: screen}

You can manage your app revisions by using the [**`ibmcloud ce revision get`**](/docs/codeengine?topic=codeengine-cli#cli-revision-get) command to display details of an app revision and the [**`ibmcloud ce revision delete`**](/docs/codeengine?topic=codeengine-cli#cli-revision-delete) command to remove revisions that you don't want to keep. You can also use the  [**`ibmcloud ce revision logs`**](/docs/codeengine?topic=codeengine-cli#cli-revision-logs) command to view logs of application revision instances. Use the [**`ibmcloud ce revision events`**](/docs/codeengine?topic=codeengine-cli#cli-revision-events) command to display system events of application revision instances.

## Updating your app to use project-only endpoints with the CLI
{: #update-app-cli-projectonly}

By default, when you deploy an app, the app deploys such that it can receive requests from the public internet, from a private network, or from components within the project. To change the visibility of your app such that it is accessed only by other {{site.data.keyword.codeengineshort}} resources that are running in the same project, use the `--visibility=project` option with the [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) or [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.{: shortdesc}

In this scenario, update the application that you created in [Deploying an application with the CLI](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-cli) to change the visibility of the app to use a [project endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly).  

1. Run the **`application update`** command. For example,

    ```txt
    ibmcloud ce application update -n myapp --visibility=project
    ```
    {: pre}

    Example output

    ```txt
    Updating application 'myapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myapp' to check the application status.
    OK

    http://myapp.4svg40kna19.svc.cluster.local   
    ```
    {: screen}

2. Run the **`application get`** command to display the status of your app, including the latest revision information. 

    ```txt
    ibmcloud ce application get --name myapp  
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myapp
    [...]
    URL:           http://myapp.4svg40kna19.svc.cluster.local
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Environment Variables:
    Type     Name    Value
    Literal  TARGET  Stranger
    Image:                  icr.io/codeengine/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

    Revisions:
    myapp-hc3u8-2:
        Age:                82s
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
    ConfigurationsReady  true  75s
    Ready                true  62s
    RoutesReady          true  62s

    Events:
    Type    Reason   Age    Source              Messages
    Normal  Created  2m11s  service-controller  Created Configuration "myapp"
    Normal  Created  2m11s  service-controller  Created Route "myapp"

    Instances:
    Name                                       Revision       Running  Status       Restarts  Age
    myapp-hc3u8-1-deployment-65cf8cd4f5-jx8b8  myapp-hc3u8-1  1/2      Terminating  0         2m10s
    myapp-hc3u8-2-deployment-7f98b679d5-2hskr  myapp-hc3u8-2  2/2      Terminating  0         85s
    ```
    {: screen}

    From the output in the **Revisions** section, you can see the latest application revision of the `myapp` service. Also, notice that 100% of the traffic to the application is running the latest revision of the app. 

Now that you set `--visibility=project` on your application, this application is no longer accessible from the public internet and network access is only possible from components within this project (cluster-local).

## Updating your app to use private endpoints with the CLI
{: #update-app-cli-privateendpt}

By default, when you deploy an app, the app deploys such that it can receive requests from the public internet, from a private network, or from components within the project. You can set the endpoint visibility for your app such that it is deployed with a private endpoint. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services from virtual private endpoints (VPC) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).
{: shortdesc}

 To change the visibility of your app such that it is accessed only with a private endpoint, use the `--visibility=private` option with the [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) or [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.{: shortdesc}

 You can only use your VPE to access your app with a private endpoint if your selected project supports [application private visibility](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-private). To confirm if the project supports application private visibility, use the  [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to verify the output for `Application Private Visibility Supported` is set to `true`. 
{: important}

In this scenario, update the application that you created in [Deploying an application with the CLI](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-cli) to change the visibility of the app to use a [private endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-private). 


1. Confirm that the existing project supports applications with private visibility. Use the  [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to verify the output for `Application Private Visibility Supported` is set to `true`. If the value is `false`, [contact IBM support](/docs/codeengine?topic=codeengine-get-support) to enable this capability within your existing project.

    ```txt
    ibmcloud ce project get -n myproject
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
    App revisions                             1     60  
    Apps                                      1     20  
    Build runs                                1     100  
    Builds                                    2     100  
    Configmaps                                2     100  
    CPU                                       0     64  
    Ephemeral storage                         0     256G  
    Instances (active)                        0     250  
    Instances (total)                         0     2500  
    Job runs                                  0     100  
    Jobs                                      0     100  
    Memory                                    0     256G  
    Secrets                                   6     100  
    Subscriptions (cron)                      0     100  
    Subscriptions (IBM Cloud Object Storage)  0     100  
    Subscriptions (Kafka)                     0     100
    ```
    {: screen}

2. If `Application Private Visibility Supported` is `true`, then you can update your app to use private endpoints. Run the **`application update`** command. For example,

    ```txt
    ibmcloud ce application update -n myapp --visibility=private
    ```
    {: pre}

    Example output

    ```txt
    Updating application 'myapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myapp' to check the application status.
    OK

    https://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

3. Run the **`application get`** command to display the status of your app, including the latest revision information. 

    ```txt
    ibmcloud ce application get --name myapp  
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Name:          myapp
    [...]
    URL:           https://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Environment Variables:
    Type     Name    Value
    Literal  TARGET  Stranger
    Image:                  icr.io/codeengine/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

    Revisions:
    myapp-hc3u8-2:
        Age:                82s
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
    ConfigurationsReady  true  75s
    Ready                true  62s
    RoutesReady          true  62s

    Events:
    Type    Reason   Age    Source              Messages
    Normal  Created  2m11s  service-controller  Created Configuration "myapp"
    Normal  Created  2m11s  service-controller  Created Route "myapp"

    Instances:
    Name                                       Revision       Running  Status       Restarts  Age
    myapp-hc3u8-1-deployment-65cf8cd4f5-jx8b8  myapp-hc3u8-1  1/2      Terminating  0         2m10s
    myapp-hc3u8-2-deployment-7f98b679d5-2hskr  myapp-hc3u8-2  2/2      Terminating  0         85s
    ```
    {: screen}

    From the output in the **Revisions** section, you can see the latest application revision of the `myapp` service. Also, notice that 100% of the traffic to the application is running the latest revision of the app. 

4. Set up your VPE to [access your app with a private endpoint](/docs/codeengine?topic=codeengine-vpe#using-vpes-app).



## Updating an app to reference a different image in {{site.data.keyword.registryshort}} from the console
{: #update-app-crimage-console}

Update an application to reference a different image in a container registry by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

For this example, let's update the `helloapp` that you created in [Deploying an application that references an image in a container registry from the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console) to reference a different image. The updated app references the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. The following steps describe adding access to a registry during the update of an app. 

For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open the application page.
2. Click **Configuration** to open the configuration details for the selected application revision. 
3. Click **Edit and create new revision** to update the application. 
4. From the **Code** tab, click **Configure image** to open the configure image dialog. For this example, update the app to reference an existing `ibmcregistry` registry, select the `mynamespace2` namespace, select the `helloworld-repo` image, and select `1` as the value for `tag`. From the configure image page,
    * If the image you want to use resides in the same {{site.data.keyword.registryshort_notm}} account, select the access for the registry.
    * If the image that you want to use resides in a different container registry account, you can select the registry access for this registry. If the registry access does not exist, you must first [create your IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key) and then [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce). 

    If you want to update only the registry access to your image, you can make this change without clicking **Configure image** to open the configure image dialog and use the Registry access menu to select an existing registry access or [create a registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce) for the image that is referenced by your application.   
    {: note}
    
5. Click **Done**. You selected your image in the registry to reference from your app.
6. Click **Save and create** to save your change and deploy the app revision.
7. After the application status changes to **Ready**, you can test the app revision. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. For this app, `Hello World from {{site.data.keyword.codeengineshort}}` is displayed.

## Updating an app to reference a different image in {{site.data.keyword.registryshort}} with the CLI
{: #update-app-crimage-cli}

Update an application to reference a different image in {{site.data.keyword.registryshort}} from the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

For this example, update the `myhelloapp` that you created in [Deploying an application that references an image in a container registry with the CLI](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-cli) to reference a different image in a different namespace in the same account. Update the app to reference the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. 

1. Add a different image to {{site.data.keyword.registryshort_notm}}. For this example, add the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

2. Add registry access to {{site.data.keyword.codeengineshort}}. For this example, because the `helloworld_repo` image resides in the same account, use the previously defined `myregistry` registry access. 

3. Update your app and reference the image in {{site.data.keyword.registryshort}} by using the `myregistry` access. For example, update the `myhelloapp` app to reference the `us.icr.io/mynamespace2/helloworld_repo` by using the `myregistry` access information. 

    ```txt
    ibmcloud ce app update --name myhelloapp --image us.icr.io/mynamespace2/helloworld_repo:1 --registry-secret myregistry
    ```
    {: pre}

    The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
    {: important}

4. After your app is updated, you can access the app. To obtain the URL of your app, run `ibmcloud ce app get --name myhelloapp --output url`. When you curl the `myhelloapp` app, the app returns `Hello World from {{site.data.keyword.codeengineshort}}`, which demonstrates the app is now using the `helloworld_repo` image. 

## Updating an app to reference an image that is built from source code from the console
{: #update-app-source-console}

Update an application to reference an image that is built from source code by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

For this example, let's update the `helloapp` that you created in [Deploying an application that references an image in a container registry from the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console) to reference an image that is built from your source code. 

For more information about creating a build configuration from the console, see [create a build](/docs/codeengine?topic=codeengine-build-image#build-create-console).

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open the application page.
2. Click **Configuration** to open the configuration details for the selected application revision. 
3. Click **Edit and create new revision** to update the application. 
4. From the **Code** tab, you can create an image build, or you can rerun an existing image build that is referenced by your application. To create an image build, click **Create image from source** to run an image build. The Specify build details page opens where you can enter the details of your build to [deploy your app from source code](/docs/codeengine?topic=codeengine-app-source-code). Click **Done** when build detail updates are specified. 
5. Click **Save and create** to save your changes, run the build, and deploy the app revision.
6. After the application status changes to **Ready**, you can test the app revision. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. 
7. To update this application again to reference an updated build image, click **Edit and create new revision** to update the application.
8. From the **Code** tab, click **Rerun build** and specify a unique image tag for the updated build image. If you want to make more changes to the build details, click **Edit build details**. The Specify build details page opens where you can enter the details of your build to [deploy your app from source code](/docs/codeengine?topic=codeengine-app-source-code). Click **Done** when build detail updates are specified. 
9. Click **Save and create** to save your changes, run the build with your changes, and deploy the app revision.
10. After the application status changes to **Ready**, you can test the app revision. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.

## Updating an app to reference an image that is built from source code with the CLI
{: #update-app-source-cli}

Update an application to reference an image that is built from source code by using the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

For this example, let's change the `myhelloapp` that you updated in [Updating an app to reference a different image in Container Registry with the CLI](#update-app-crimage-cli) to reference a different image that is built from your source code. 

From the previous example, the `myhelloapp` app references the `us.icr.io/mynamespace2/helloworld_repo` by using the `myregistry` access information. Let's create a build configuration, run the build, and update the `myhelloapp` to reference the image that was built from source code. 

1.  Create the build configuration. For example, the following **`build create`** command creates a build configuration that is called `helloworld-build`. This configuration builds from the public Git repo `https://github.com/IBM/CodeEngine`, uses the `dockerfile` strategy and `medium` build size, and stores the image to `us.icr.io/mynamespace/codeengine-helloworld` by using the image registry secret that is defined in `myregistry`.

    ```txt
    ibmcloud ce build create --name helloworld-build --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry --source https://github.com/IBM/CodeEngine --commit main --context-dir /hello --strategy dockerfile --size medium
    ```
    {: pre}

2. Run the build. This example runs a build that is called `helloworld-build-run` and uses the `helloworld-build` build configuration. 

    ```txt
    ibmcloud ce buildrun submit --build helloworld-build --name helloworld-build-run 
    ```
    {: pre}

    The following output displays the details of the build run by using the  [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command.

    Example output

    ```txt
    Getting build run 'helloworld-build-run'...
    [...]
    OK

    Name:          helloworld-build-run  
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
    Project Name:  myproject  
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
    Age:           21m  
    Created:       2021-09-30T14:50:13-05:00  

    Summary:  Succeeded  
    Status:   Succeeded  
    Reason:   All Steps have completed executing

    Image:  us.icr.io/mynamespace/codeengine-helloworld

    ```
    {: screen}

    For more information about creating a build configuration with the CLI, see [create a build](/docs/codeengine?topic=codeengine-build-image#build-create-cli).

3. Update the `myhelloapp` to reference the image that you built and uses the `myregistry` registry secret.

    ```txt
    ibmcloud ce app update --name myhelloapp --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry
    ```
    {: pre}

4. Display information about the updated app to confirm the image that is referenced is the image that you built. 

    ```txt
    ibmcloud ce app get -name myhelloapp 
    ```
    {: pre}

    Example output

    ```txt
    [...]
    OK

    Name:               myhelloapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                2m4s
    Created:            2021-09-09T14:01:02-04:00
    URL:                https://myhelloapp.abcdabcdabc.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myhelloapp.abcdabcdabc.svc.cluster.local
    Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myhelloapp/configuration
    Status Summary:     Application deployed successfully

    Environment Variables:
    Type     Name          Value
    Literal  CE_APP        myhelloapp
    Literal  CE_DOMAIN     us-south.codeengine.appdomain.cloud
    Literal  CE_SUBDOMAIN  8aaon2dfwa0
    Image:                  us.icr.io/mynancesnamespace/codeengine-helloworld
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G
    Registry Secrets:
    myregistry

    Revisions:
    helloapp-00003:
        Age:                2m46s
        Latest:             true
        Traffic:            100%
        Image:              us.icr.io/mysnamespace/codeengine-helloworld (pinned to eeca2b)
        Running Instances:  1
    [...]
    ```
    {: screen}


