---

copyright:
  years: 2020
lastupdated: "2020-07-13"

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

This tutorial uses a sample [ibmcom/helloworld](https://hub.docker.com/r/ibmcom/helloworld) Docker image file. This example is a simple `Hello World!` program. The program includes an environment variable `TARGET`, and prints "Hello ${TARGET}!". If the environment variable is empty, "Hello World!" is returned.

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
    ibmcloud coligo application create --name myapp --image ibmcom/helloworld
    ```
    {: pre}

   **Example output**

   ```
      Successfully created application 'myapp'.
      Run 'ibmcloud coligo application get -n myapp' to check the application status.
      https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud
   ```
   {: screen}

2.  Run the `application get` command to display details about the application, which includes the URL for the `myapp` application. 

    ```
    ibmcloud coligo application get -n myapp
    ```
    {: pre}

   **Example output**

   ```
      Getting application 'myapp'...
      Name: myapp
      Namespace: efd6cd29-3280
      Age: 1m28s
      URL: https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud
      Console URL: https://test.cloud.ibm.com/knative/project/us-south/efd6cd29-3280-4d27-a19e-c12a83c69d2b/application/myapp/configuration

      Latest Revision:
      100%  @latest myapp-xvlbz-1 (1m28s)
            Image:  ibmcom/helloworld (pinned to f7fde9)
            Running instances: 1

      Conditions:
      OK   Type                  Age     Reason
      ++   ConfigurationsReady   1m21s
      ++   Ready                 1m18s
      ++   RoutesReady           1m18s
      OK
      Command 'application get' performed successfully
   ```
   {: screen}

3. Obtain the URL of the application from running the `application get` command as described in the previous step.  Additionally, you can run the `application list` command to get the application URL.  

   ```
   ibmcloud coligo application list
   ```
   {: pre}

   **Example output**

   ```
      Listing all applications...
      Name     URL                                                                  Latest            Age     Conditions   Ready   Reason
      myapp    https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud    myapp-xvlbz-1     2m58s   3 OK / 3     True   
      OK
      Command 'application list' performed successfully
   ```
   {: screen}

4. Copy the domain URL from the previous output and call the application with `curl`.

   ```
   curl https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud
   ```
   {: pre}
   
   **Example output**

   ```
      StatusCode        : 200
      StatusDescription : OK
      Content           : Hello World! (revision: myapp-xvlbz-1)

      RawContent        : HTTP/1.1 200 OK
                        x-envoy-upstream-service-time: 4375
                        Content-Length: 39
                        Content-Type: text/plain; charset=utf-8
                        Date: Fri, 10 Jul 2020 18:25:31 GMT
                        Server: istio-envoy

                        Hello World! (revision: m...
      Forms             : {}
      Headers           : {[x-envoy-upstream-service-time, 4375], [Content-Length, 39], [Content-Type, text/plain;
                        charset=utf-8], [Date, Fri, 10 Jul 2020 18:25:31 GMT]...}
      Images            : {}
      InputFields       : {}
      Links             : {}
      ParsedHtml        : mshtml.HTMLDocumentClass
      RawContentLength  : 39
   ```
   {: screen}
   
You have successfully deployed and started your first {{site.data.keyword.codeengineshort}} application!

## Step 3 - Update your application

1. Update your newly created application by providing a memory limit.

   ```
   ibmcloud coligo application update --name myapp --memory 256Mi
   ```
   {: pre}
   
   **Example output**

   ```
      Updating application 'myapp'
      Application 'myapp' updated to latest revision and is available at URL:
      http://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud
   ```
   {: screen}

2. Use the `application get` command to display the status of your application, including the latest revision information.

   ```
   ibmcloud coligo application get --name myapp 
   ```
   {: pre}
   
   **Example output**

   ```
   Getting application 'myapp'...
   Name: myapp
   Namespace: efd6cd29-3280
   Age: 12m38s
   URL: https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/efd6cd29-3280-4d27-a19e-c12a83c69d2b/application/myapp/configuration

   Latest Revision:
   100%  @latest myapp-xvlbz-2 (3m11s)
         Image:  ibmcom/helloworld (pinned to f7fde9)
         Running instances: 0

   Conditions:
   OK   Type                  Age    Reason
   ++   ConfigurationsReady   3m4s
   ++   Ready                 3m1s
   ++   RoutesReady           3m1s
   OK
   Command 'application get' performed successfully
   ```
   {: screen}

   From the output, you can see the latest application revision of the 'myapp` service. 

3. By default, new calls to the application are routed to the new revision. You can verify this action by listing the applications. 

   ```
   ibmcloud coligo application list 
   ```
   {: pre}
   
   **Example output**

   ```
   Listing all applications...
   Name     URL                                                                  Latest            Age      Conditions   Ready   Reason
   myapp    https://myapp.efd6cd29-3280.us-south.knative.test.appdomain.cloud    myapp-xvlbz-2     33m29s   3 OK / 3     True 
   ```
   {: screen}


