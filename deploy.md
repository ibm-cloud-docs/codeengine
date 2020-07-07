---

copyright:
  years: 2020
lastupdated: "2020-07-07"

keywords: knative

subcollection: code-engine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Deploying applications
{: #application-workloads}

An *application*, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: #shortdesc} 

## Deploying application workloads
{: #knative-deploy-app}

Deploy your app with {{site.data.keyword.codeengineshort}}.
{: shortdesc}

**Before you begin**
   * If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/knative/overview){: external}. 
   * If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/code-engine?topic=code-engine-kn-install-cli).
   * Create a container image for {{site.data.keyword.codeengineshort}} applications.

## Creating a container image for {{site.data.keyword.codeengineshort}} applications
{: #deploy-app-containerimage}

To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application will need to run, such as runtime libraries. There are many different ways of creating the image, such as using the Docker `docker build` command, but there are a couple of key things to keep in mind. Your container image: 
   * Must have an HTTP server listening on port 8080.
   * Must be downloadable from a publicly accessible image registry.

### Deploying an application from console
{: #deploy-app-console}

The following steps describe how to deploy an application by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

1. To work with a project, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}. 
2. From the Projects page, click the name of your project to open the project Components page. 
3. From your project Components page, click **Application** to create an app. 
4. From the Create Application page, enter a name for your application and provide an image reference for your container. For example, enter `myapp` for the application name and `ibmcom/helloworld` for container image. Click **Deploy**. 
  When you use this image, the application uses the sample `ibmcom/helloworld` image, reads the environment variable `TARGET`, and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
5. After the application status changes to **Ready**, you can run your application by clicking **Test application**. To see the running application, click **Application URL**.  

You have created and deployed an application to {{site.data.keyword.codeengineshort}} and tested it out using the console.

### Deploying an application from CLI
{: #deploy-app-cli}

Deploy your application from the CLI with the `ibmcloud coligo application create` command. 
{: shortdesc}

```
ibmcloud coligo application create --name NAME --image IMAGE
```
{: pre}

<table>
   <caption>application create components</caption>
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
   <td>The name of the application. This value is required. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique within the project.</td>
   </tr>
   <tr>
   <td><code>--image</code></td>
   <td>The container image for this application. This value is required. For images in [Docker Hub](https://hub.docker.com), you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</td>
   </tr>
   <tr>
   <td><code>--concurrency</code></td>
   <td>The number of requests that can be processed concurrently per instance. The default value is 10. This value is optional. 
   <p> If you set this value to 0, the system attempts to ensure that no more than 100 requests will be sent to any one instance; however, this is not a hard limit and can exceed this value at times. </p>
   <p> If your code should work on a single request at a time, set concurrency to 1 and each instance will only process one request at a time. </p>
   <p> The maximum number of overall concurrent requests that the app component can work on concurrently is determined by "the maximum number of concurrent requests per instance" times "the maximum number of instances":  max_instances x max_concurrency.</p>
   </td>
   </tr>
   <tr>
   <td><code>--cpu</code></td>
   <td>The amount of CPU set for the application. The default value is 1. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--memory</code></td>
   <td>The amount of memory set for the application. The default value is 64 M. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--minscale</code></td>
   <td>The minimum number of instances that can be used for this application. This option is useful to ensure no instances are running when not needed. The default value is 0. This value is optional. </td>
   </tr>
   <tr>
   <td><code>--maxscale</code></td>
   <td>The maximum number of instances that can be used for this application. The default value is 10. This value is optional.</td>
   </tr>
   <tr>
   <td><code>--timeout</code></td>
   <td>The amount of time that can pass before the application must succeed or fail. The default value is 300 seconds. This value is optional.</td>
   </tr>
      <tr>
   <td><code>--registry-secret</code></td>
   <td>The name of the secret used to authenticate with a private registry when downloading the container image. This value is optional.</td>
   </tr>
      </table>

## Accessing your service
{: #access-service}

After your service deploys, you can access it through a URL.
{: shortdesc}

From the console, your application URL is available from the components page and on the application details page.

From the CLI, run `ibmcloud coligo application get` to find the URL. 

```
ibmcloud coligo application get --name NAME
```
{: pre}

## Updating your app
{: #update-app}

An application contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.
{: shortdesc} 

To create a revision of the application, modify the application. 

### Updating your app from the console
{: #update-app-console}

Let's update the application that you created in [Deploying an application from console](#deploy-app-cli) to add an environment variable.

1. Navigate to your application page. One way to navigate to your application page is to: 
   * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}. 
   * Click the name of your project to open the project component page.
   * Click the name of your application to open the application page.
2. Click **Env. variables**.
3. Click **Add environment variable** and enter `TARGET` for name and `Stranger` for value.
4. Click **Save and deploy** to save your change and deploy the application revision.
5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.

### Updating your app with the CLI
{: #update-app-cli}

Let's update the application that you created in [Deploying an application from console](#deploy-app-console) to add an environment variable. 

The sample `ibmcom/helloworld` image that we used earlier, reads the environment variable `TARGET`, and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. Let's modify the `TARGET` environment value to `Stranger`.

1. Run the `application update` command.  For example:

    ```
    ibmcloud coligo application update -n myapp --env TARGET=Stranger
    ```
    {: pre}

   **Example output**

   ```
   Updating application 'myapp' in namespace '8a87129b-97fb':
   Application 'myapp' updated to latest revision 'myapp-bqawk-4' and is available at URL:
   http://myapp.8a87129b-97fb.us-south.knative.appdomain.cloud
   ```
   {: screen}

2. View the provided URL to see the updated application. The application displays `Hello Stranger`.


## Application status
{: #app-status}

The following table shows the possible status that your application might have.

| Status | Description |
| ------ | ------------|
| Deploying | The application is deploying. This includes time before being scheduled as well as time spent downloading images over the network, which can take a while. |
| Ready | The application is deployed and ready to use. |
| Ready (with warnings) | The deployment of a new application revision failed, but the original deployment is available. |
| Failed | The application deployment has terminated, and at least one instance has terminated in failure. That is, the instance either exited with non-zero status or was terminated by the system.
| Unknown |	For some reason the state of the application could not be obtained, typically due to an error in communicating with the host. |


