---

copyright:
  years: 2021
lastupdated: "2021-01-08"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine

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


# Deploying applications
{: #application-workloads}

An application, or app, runs your code to serve HTTP requests. An app has a URL for incoming requests. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workload. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app.
{: #shortdesc}

**Before you begin**
   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
   * Plan a container image for {{site.data.keyword.codeengineshort}} applications. 

## Plan a container image for {{site.data.keyword.codeengineshort}} applications
{: #deploy-app-containerimage}

To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application needs in order to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

## Deploy application workloads from public repository
{: #deploy-app}

Deploy your app with {{site.data.keyword.codeengineshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Deploying an app from console
{: #deploy-app-console}

Deploy an application with an image from public Docker Hub with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your app needs to listen on a port other than port `8080`, deploy your app by using the CLI and use the `--port` option on the `app create` command to specify the port.
{: important}

This example references an image in public Docker Hub. You can also reference an [image in {{site.data.keyword.registryshort}}](#deploy-app-crimage) or an [image in a private repository](#deploy-app-private).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Application**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the application and specify a container image, for example, `docker.io/ibmcom/helloworld`. Use a name for your application that is unique within the project. You can also modify the default values for environment variables or runtime settings.
6. Click **Deploy**. 
7. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To open the application in a web page, click **Application URL**. 

### Deploying an app from CLI
{: #deploy-app-cli}

Deploy your application from the CLI with the `ibmcloud ce application create` command. 
{: shortdesc}

By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your app needs to listen on a port other than port `8080`, use the `--port` option on the `app create` command to specify the port.
{: important}

```
ibmcloud ce application create --name myapp --image docker.io/ibmcom/helloworld
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
   <td>The name of the image that is used for this application. For images in [Docker Hub](https://hub.docker.com), you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. </td>
   </tr>
</tbody>
</table>
	
## Deploy application workloads from images in {{site.data.keyword.registryshort}}
{: #deploy-app-crimage}

Deploy your app with {{site.data.keyword.codeengineshort}} that uses an image in {{site.data.keyword.registryshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

**Before you begin**

- You must have an IAM API key for your {{site.data.keyword.registryshort}} instance. If you do not have an IAM API key, [create one](/docs/codeengine?topic=codeengine-add-registry#access-registry-account). 
- You must have an image in {{site.data.keyword.registryshort}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started).

By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your app needs to listen on a port other than port `8080`, use the `--port` option on the `app create` command to specify the port.
{: important}

### Deploying an app that references an image in {{site.data.keyword.registryshort}} with the console
{: #deploy-app-crimage-console}

Deploy an application that uses an image in a container registry by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then deploy it. 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Application**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the application; for example `helloapp`.
6. Select **Container Image** from **Code** and click **Select image**. 
7. To add registry access, click **Edit image details** and then **Add registry**. 
8. From the Add Registry Access page, specify the registry name and registry server.  For example, specify `ibmcregistry1` as the registry name and specify `us.icr.io` as the registry server. 
9. Enter a name. For {{site.data.keyword.registryshort}}, it is `iamapikey`. 
10. Enter the password. For {{site.data.keyword.registryshort}}, the password is your API key. If you do not have an IAM API key, [create one](/docs/codeengine?topic=codeengine-add-registry#access-registry-account).
11. Click **Add** to add the registry access for {{site.data.keyword.codeengineshort}}.
12. From the Select image page, the registry that was added is listed. Select the registry of your image.
13. Select the namespace and name of the image in the registry for the {{site.data.keyword.codeengineshort}} app to reference. For example, select `mynamespace` and select the image `hello_repo` in that namespace.
14. Select a value for **TAG**; for example, `latest`.
15. Click **Done**. You have selected your image in the registry to reference from your app.
16. From the Create application page, click **Deploy**. 
17. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To open the application in a web page, click **Application URL**.  

If you want to add registry access before you create an app, see [Adding access to a {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-add-registry). 

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Deploying an app with an image in {{site.data.keyword.registryshort}} from CLI
{: #deploy-app-crimage-cli}

Deploy an application that uses an image in a container registry from the CLI with the `ibmcloud ce app create` command. 
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then deploy it. 

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM key](/docs/codeengine?topic=codeengine-add-registry#access-registry-account). To create an {{site.data.keyword.cloud_notm}} IAM API key from the CLI, run the [`iam api-key-create`](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

```
ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
```
{: pre}

If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
{: important}

2. After you create your API key, add registry access to {{site.data.keyword.codeengineshort}}. To add access to {{site.data.keyword.registryshort}} with the CLI, use the `registry create` command to create an image registry access secret. For example, create registry access to a {{site.data.keyword.registryshort}} instance called `myregistry` that is at `us.icr.io` that uses the IAM API key:

```
ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password APIKEY
```
{: pre}

**Example output**

```
Creating image registry access secret 'myregistry'...
OK
```
{: screen}

3. Create your app and reference the `hello_repo` image in {{site.data.keyword.registryshort}}. For example, create the `myhelloapp` app to reference the `us.icr.io/mynamespace/hello_repo` by using the `myregistry` access information. 

```
ibmcloud ce app create --name myhelloapp --image us.icr.io/mynamespace/hello_repo --registry-secret myregistry
```
{: pre}

The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: important}

4. After your app deploys, you can access the app. Run `ibmcloud ce app get` to find the URL of your app. For example, when you curl the `myhelloapp` app, `Hello World` is returned.  

```
curl https://myhelloapp.abcdabcdhye.us-south.codeengine.appdomain.cloud
```
{: pre}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deploy application workloads from images in a private repository
{: #deploy-app-private}

Deploy your app with {{site.data.keyword.codeengineshort}} that uses an image in a private repository or registry such as private Docker Hub. You can create an app from the console or with the CLI. 
{: shortdesc}

**Before you begin**

This example references an image in Docker Hub. In order to pull an image from Docker Hub, you must first push an image to {{site.data.keyword.registrylong_notm}}. Specifically, this example references an image called `hello_repo` in the `mynamespace` namespace; however, you can use any image and namespace. For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your app needs to listen on a port other than port `8080`, use the `--port` option on the `app create` command to specify the port.
{: important}

### Deploying an app that references an image in private respository with the console
{: #deploy-app-private-console}

Deploy an application that uses an image in a private repository with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in a private repository, you must first add access to the repository, pull the image, and then deploy it. 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Application**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Provisioning your project can take a few minutes. Wait until the project status is `Active` before you continue to the next step.
5. Enter a name for the application; for example `helloapp`.
6. Select **Container Image** from **Code**.
7. To add registry access, click **Edit image details** and then **Add registry**. 
8. From the Add Registry Access page, specify the registry name and registry server.  For example, specify `privatedocker` as the registry name and specify `https://index.docker.io/v1/` as the registry server. 
9. Enter a name. For Docker Hub, it is your Docker ID. 
10. Enter the password. For Docker Hub, you can use your Docker Hub password or an [access token](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-docker).
11. Click **Add** to add the registry access for {{site.data.keyword.codeengineshort}}.
12. From the Select image page, the registry that was added is listed. Select the registry of your image.
13. Select the namespace and name of the image in Docker Hub for the {{site.data.keyword.codeengineshort}} app to reference. For example, select `mynamespace` and select the image `hello_repo' in that namespace.
14. Select a value for **TAG**; for example, `latest`.
15. Click **Done**. You have selected your image in the registry to reference from your app.
16. From the Create application page, click **Deploy**. 
17. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To open the application in a web page, click **Application URL**.  

If you want to add registry access before you create an app, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry). 

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

### Deploying an app with an image from a private repository with CLI
{: #deploy-app-private-cli}

Deploy an application that uses an image in a container registry from the CLI with the `ibmcloud ce app create` command. 
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in a private repository, you must first add access to the registry, pull the image, and then deploy it. 

1. In order to pull images from a private repository, you must first create a private repository. For example, to create a private Docker Hub repository, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private repository, [push an image to it](https://docs.docker.com/docker-hub/repos/){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private respository in order to pull images. To add access to a private repository with the CLI, use the `registry create` command to create an image registry access secret. For example, create registry access to a Docker Hub repository called `privatedocker` that is at ``https://index.docker.io/v1/`` and uses your username and password.

```
ibmcloud ce registry create --name privatedocker --server `https://index.docker.io/v1/` --username <Docker_User_Name> --password <Password>
```
{: pre}

**Example output**

```
Creating image registry access secret 'privatedocker'...
OK
```
{: screen}

3. Create your app and reference the image in your private Docker Hub repository. For example, create the `myhelloapp` app to reference the `docker.io/PrivateRepo/helloworld` by using the `privatedocker` access information. 

```
ibmcloud ce app create --name myhelloapp --image docker.io/PrivateRepo/helloworld --registry-secret privatedocker
```
{: pre}

The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: important}

4. After your app deploys, you can access the app. Run `ibmcloud ce app get` to find the URL of your app. For example, when you curl the `myhelloapp` app, `Hello World` is returned.  

```
curl https://myhelloapp.abcdabcdhye.us-south.codeengine.appdomain.cloud
```
{: pre}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Access the app
{: #access-service}

After your app deploys, you can access it through a URL.
{: shortdesc}

From the console, your application URL is available from the components page and on the application details page.

From the CLI, run `ibmcloud ce app get` to find the URL of your app. 

```
ibmcloud ce application get --name NAME
```
{: pre}

## Deploying your app with a private endpoint
{: #deploy-app-endpoint}

You can deploy your application with a private endpoint so that the app is not exposed to external traffic. 
{: shortdesc}

To create the previous application with a private endpoint, add `--cluster-local` to the CLI command.

```
ibmcloud ce app create --name myapp --image docker.io/ibmcom/helloworld --cluster-local
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

1. Navigate to your application page. One way to navigate to your application page is to 
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

1. Run the `application update` command.  For example,

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
      Concurrency:         100
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
	
### Updating an app to reference a different image in {{site.data.keyword.registryshort}} from console
{: #update-app-crimage-console}

Update an application to reference a different image in a container registry by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

For this example, let's update the `helloapp` that you created in [Deploying an application that references an image in a container registry from console](#deploy-app-crimage-console) to reference a different image. The updated app will reference the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. The following steps describe adding access to a registry during the update of an app. 

For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [{{Getting started with site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started).

1. Navigate to your application page. One way to navigate to your application page is to 
   * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
   * Click the name of your project to open the **Overview** page.
   * Click the name of your application to open the application page.
2. Select the registry where your image resides. 
   * If the image you want to use resides in the same {{site.data.keyword.registryshort_notm}} account, select the registry.
   * If the image that you want to use resides in a different container registry account, click **Add registry**.  You must first {create your IAM API](/docs/codeengine?topic=codeengine-add-registry#access-registry-account) and then [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#access-registry-account).
   
   For this example, select the existing `ibmcregistry` registry, select the `mynamespace2` namespace, select the `helloworld-repo` image, and select `1` as the value for `tag`.  

3. Click **Done**. You have selected your image in the registry to reference from your app.
4. Click **Save and deploy** to save your change and deploy the app revision.
5. After the application status changes to **Ready**, you can test the app revision by clicking **Test application**. To see the running app, click **Application URL**. `Hello World from {{site.data.keyword.codeengineshort}}` is displayed.

### Updating an app to reference a different image in {{site.data.keyword.registryshort}} with the CLI
{: #update-app-crimage-cli}

Update an application to reference a different image in {{site.data.keyword.registryshort}} from the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

For this example, update the `helloapp` that you created in [Deploying an application that references an image in a container registry from CLI](#deploy-app-crimage-cli) to reference a different image in a different namespace in the same account. Update the app to reference the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. 

1. Add a different image to {{site.data.keyword.registryshort_notm}}. For this example, add the `helloworld_repo` image in the `mynamespace2` namespace in {{site.data.keyword.registryshort_notm}}. For more information about adding an image to {{site.data.keyword.registryshort_notm}}, see [{{Getting started with site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started)

2. Add registry access to {{site.data.keyword.codeengineshort}}. For this example, because the `helloworld_repo` image resides in the same account, use the previously defined `myregistry` registry access. 

3.Update your app and reference the image in {site.data.keyword.registryshort}} by using the `myregistry` access. For example, update the `myhelloapp` app to reference the `us.icr.io/mynamespace2/helloworld_repo` by using the `myregistry` access information. 

```
ibmcloud ce app update --name myhelloapp --image us.icr.io/mynamespace2/helloworld_repo:1 --registry-secret myregistry
```
{: pre}

The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: important}

4. After your app is updated, you can access the app. Run the `ibmcloud ce app get` command to get the URL of your app. For example, when you curl the `myhelloapp` app, the app returns `Hello World from {{site.data.keyword.codeengineshort}}` which demonstrates the app is now using the `helloworld_repo` image. 

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
