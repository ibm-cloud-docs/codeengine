---

copyright:
  years: 2020
lastupdated: "2020-07-16"

keywords: code engine, tutorial, application

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Tutorial: Deploying applications 
{: #knative-deploy-app-tutorial}

With this tutorial, deploy a containerized application in a serverless fashion by using the {{site.data.keyword.codeengineshort}} CLI. The application scales to zero when not in use.

** Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli)
- [Create and target a project](/docs/codeengine?topic=codeengine-manage-project)


## Select an image file

This tutorial uses a sample [ibmcom/helloworld](https://hub.docker.com/r/ibmcom/helloworld) Docker image file. This example is a simple `Hello World!` program. The program includes an environment variable `TARGET`, and prints `Hello ${TARGET}!`. If the environment variable is empty, `Hello World!` is returned.

If you have a container image that you want to use, you can replace the image reference in the next step with your Docker repository, image name, and version.

For example, review the `ibmcom/helloworld` application in Go.

   ```
   cat helloworld.go
   package main

   import (
      	   "fmt"
	   "log"
	   "net/http"
	   "os"
   )

   func handler(w http.ResponseWriter, r *http.Request) {
	   log.Print("Hello world received a request.")
	   target := os.Getenv("TARGET")
	   if target == "" {
	   	   target = "World"
	   }
	   fmt.Fprintf(w, "Hello %s!\n", target)
   }

   func main() {
	   log.Print("Hello world sample started.")

	   http.HandleFunc("/", handler)

	   port := os.Getenv("PORT")
	   if port == "" {
		   port = "8080"
	   }
   
	   log.Fatal(http.ListenAndServe(fmt.Sprintf(":%s", port), nil))
   }
   ```
   {: pre}



## Create and deploy an application

1.  Create your application. Provide a name of the image that is used for this application and a name for your application. We are using the `ibmcom/helloworld` image reference.  

    ```
    ibmcloud ce application create --name myapp --image ibmcom/helloworld
    ```
    {: pre}

   **Example output**

   ```
   Successfully created application 'myapp'.
   Run 'ibmcloud ce application get -n myapp' to check the application status.
   https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   ```
   {: screen}

2.  Run the `application get` command to display details about the application, which includes the URL for the `myapp` application. 

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**

   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: 9f6e2161-64ac
   Age: 1m21s
   URL: https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/9f6e2161-64ac-4596-ac55-2810bdf1ca2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-1 (1m20s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 1

   Conditions:
   OK   Type                  Age     Reason
   ++   ConfigurationsReady   1m13s
   ++   Ready                 1m11s
   ++   RoutesReady           1m11s
   OK
   Command 'application get' performed successfully
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
   myapp   https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud   myapp-xvlbz-1   2m20s   3 OK / 3     True
   OK
   Command 'application list' performed successfully
   ```
   {: screen}

4. Copy the domain URL from the previous output and call the application with `curl`.

   ```
   curl https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   ```
   {: pre}
   
   **Example output**

   ```
   StatusCode        : 200
   StatusDescription : OK
   Content           : Hello World! (revision: myapp-xvlbz-1)

   RawContent        : HTTP/1.1 200 OK
                     x-envoy-upstream-service-time: 3740
                     Content-Length: 39
                     Content-Type: text/plain; charset=utf-8
                     Date: Wed, 15 Jul 2020 14:39:01 GMT
                     Server: istio-envoy

                     Hello World! (revision: m...
   Forms             : {}
   Headers           : {[x-envoy-upstream-service-time, 3740], [Content-Length, 39], [Content-Type, text/plain; charset=utf-8], [Date, Wed, 15 Jul 2020
                     14:39:01 GMT]...}
   Images            : {}
   InputFields       : {}
   Links             : {}
   ParsedHtml        : mshtml.HTMLDocumentClass
   RawContentLength  : 39
   ```
   {: screen}

You have successfully deployed and started your first {{site.data.keyword.codeengineshort}} application!

## Update your application

1. Update your newly created application by adding an environment variable to return `Hello Stranger!`.

   ```
   ibmcloud ce application update --name myapp --env TARGET=Stranger
   ```
   {: pre}
   
   **Example output**

   ```
   Updating application 'myapp'
   Application 'myapp' updated to latest revision and is available at URL:
   http://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   ```
   {: screen}

2. Use the `application get` command to display the status of your app, including the latest revision information. For this example, let's use the `--more-details` option on the command to view more information about the updated app, including the value for the environment variable.

   ```
   ibmcloud ce application get --name myapp --more-details 
   ```
   {: pre}
   
   **Example output**

   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: 9f6e2161-64ac
   Age: 5m13s
   URL: https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/9f6e2161-64ac-4596-ac55-2810bdf1ca2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-2 (49s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 1

   Conditions:
   OK   Type                  Age   Reason
   ++   ConfigurationsReady   41s
   ++   Ready                 39s
   ++   RoutesReady           39s

   ---------------------
   Environment Variables
   ---------------------

   TARGET: Stranger

   ---------------------
   Runtime
   ---------------------

   MinScale:
   MaxScale:
   CPU Request: 0.1
   Memory Request: 1Gi
   Timeout: 300
   Container Concurrency: 10

   OK
   Command 'application get' performed successfully
   ```
   {: screen}

From the output in the **Latest revision** section, you can see the latest application revision of the `myapp` service. Also, notice that 100% of the traffic to the application is running the latest revision of the app. 

3. Call the application. 

   ```
   curl https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
      ```
   {: pre}
   
   **Example output**
   
   ```
   StatusCode        : 200
   StatusDescription : OK
   Content           : Hello Stranger! (revision: myapp-xvlbz-2)

   RawContent        : HTTP/1.1 200 OK
                     x-envoy-upstream-service-time: 4271
                     Content-Length: 42
                     Content-Type: text/plain; charset=utf-8
                     Date: Wed, 15 Jul 2020 15:04:42 GMT
                     Server: istio-envoy

                     Hello Stranger! (revision...
   Forms             : {}
   Headers           : {[x-envoy-upstream-service-time, 4271], [Content-Length, 42], [Content-Type, text/plain;
                     charset=utf-8], [Date, Wed, 15 Jul 2020 15:04:42 GMT]...}
   Images            : {}
   InputFields       : {}
   Links             : {}
   ParsedHtml        : mshtml.HTMLDocumentClass
   RawContentLength  : 42
   ```
   {: screen}

From the output of this command, you can see the updated app now returns `Hello Stranger!`.  

## Application scaling (scale-to-zero and scale-from-zero)

The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. 

The following example illustrates application scaling with the CLI. You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options using the `application create` or `application update` command.

1. Call the application. 

   ```
   curl https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
      ```
   {: pre}
   

2. Run the `application get` command to display the status of your application. Specifically, notice the value for `Running instances`. In this example, the app has `1` running instance. For example:

    ```
    ibmcloud ce application get -name myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: 9f6e2161-64ac
   Age: 30m2s
   URL: https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/9f6e2161-64ac-4596-ac55-2810bdf1ca2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-2 (25m38s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 1

   Conditions:
   OK   Type                  Age      Reason
   ++   ConfigurationsReady   25m30s
   ++   Ready                 25m28s
   ++   RoutesReady           25m28s
   OK
   Command 'application get' performed successfully
   ```
   {: screen}

  Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
  {: note}

3. Run the `application get` command again and notice that the value for `Running instances` has scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value. For example:

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: 9f6e2161-64ac
   Age: 30m59s
   URL: https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/9f6e2161-64ac-4596-ac55-2810bdf1ca2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-2 (26m35s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 0

   Conditions:
   OK   Type                  Age      Reason
   ++   ConfigurationsReady   26m27s
   ++   Ready                 26m25s
   ++   RoutesReady           26m25s
   OK
   Command 'application get' performed successfully
   ```
   {: screen}

4. Call the application again to scale from zero:

   ```
   curl https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   ```
   {: pre}
   
5. Run the `application get` command again and notice that the value for `Running instances` has scaled from zero. For example:

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: 9f6e2161-64ac
   Age: 32m30s
   URL: https://myapp.9f6e2161-64ac.us-south.codeengine.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/9f6e2161-64ac-4596-ac55-2810bdf1ca2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-2 (28m6s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 1

   Conditions:
   OK   Type                  Age      Reason
   ++   ConfigurationsReady   27m58s
   ++   Ready                 27m56s
   ++   RoutesReady           27m56s
   OK
   Command 'application get' performed successfully
   ```
   {: screen}   

Voilà!

## What have you seen?
You have deployed and updated an arbitrary containerized application in a serverless fashion, meaning that you: 

1. Don't need to think about scaling, the environment **scales-from zero** to however many instances you need.
2. Don't need to pay for resources that are not used. The environment automatically **scales-to zero** if no requests come in.

