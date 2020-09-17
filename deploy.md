---

copyright:
  years: 2020
lastupdated: "2020-09-17"

keywords: code engine, application, app, http requests

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


# Deploying applications
{: #application-workloads}

An application, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: #shortdesc}

**Before you begin**
   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli).
   * Plan a container image for {{site.data.keyword.codeengineshort}} applications. 

## Plan a container image for {{site.data.keyword.codeengineshort}} applications
{: #deploy-app-containerimage}

To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application needs in order to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

## Deploy application workloads
{: #deploy-app}

Deploy your app with {{site.data.keyword.codeengineshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeengineful_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Deploying an application from console
{: #deploy-app-console}

Deploy an application by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

1. To work with a project, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Projects page, click the name of your project to open the **Overview** page. 
3. From your **Overview** page, click **Application** to create an app. 
4. From the Create Application page, enter a name for your application and provide an image reference for your container. For example, enter `myapp` for the application name and `ibmcom/hello` for container image. Click **Deploy**. 
5. After the application status changes to **Ready**, you can run your application by clicking **Test application**. To see the running application, click **Application URL**.  

### Deploying an application from CLI
{: #deploy-app-cli}

Deploy your application from the CLI with the `ibmcloud ce application create` command. 
{: shortdesc}

```
ibmcloud ce application create --name myapp --image ibmcom/hello
```
{: pre}

<table>
	<caption><code>application create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>application create</code></td>
   <td>The command to create your application.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the application. Use a name that is unique within the project. This value is required.
      <ul>
	   <li>The name must begin with a lowercase letter.</li>
	   <li>The name must end with a lowercase alphanumeric character.</li>
	   <li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
      </ul>
   </td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The name of the image that is used for this application. For images in [Docker Hub](https://hub.docker.com), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. </td>
   </tr>
</table>

## Access the app
{: #access-service}

After your app deploys, you can access it through a URL.
{: shortdesc}

From the console, your application URL is available from the components page and on the application details page.

From the CLI, run `ibmcloud ce application get` to find the URL of your app. 

```
ibmcloud ce application get --name NAME
```
{: pre}

## Deploying your app with a private endpoint
{: #deploy-app-private}

You can deploy your application with a private endpoint The application is not exposed to external traffic. 
{: shortdesc}

To create previous application with a private endpoint, add `--cluster-local` to the CLI command.

```
ibmcloud ce application create --name myapp --image ibmcom/hello --cluster-local
```
{: pre}

## Update your app
{: #update-app}

An application contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: shortdesc} 

To create a revision of the application, modify the application. 

### Updating your app from the console
{: #update-app-console}

Update the application that you created in [Deploying an application from console](#deploy-app-console) to add an environment variable.

1. Navigate to your application page. One way to navigate to your application page is to: 
   * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
   * Click the name of your project to open the **Overview** page.
   * Click the name of your application to open the application page.
2. Click **Env. variables**.
3. Click **Add environment variable** and enter `TARGET` for name and `Stranger` for value.
4. Click **Save and deploy** to save your change and deploy the application revision.
5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.

### Updating your app with the CLI
{: #update-app-cli}

Update the application that you created in [Deploying an application from CLI](#deploy-app-cli) to add an environment variable. 

The sample `ibmcom/hello` image reads the environment variable `TARGET`, and prints `"Hello ${TARGET}"`. If this environment variable is empty, `"Hello World"` is returned. Let's modify the value of the `TARGET` environment variable to `Stranger`.

1. Run the `application update` command.  For example:

    ```
    ibmcloud ce application update -n myapp --env TARGET=Stranger
    ```
    {: pre}

   **Example output**

   ```
   Updating application 'myapp'
   OK
   Application 'myapp' updated to latest revision.
   https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud

   ```
   {: screen}

2. Run the `application get` command to display the status of your app, including the latest revision information. 

   ```
   ibmcloud ce application get --name myapp  
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
      Concurrency:         10
      Concurrency Target:  10
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

## Scale your application
{: #scale-app}

With {{site.data.keyword.codeengineshort}}, you don't need to think about scaling, as the number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. With automatic scaling, you don't need to pay for resources that are not used. 
{: shortdesc} 

### Scaling your application from the console
{: #scale-app-console}

To observe application scaling from the {{site.data.keyword.codeengineshort}} console, navigate to your running application and click **Instances** to view the graphical representation of the running instances of your application. While the application is running, the number of running instances is `1` or greater based on your maximum number of instances setting. When the application is finished running, the number of running instances scales to zero, if the minimum number of instances is set to `0`. 

You can control the maximum and minimum number of running instances of your app by changing the `Minimum number of instances` and `Maximum number of instances` scaling values that are found on your application's **Configuration** page.
{: tip}

### Scaling your application with the CLI
{: #scale-app-cli}

You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options by using the `application create` or `application update` command.

To observe application scaling from the {{site.data.keyword.codeengineshort}} CLI:

1. Call the application. 

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

2. Run the `application get` command to display the status of your application. Look for the value for `Running instances`. In this example, the app has `1` running instance. For example:

    ```
    ibmcloud ce application get -name myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   
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
      Concurrency:         10
      Concurrency Target:  10
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

3. Run the `application get` command again and notice that the value for `Running instances` scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value. For example:

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
      Concurrency:         10
      Concurrency Target:  10
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

4. Call the application again to scale from zero:

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

5. Run the `application get` command again and notice that the value for `Running instances` scaled up from zero. For example:

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

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-2-deployment-65766594d4-hj6c5  2/2      Running  0         22s
   ```
   {: screen}

## View application logs
{: #view-app-logs}

After your application has deployed, find the logs.
{: shortdesc}



### Viewing app logs with the CLI
{: #view-applog-cli}

To view app logs with the CLI, use the `ibmcloud ce app logs` command. 

```
ibmcloud ce app logs --instance APP_INSTANCE 
```
{: pre}

Use the `app get` command to find the instance name. For example, to view the logs for an instance of `myapp`, use the command: 

```
ibmcloud ce app logs --instance myapp-a5yp2-2-deployment-65766594d4-hj6c5
```
{: pre}

**Example output**
   
```
Logging application instance 'myapp-a5yp2-2-deployment-65766594d4-hj6c5'...
OK

Server running at http://0.0.0.0:8080/
```
{: screen}

## Application status
{: #app-status}

The following table shows the possible status that your application might have.

| Status | Description |
| ------ | ------------|
| Deploying | The application is deploying. Deployment time includes the time before the app is scheduled as well as time to download images over the network, which can take a while. |
| Ready | The application is deployed and ready to use. |
| Ready (with warnings) | The deployment of a new application revision failed, but the original deployment is available. |
| Failed | The application deployment terminated, and at least one instance terminated in failure. The instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the application could not be obtained, typically due to an error in communicating with the host. |
