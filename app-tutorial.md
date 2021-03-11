---

copyright:
  years: 2021
lastupdated: "2021-03-11"

keywords: app tutorial for code engine, application and code engine, apps and code engine, images for code engine apps, tutorial for code engine

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


# Tutorial: Deploying applications
{: #deploy-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, deploy an application with the {{site.data.keyword.codeengineshort}} CLI. The application scales to zero when not in use.
{: shortdesc}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeengineshort}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).


## Select an image file
{: #deploy-app-image-file}
{: step}

This tutorial uses a sample image, `ibmcom/hello`, which is a simple `Hello World` program. The program includes an environment variable `TARGET`, and prints `Hello ${TARGET}`. If the environment variable is empty, `Hello World` is returned.

If you have a container image that you want to use, you can replace the image reference in the next step with your own Docker repository, image name, and version.

You can review the code that is used for this example at [`ibmcom/hello`](https://github.com/IBM/CodeEngine/blob/main/hello/server.js).

## Creating and deploying an application
{: #app-creating-deploying}
{: step}

1.  Create your application by using the [`ibmcloud ce application create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. In the following example, use `myapp` as the name of the application and specify `ibmcom/hello` as the image to reference. 

    ```
    ibmcloud ce application create --name myapp --image ibmcom/hello
    ```
    {: pre}

   **Example output**

   ```
   Creating application 'myapp'...
   [...]
   Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce application get -n myapp' to check the application status.
   OK
   https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

2.  Run the [`ibmcloud ce application get`](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display details about the application, including the URL for the `myapp` application. 

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**

   ```
   OK

   Name:          myapp
   ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
   Project Name:  myproject
   Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
   Age:           3m6s
   Created:       2021-02-11T06:39:41-05:00
   URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

   Status Summary:  Application deployed successfully

   Image:                ibmcom/hello
   Resource Allocation:
   CPU:                0.1
   Ephemeral Storage:  500Mi
   Memory:             1Gi

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

3. Obtain the URL of the application from running the `application get` command as described in the previous step. To retrieve the URL of the application directly, you can use the `--output` option and specify the URL format on the `application get` command. Additionally, you can run the [`ibmcloud ce application list`](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to get the application URL.

   ```
   ibmcloud ce application get -n myapp -output url
   ```
   {: pre}

   **Example output**

   ```
   https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   ```
   {: screen}


4. Copy the URL from the previous output and call the application with `curl`.

   ```
   curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   ```
   {: pre}
   
   **Example output**

   ```
   Hello World
   ```
   {: screen}

You successfully deployed and started a {{site.data.keyword.codeengineshort}} application!

## Updating your application
{: #app-updating}
{: step}

1. Update your newly created application by adding an environment variable to return `Hello Stranger` with the [`ibmcloud ce application update`](/docs/codeengine?topic=codeengine-cli#cli-application-update) command.

   ```
   ibmcloud ce application update --name myapp --env TARGET=Stranger
   ```
   {: pre}
   
   **Example output**

   ```
   Updating application 'myapp' to latest revision.
   [...]
   Run 'ibmcloud ce application get -n myapp' to check the application status.
   OK

   https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

2. Use the `application get` command to display details about your app, including the latest revision information. 

   ```
   ibmcloud ce application get --name myapp 
   ```
   {: pre}
   
   **Example output**

   ```
   OK

   Name:          myapp
   ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
   Project Name:  myproject
   Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
   Age:           3m6s
   Created:       2021-02-11T06:39:41-05:00
   URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

   Status Summary:  Application deployed successfully

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:                0.1
      Ephemeral Storage:  500Mi
      Memory:             1Gi

   Revisions:
    myapp-huv70-2:
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
   Name                                       Revision       Running  Status       Restarts  Age
   myapp-huv70-2-deployment-745589dbf5-dz5hd  myapp-huv70-2  2/2      Terminating  0         90s
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

## Scaling your application (scale-to-zero and scale-from-zero)
{: #app-scaling}
{: step}

The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. 

The following example illustrates how to scale your application with the CLI. You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options with the `application create` or `application update` command.

1. Call the application. 

   ```
   curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

2. Run the `application get` command to display the status of your application. Notice the value for `Running instances`. In this example, the app has `1` running instance.

    ```
    ibmcloud ce application get -name myapp
    ```
    {: pre}

   **Example output**
   
   ```
   OK

   Name:          myapp
   [...]
   URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

   Status Summary:  Application deployed successfully

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
      Resource Allocation:
      CPU:                0.1
      Ephemeral Storage:  500Mi
      Memory:             1Gi

   Revisions:
    myapp-huv70-2:
      Age:                58m
      Traffic:            100%
      Image:              ibmcom/hello (pinned to f0dc03)
      Running Instances:  2

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
   Name                                       Revision       Running  Status       Restarts  Age
   myapp-huv70-2-deployment-745589dbf5-dz5hd  myapp-huv70-2  1/2      Terminating  0         5m29s
   myapp-huv70-2-deployment-745589dbf5-fs8cd  myapp-huv70-2  2/2      Running      0         75s
   ```
   {: screen}

  Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
  {: note}

3. Run the `application get` command again and notice that the value for `Running instances` scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value.

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**

   ```
   [...]
   URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

   Status Summary:  Application deployed successfully

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:                0.1
      Ephemeral Storage:  500Mi
      Memory:             1Gi

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
   ```
   {: screen}   
   ```

   Your application scaled down to zero.

4. Call the application again to scale from zero.

5. Run the `application get` command again and notice that the value for `Running instances` scaled from zero and information about the instance is displayed. 

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Name:          myapp
   [...]
   URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

   Status Summary:  Application deployed successfully

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:                0.1
      Ephemeral Storage:  500Mi
      Memory:             1Gi

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
   Name                                       Revision       Running  Status   Restarts  Age
   myapp-huv70-2-deployment-745589dbf5-b5vts  myapp-huv70-2  2/2      Running  0         22s
   ```
   {: screen}   

   Your application scales back up.
   
   For more information about scaling your app, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).
   
## Next steps
{: #nextsteps-deployapptut}

For more information, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
