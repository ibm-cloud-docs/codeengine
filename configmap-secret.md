---

copyright:
  years: 2020
lastupdated: "2020-07-27"

keywords: code engine, configmap, secret

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

# Working with configmaps and secrets
{: #configmap-secret} 

Learn how to work with configmaps and secrets with your jobs and applications in {{site.data.keyword.codeengineshort}}. In {{site.data.keyword.codeengineshort}}, you can store your information in key-value pairs in secrets or configmaps that can be consumed by your job runs or application deployments by using environment variables. Values can be specified literally or as references into secrets or configmaps. 
{: shortdesc}

## What are configmaps and secrets and why would I use them? 
{: #configmapsec-whatwhy}

In {{site.data.keyword.codeengineshort}}, both secrets and configmaps are key-value pairs such that any environment variables that are set have a name corresponding to the "key" of each entry in those maps, and the value of the environment variable is the value of that key.

A *configmap* provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environmental variables, you can decouple specific information from your deployment and keep your app or job portable. Configmaps contain information in key-value pairs. You can create and work with configmaps from the console or from the CLI.

A *secret* provides a method to include sensitive configuration information, such as passwords or ssh keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Note that anyone who is authorized to your project can also view your secrets so be sure that you know the secret information can be shared with those users. Secrets contain information in key-value pairs. You can create and work with secrets from the console or from the CLI.

By using configmaps (for non-sensitive data) and secrets (for sensitive data) you can manage input and data for your applications and jobs. For sensitive data, use secrets instead of configmaps.

## Creating configmaps
{: #configmap-create}

### Creating a configmap from the console
{: #configmap-create-ui}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).  

1. After your project is in **Active** status, click the name of your project on the Projects page.
2. From the Components page, click **Config**.  
3. From the Create Config page:
    * Choose your configuration type. 
    * Provide a name for this configmap.
    * Specify one or more our key-value pairs for this configmap. 
    * Click **Config Maps** to create the configmap. 
4. Now that your configmap is created from the console, navigate to the Config page to view details about your configmap. 

### Creating a configmap with the CLI
{: #configmap-create-cli}

Before you begin:

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create a configmap with the `configmap create` command in one of the following ways: 

**QUESTION Any guidance on when user would want to use --from-literal vs --from-file?**

* Create a configmap that is named `configmap-fromfile` by using the `--from-file` option. Let's use a file that is named `TARGET` (no extension) which contains the value `Happy Day`. For example: 

    ```
    ibmcloud ce configmap create --name configmap-fromfile --from-file ./TARGET
    ```
    {: pre}

   **Example output**
   
   ```
    Creating configmap 'configmap-fromfile'...
    OK
    Successfully created configmap 'configmap-fromfile'. Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce configmap get -n configmap-fromfile' to see more details.
   ```
   {: screen}

* Create a configmap that is named `configmap-fromlit` by using the `--from-literal` option. For example: 

    ```
    ibmcloud ce configmap create --name configmap-fromlit --from-literal TARGET=Sunshine
    ```
    {: pre}

   **Example output**
   
   ```
    Creating configmap 'configmap-fromlit'...
    OK
    Successfully created configmap 'configmap-fromlit'. Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce configmap get -n configmap-fromlit' to see more details.
   ```
   {: screen}

2.  Now that configmaps are created, use the `configmap list` command to list all configmaps in your project or use the `configmap get` command to display details about a specific configmap. For example:

    ```
    ibmcloud ce configmap get --name configmap-fromfile
    ```
    {: pre}

   **Example output**
   
   ```
    Getting configmap 'configmap-fromfile'...
    Name:        configmap-fromfile
    Namespace:   f6629592-edf4
    Labels:      <none>
    Annotations: <none>

    Data
    ====
    TARGET:
    ----
    Happy Day
    Events:  <none>

    OK
    Successfully performed 'configmap get configmap-fromfile' command
   ```
   {: screen}

## Using configmaps with jobs or apps
{: #configmap-using}

After defining your configmap, your jobs or apps can use the configmap. 

To use a configmap from a job, specify the `--env-fromconfigmap` option on the `jobdef create`, `jobdef update`, `job run` or `job update` commands. Similarly, to use a configmap from an application, specify the `--env-fromconfigmap` option on the `app create` or `app update` commands.  

### Using configmaps with job or apps from the console 
{: #configmap-using-ui}

TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD 

### Using configmaps with job or apps with the CLI 
{: #configmap-using-cli}

Let's use a previously defined configmap with an application. 

1.  Create your app by using the `app create` command. For this example, let's create a {{site.data.keyword.codeengineshort}} app by using the [`Hello World`](https://hub.docker.com/r/ibmcom/helloworld) image in Docker Hub. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.

    ```
    ibmcloud ce app create --name myhelloapp --image ibmcom/helloworld
    ```
    {: pre}

2. Call the application. You can obtain the URL for your app by using the `app get` command. 

    ```
    curl https://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    StatusCode        : 200
    StatusDescription : OK
    Content           : Hello World! (revision: myhelloapp-xvlbz-1)

    RawContent        : HTTP/1.1 200 OK
                        x-envoy-upstream-service-time: 26
                        Content-Length: 44
                        Content-Type: text/plain; charset=utf-8
                        Date: Fri, 24 Jul 2020 12:30:11 GMT
                        Server: istio-envoy

                        Hello World! (revision: myh...
    Forms             : {}
    Headers           : {[x-envoy-upstream-service-time, 26], [Content-Length, 44], [Content-Type, text/plain; charset=utf-8],
                        [Date, Fri, 24 Jul 2020 12:30:11 GMT]...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 44
   ```
   {: screen}

2. Update the app to use the previously defined `configmap-fromfile` configmap. 

    ```
    ibmcloud ce app update --name myhelloapp --env-from-configmap configmap-fromfile
    ```
    {: pre}

   **Example output**
   
   ```
    Application 'myhelloapp' updated to latest revision and is available at URL:
    http://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

3.  Call the application again.  This time, the app returns `Hello Happy Day!` which is the value specified in the `configmap-fromfile` configmap.
    ```
    curl http://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    StatusCode        : 200
    StatusDescription : OK
    Content           : Hello Happy Day! (revision: myhelloapp-xvlbz-2)

    RawContent        : HTTP/1.1 200 OK
                        x-envoy-upstream-service-time: 72
                        Content-Length: 48
                        Content-Type: text/plain; charset=utf-8
                        Date: Fri, 24 Jul 2020 12:34:28 GMT
                        Server: istio-envoy

                        Hello Happy Day! (revision:...
    Forms             : {}
    Headers           : {[x-envoy-upstream-service-time, 72], [Content-Length, 48], [Content-Type, text/plain; charset=utf-8],
                        [Date, Fri, 24 Jul 2020 12:34:28 GMT]...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 48
   ```
   {: screen}

4. Update the app again to use the `configmap-fromlit` configmap. 

Because we are updating the same `TARGET` environment variable for the `myhelloapp` application with both configmaps, the value for `TARGET` is replaced. 

If the name of your key (of your key-value pair environment variable) is different for your configmaps, then when the value of the key-value pair in the configmap is changed, the value is appended to the configmap. If the name of your key in your  key-value pair environment variable is different for your configmaps, then the value of the key is appended to the configmap.
{: note}

    ```
    ibmcloud ce app update --name myhelloapp --env-from-configmap configmap-fromlit
    ```
    {: pre}

   **Example output**
   
   ```
    Updating application 'myhelloapp'
    Application 'myhelloapp' updated to latest revision and is available at URL:
    http://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

5. Call the application again.  This time, we see that the app returns `Hello Sunshine!` which is the value specified in the `configmap-fromlit` configmap.

    ```
    curl http://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    StatusCode        : 200
    StatusDescription : OK
    Content           : Hello Sunshine! (revision: myhelloapp-xvlbz-3)

    RawContent        : HTTP/1.1 200 OK
                        x-envoy-upstream-service-time: 6
                        Content-Length: 47
                        Content-Type: text/plain; charset=utf-8
                        Date: Fri, 24 Jul 2020 12:36:30 GMT
                        Server: istio-envoy

                        Hello Sunshine! (revision: m...
    Forms             : {}
    Headers           : {[x-envoy-upstream-service-time, 6], [Content-Length, 47], [Content-Type, text/plain; charset=utf-8],
                        [Date, Fri, 24 Jul 2020 12:36:30 GMT]...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 47
     ```
   {: screen}

6. To change the value of key-value pair in a configmap, use the `configmap update` command to update the configmap.  Let's update the `configmap-lit` configmap to change the value of the `TARGET` key from `Sunshine` to `Stranger.

    ```
    ibmcloud ce configmap update --name configmap-fromlit --from-literal TARGET=Stranger
    ```
    {: pre}

7. Call the application again.  This time, we see that the app returns `Hello Stranger!` which is the updated value specified in the `configmap-lit` configmap. **FMO RECAPTURE OUTOUT AFTER DEV MAKES FIX**

    ```
    curl https://myhelloapp.f6629592-edf4.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    StatusCode        : 200
    StatusDescription : OK
    Content           : Hello Stranger!
                        ! (revision: myhelloapp-xvlbz-3)

    RawContent        : HTTP/1.1 200 OK
                        x-envoy-upstream-service-time: 4994
                        Content-Length: 63
                        Content-Type: text/plain; charset=utf-8
                        Date: Fri, 24 Jul 2020 12:44:00 GMT
                        Server: istio-envoy

                        Hello Sunshine!
    Forms             : {}
    Headers           : {[x-envoy-upstream-service-time, 4994], [Content-Length, 63], [Content-Type, text/plain; charset=utf-8],
                        [Date, Fri, 24 Jul 2020 12:44:00 GMT]...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 63
   ```
   {: screen}

## Creating secrets
{: #secret-create}

Use secrets to provide sensitive information to your apps or jobs. Secrets are defined in key-value pairs.

You can create a secret with the CLI where the secret is stored in a registry, in a file, or specified with the `secret create` command. Secrets that are stored in a file or created with the `secret create` command are called *generic secrets*  Secrets that are used to pull an image from a private container registry are called *pull secrets*. 

### Creating a secret from the console
{: #secret-create-ui}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).  

TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD 


### Creating a secret with the CLI
{: #secret-create-cli}

Before you begin:

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create a generic secret with the `secret create` command or by key-value pairs that are stored in a file.  


* Create a secret that is named `secret-fromfile` by using the `--from-file` option. For example: 

    ```
    ibmcloud ce secret create --name mysecret-fromfile  --from-file ./username.txt --from-file ./password.txt
    ```
    {: pre}

   **Example output**
   
   ```
    Creating secret mysecret-fromfile...
    OK
    Successfully created secret 'mysecret-fromfile'.
   ```
   {: screen}

* Create a secret that is named `secret-fromliteral` by using the `--from-literal` option. For example: 

    ```
    ibmcloud ce secret create --name mysecret-lit --from-literal username=devuser --from-literal password='S!B\*d$zDsb'
    ```
    {: pre}

   **Example output**
   
   ```
    Creating secret secret-lit...
    OK
    Successfully created secret 'secret-lit'.
   ```
   {: screen}

2. Create a pull secret with the `secret create` command by specifying a the registry that contains the secret.  
    ```
    ibmcloud ce secret create --name mysecret-fromimage --from-registry us.icr.io --username myusername --password 39c-fa445-9773ac48a92
    ```
    {: pre}

   **Example output**
   
   ```
    Creating secret mysecret-fromimage...
    OK
    Successfully created secret 'mysecret-fromimage'.
   ```
   {: screen}

3.  Now that secrets are created, use the `secret list` command to list all secrets in your project or use the `secret get` command to display details about a specific secret. For example:

    ```
    ibmcloud ce secret get --name secret-fromfile
    ```
    {: pre}

   **Example output**
   
   ```
    Getting secret mysecret-fromfile...
    Name:        mysecret-fromfile
    Namespace:   f6629592-edf4
    Labels:      <none>
    Annotations: <none>

    Type: generic

    Data
    ====

    password.txt:   20 bytes
    username.txt:   10 bytes
    OK
    Successfully performed 'secret get mysecret-fromfile.
   ```
   {: screen}

## Using secrets with jobs or apps
{: #secret-using}

After defining your secret, your jobs or apps can consume and use the secret. 


### Using secrets with job or apps from the console 
{: #secret-using-ui}

TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD TBD 

### Using secrets with job or apps with the CLI 
{: #secret-using-cli}

To use a secret from a job, specify the `--env-fromsecret` option on the `jobdef create`, `jobdef update`, `job run` or `job update` commands. Similarly, to reference a secret from an application, specify the `--env-fromsecret` option on the `app create` or `app update` commands.  

**WHAT APP CAN WE USE A SECRET WITH??  DO I NEED TO SHOW EXAMPLE STEPS?**


