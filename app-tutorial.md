---

copyright:
  years: 2020
lastupdated: "2020-07-07"

keywords: code engine, tutorial, application

subcollection: code-engine

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

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/code-engine?topic=code-engine-kn-install-cli)
- [Create and target a project](/docs/code-engine?topic=code-engine-manage-project)


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
    ibmcloud coligo application create --image ibmcom/helloworld --name helloworld
    ```
    {: pre}

   **Example output**

   ```
      Creating Application 'helloworld'...
      Successfully created application 'helloworld' created. Run `ibmcloud coligo application get -n 'helloworld'` to check the application status.
   ```
   {: screen}

2.  Run the `application get` command to display details about the application, which includes the URL for the `helloworld` application. 

    ```
    ibmcloud coligo application get -n helloworld
    ```
    {: pre}

   **Example output**

   ```
   Getting application 'helloworld'...
   Name: helloworld
   Namespace: 42642513-8805
   Age: 25m18s
   URL: http://helloworld.42642513-8805.us-south.knative.test.appdomain.cloud
   Console URL: https://test.cloud.ibm.com/knative/project/us-south/42642513-8805-4da8-8dbf-ae4f409f8054/application/helloworld/configuration

   Revisions:
      100%  @latest (helloworld-plnxt-1) [1] (25m15s)
        Image:  ibmcom/helloworld (pinned to b898f1)

   Conditions:
      OK   Type                  Age      Reason
      ++   ConfigurationsReady   25m1s
      ++   Ready                 24m51s
      ++   RoutesReady           24m51s
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
   Name        URL                                                                    Latest              Age     Conditions  Ready   Reason
   helloworld  http://helloworld.42642513-8805.us-south.knative.test.appdomain.cloud  helloworld-plnxt-1  19m26s  3 OK / 3    True
   Command 'application list' performed successfully
   ```
   {: screen}

4. Copy the domain URL from the previous output and call the application with `curl`.

   ```
   curl http://helloworld.42642513-8805.us-south.knative.test.appdomain.cloud
   ```
   {: pre}
   
   **Example output**

   ```
      Hello World!
   ```
   {: screen}
   
You have successfully deployed and started your first {{site.data.keyword.codeengineshort}} application!



## Application scaling (scale-to-zero and scale-from-zero)

1. Call the application. 

   ```
   curl http://helloworld.42642513-8805.us-south.knative.test.appdomain.cloud
   ```
   {: pre}
   
   **Example output**
   
   ```
   Hello World!
   ```
   {: screen}

2. List the pods of the service and notice that it has a running pod by using `kubectl`:

   ```
   kubectl get pods
   ```
   {: pre}

   **Example output**

   ```
   NAME                                            READY   STATUS    RESTARTS   AGE
   helloworld-ysqxw-2-deployment-bdc8975dd-mqn4g   2/2     Running   0          72s
   ```
   {: screen}
   
   Wait a few minutes...

3. List pods again and notice that the application has scaled the pod to zero. 

   ```
   kubectl get pods
   ```
   {: pre}

   **Example output**

   ```
   No resources found.
   ```
   {: screen}

4. Call the application again to scale from zero:

   ```
   curl http://helloworld.42642513-8805.us-south.knative.test.appdomain.cloud
   ```
   {: pre}
   
   **Example output**
   
   ```
   Hello World!
   ```
   {: screen}

Voilà!

## What have you seen?
You have deployed an arbitrary containerized application in a serverless fashion, meaning that you: 

1. Don't need to think about scaling, the environment **scales-from zero** to however many instances you need.
2. Don't need to pay for resources that are not used. The environment automatically **scales-to zero** if no requests come in.
