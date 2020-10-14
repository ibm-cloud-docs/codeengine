---

copyright:
  years: 2020
lastupdated: "2020-10-14"

keywords: code engine, tutorial, application

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Tutorial: Deploying applications 
{: #deploy-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, deploy an application with the {{site.data.keyword.codeengineshort}} CLI. The application scales to zero when not in use.
{: shortdesc}

An application, or app, runs your code to serve HTTP requests. An app has a URL for incoming requests. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workload. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app.


**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli).
- [Create and target a project](/docs/codeengine?topic=codeengine-manage-project).


## Select an image file
{: #deploy-app-image-file}
{: step}

This tutorial uses a sample [`ibmcom/hello`](https://hub.docker.com/r/ibmcom/hello) Docker image file. This example is a simple `Hello World!` program. The program includes an environment variable `TARGET`, and prints `Hello ${TARGET}!`. If the environment variable is empty, `Hello World!` is returned.

If you have a container image that you want to use, you can replace the image reference in the next step with your Docker repository, image name, and version.

For example, review the [`ibmcom/hello`](https://github.com/IBM/CodeEngine/blob/master/hello/hello.js) application in JavaScript.

   ```
   // Just a simple "Hello World" app 

   const http = require('http');

   http.createServer(function (request, response) {
      target = process.env.TARGET ? process.env.TARGET : 'World' ;
      msg = process.env.MSG ? process.env.MSG : 'Hello ' + target + '\n';
      response.writeHead(200, {'Content-Type': 'text/plain'});
      response.end(msg);
   }).listen(8080);

   console.log('Server running at http://0.0.0.0:8080/');
   ```
{: codeblock}


## Creating and deploying an application
{: #app-creating-deploying}
{: step}

1.  Create your application. Provide a name of the image that is used for this application and a name for your application. We are using the `ibmcom/hello` image reference.  

    ```
    ibmcloud ce application create --name myapp --image ibmcom/hello
    ```
    {: pre}

   **Example output**

   ```
   Creating application 'myapp'...
   Run 'ibmcloud ce application get -n myapp' to check the application status.
   https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

2.  Run the `application get` command to display details about the application, including the URL for the `myapp` application. 

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**

   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   ID:            a744a50a-7767-4fc3-ac1f-2172bdffa699
   Project Name:  myproject
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-b35f-abcd-abcd-abcdabcd111a/application/myapp/configuration

   Image:  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-nv321-1:
      Age:                2m6s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         10
      Concurrency Target:  10
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age   Reason
      ConfigurationsReady  true  112s
      Ready                true  107s
      RoutesReady          true  107s

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-nv321-1-deployment-85cbc5abcd-abcdg  1/2      Running  0         2m6s
   ```
   {: screen}

3. Obtain the URL of the application from running the `application get` command as described in the previous step.  Additionally, you can run the `application list` command to get the application URL.  

   ```
   ibmcloud ce application list
   ```
   {: pre}

   **Example output**

   ```
   Listing all applications...
   Name    URL                                                                    Latest          Age     Conditions   Ready   Reason
   myapp   https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud   myapp-xvlbz-1   2m20s   3 OK / 3     True
   ```
   {: screen}

4. Copy the domain URL from the previous output and call the application with `curl`.

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}
   
   **Example output**

   ```
   Hello World
   ```
   {: screen}

You have successfully deployed and started a {{site.data.keyword.codeengineshort}} application!

## Updating your application
{: #app-updating}
{: step}

1. Update your newly created application by adding an environment variable to return `Hello Stranger!`.

   ```
   ibmcloud ce application update --name myapp --env TARGET=Stranger
   ```
   {: pre}
   
   **Example output**

   ```
   Updating application 'myapp' to latest revision.
   OK

   https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

2. Use the `application get` command to display details about your app, including the latest revision information. 

   ```
   ibmcloud ce application get --name myapp 
   ```
   {: pre}
   
   **Example output**

   ```
   Getting application 'myapp'...
   Name:               myapp
   [...]
   
   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-b35f-abcd-abcd-abcdabcd111a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-nv321-2:
      Age:                65s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         10
      Concurrency Target:  10
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  49s
      Ready                true  44s
      RoutesReady          true  44s

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-nv321-1-deployment-85cbc5dff8-2qsfl  1/2      Running  0         2m56s
      myapp-nv321-1-deployment-85cbc5dff8-tp2vg  2/2      Running  0         101s
      myapp-nv321-2-deployment-5d8fd794bd-fx8th  2/2      Running  0         65s
   ```
   {: screen}

   From the output in the **Revisions** section, you can see the latest application revision of the `myapp` service. Also, notice that 100% of the traffic to the application is running the latest revision of the app. 

3. Call the application. 

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
      ```
   {: pre}
   
   **Example output**
   
   ```
   Hello Stranger
   ```
   {: screen}

From the output of this command, you can see the updated app now returns `Hello Stranger!`.  

## Scaling your application (scale-to-zero and scale-from-zero)
{: #app-scaling}
{: step}

The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. 

The following example illustrates how to scale your application with the CLI. You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options with the `application create` or `application update` command.

1. Call the application. 

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

2. Run the `application get` command to display the status of your application. Notice the value for `Running instances`. In this example, the app has `1` running instance.

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
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/a4e12aca-b35f-4b7b-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-nv321-2:
      Age:                7m8s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         10
      Concurrency Target:  10
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age    Reason
      ConfigurationsReady  true  6m52s
      Ready                true  6m47s
      RoutesReady          true  6m47s

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-nv321-2-deployment-5d8fd794bd-pzd5v  2/2      Running  0         45s
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
   Getting application 'myapp'...
   OK
   Name:          myapp
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/a4e12aca-b35f-4b7b-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-nv321-2:
      Age:                13m
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  0

   Runtime:
      Concurrency:         10
      Concurrency Target:  10
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  13m
      Ready                true  13m
      RoutesReady          true  13m
   ```
   {: screen}   

   ```
   {: screen}
   
   Your application scaled down to zero.

4. Call the application again to scale from zero.

5. Run the `application get` command again and notice that the value for `Running instances` scaled from zero.

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
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/a4e12aca-b35f-4b7b-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-nv321-2:
      Age:                13m
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         10
      Concurrency Target:  10
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  13m
      Ready                true  13m
      RoutesReady          true  13m
   ```
   {: screen}   

   Your application scales back up.
   
## Next steps

For more information, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
