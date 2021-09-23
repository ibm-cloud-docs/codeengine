---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-21"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Updating your app
{: #update-app}

An application contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: shortdesc} 

To create a revision, modify the application. Note that if you are modifying your app, you must provide valid vCPU and memory combinations. For more information about these options, see [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy)

{{site.data.keyword.codeengineshort}} has a quota for the number of apps and app revisions in a project. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas). {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted.
{: important}

## Updating your app from the console
{: #update-app-console}

Update the application that you created in [Deploying an application from the console](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) to add an environment variable.

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the **Overview** page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. Click **Environment variables**.
3. Click **Add environment variable** and enter `TARGET` for name and `Stranger` for value. Click **Save**.
4. Click **Save and deploy** to save your change and deploy the application revision.
5. After the application status changes to **Ready**, you can test the application revision by clicking **Send request**. To see the running application, click **Open application URL**. `Hello Stranger` is displayed.


## Updating your app with the CLI
{: #update-app-cli}

To update your app with the CLI, use the **`app update`** command. This command requires the name of the app that you want to update and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command.
{: shortdesc}

Update the application that you created in [Deploying an application with the CLI](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-cli) to add an environment variable. 

The sample `docker.io/ibmcom/hello ` image reads the environment variable `TARGET`, and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. The following example updates the app to modify the value of the `TARGET` environment variable to `Stranger`.

1. Run the **`application update`** command. For example,

    ```
    ibmcloud ce application update -n myapp --env TARGET=Stranger
    ```
    {: pre}

    **Example output**

    ```
    Updating application 'myapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myapp' to check the application status.
    OK

    https://myapp.4idmmq6xpss.us-south.codeengine.test.appdomain.cloud      
    ```
    {: screen}

2. Run the **`application get`** command to display the status of your app, including the latest revision information. 

    ```
    ibmcloud ce application get --name myapp  
    ```
    {: pre}

    **Example output**

    ```
    [...]
    Name:          myapp
    [...]
    URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
    Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

    Environment Variables:
    Type     Name    Value
    Literal  TARGET  Stranger
    Image:                  docker.io/ibmcom/hello
    Resource Allocation:
    CPU:                1
    Ephemeral Storage:  500Mi
    Memory:             4G

    Revisions:
    myapp-hc3u8-2:
        Age:                82s
        Traffic:            100%
        Image:              docker.io/ibmcom/hello (pinned to f0dc03)
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

    ```
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    **Example output**

    ```
    Hello Stranger
    ```
    {: screen}

    From the output of this command, you can see the updated app now returns `Hello Stranger`.

4. Use the [**`ibmcloud ce revision list`**](/docs/codeengine?topic=codeengine-cli#cli-revision-list) command to display all of your app revisions. Use this information to help you manage your app revisions as {{site.data.keyword.codeengineshort}} has a [quota for the number of app revisions in a project](/docs/codeengine?topic=codeengine-limits#project_quotas).

    In the following **`revision list`** output, notice that {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. 

    ```
    ibmcloud ce revision list 
    ```
    {: pre}

    **Example output**

    ```
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

You can manage your app revisions by using the [**`ibmcloud ce revision get`**](/docs/codeengine?topic=codeengine-cli#cli-revision-get) command to display details of an app revision and the [**`ibmcloud ce revision delete`**](/docs/codeengine?topic=codeengine-cli#cli-revision-delete) command to remove revisions that you don't want to keep. You can also use the  [**`ibmcloud ce revision logs `**](/docs/codeengine?topic=codeengine-cli#cli-revision-logs) command to view logs of application revision instances. Use the [**`ibmcloud ce revision events `**](/docs/codeengine?topic=codeengine-cli#cli-revision-events) command to display system events of application revision instances.

## Updating an app to reference a different image in {{site.data.keyword.registryshort}} from the console
{: #update-app-crimage-console}

Update an application to reference a different image in a container registry by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

For this example, let's update the `helloapp` that you created in [Deploying an application that references an image in a container registry from the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console) to reference a different image. The updated app references the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. The following steps describe adding access to a registry during the update of an app. 

For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

1. Navigate to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the **Overview** page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open the application page.
2. Select the registry where your image resides. 
    * If the image you want to use resides in the same {{site.data.keyword.registryshort_notm}} account, select the registry.
    * If the image that you want to use resides in a different container registry account, click **Add registry**.  You must first [create your IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key) and then [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).

    For this example, select the existing `ibmcregistry` registry, select the `mynamespace2` namespace, select the `helloworld-repo` image, and select `1` as the value for `tag`.  

3. Click **Done**. You selected your image in the registry to reference from your app.
4. Click **Save and deploy** to save your change and deploy the app revision.
5. After the application status changes to **Ready**, you can test the app revision by clicking **Send request**. To see the running app, click **Open application URL**. `Hello World from {{site.data.keyword.codeengineshort}}` is displayed.

## Updating an app to reference a different image in {{site.data.keyword.registryshort}} with the CLI
{: #update-app-crimage-cli}

Update an application to reference a different image in {{site.data.keyword.registryshort}} from the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

For this example, update the `helloapp` that you created in [Deploying an application that references an image in a container registry with the CLI](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-cli) to reference a different image in a different namespace in the same account. Update the app to reference the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. 

1. Add a different image to {{site.data.keyword.registryshort_notm}}. For this example, add the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

2. Add registry access to {{site.data.keyword.codeengineshort}}. For this example, because the `helloworld_repo` image resides in the same account, use the previously defined `myregistry` registry access. 

3. Update your app and reference the image in {{site.data.keyword.registryshort}} by using the `myregistry` access. For example, update the `myhelloapp` app to reference the `us.icr.io/mynamespace2/helloworld_repo` by using the `myregistry` access information. 

    ```
    ibmcloud ce app update --name myhelloapp --image us.icr.io/mynamespace2/helloworld_repo:1 --registry-secret myregistry
    ```
    {: pre}

    The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
    {: important}

4. After your app is updated, you can access the app. To obtain the URL of your app, run `ibmcloud ce app get --name myhelloapp --output url`. When you curl the `myhelloapp` app, the app returns `Hello World from {{site.data.keyword.codeengineshort}}`, which demonstrates the app is now using the `helloworld_repo` image. 


