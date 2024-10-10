---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-09"

keywords: domain mapping, custom domain, applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with liveness and readiness probes for your app
{: #app-probes}

With {{site.data.keyword.codeengineshort}}, you can set health checks to improve the robustness of your applications by using liveness and readiness probes. You can configure {{site.data.keyword.codeengineshort}} to use these probes when you create or update your applications. 
{: shortdesc}

## What are liveness and readiness probes?  
{: #app-probes-terms}

Use liveness and readiness probes to check whether your app is *alive* and *ready* to respond to requests and serve traffic. 

Liveness probe  
:   A liveness probe periodically checks whether the application is operational (or alive) and can respond to incoming requests. You can use a liveness probe to check whether the app is responsive to incoming requests, or if the app is in a situation that requires the system to stop the instance and start a new instance. If the liveness probe fails, the app instance is restarted. If the liveness probe succeeds, then the app instance is operational. For example, you might have a single-threaded Node.js app where the code is stuck in an endless loop, which prevents the app from responding to requests. A liveness probe can detect this case and restart the instance. No liveness probe is automatically set by default. You can configure the liveness probe with [Liveness probe properties](#app-probes-properties).

Readiness probe 
:   A readiness probe periodically checks whether the application is ready to receive traffic. You can use a readiness probe to temporarily remove an app instance from load balancing. If the readiness probe fails, the app instance cannot receive more requests until the readiness probe succeeds again. For example, consider the case where your application is able to serve requests, such as when a liveness probe returns successful. However, your app might have other required conditions before it can serve the intended user workload. Perhaps your app requires that a working connection to the backend is established before the app can respond to user requests. This scenario requires a different type of check because the state of the app is considered recoverable. Suppose that your app revision instance is in an active state for some time; however, the database connection was ended unexpectedly. The app instance needs to reconnect to the database. The app instance is in a `not ready` state because it fails the readiness probe request. As a result, the readiness probe instructs the load balancer to temporarily stop sending requests to that app instance. When the connection to the database is recovered, the readiness probe succeeds, and traffic starts to route to the app instance again. 

    By default, every app has a readiness probe that is defined of of type `tcp` and this probe checks that the configured listening port to the application is open. When this readiness check completes as successful, the app is in a ready status. You can further customize the readiness probe with [Readiness probe properties](#app-probes-properties).


Liveness and readiness probes act independently of each other. 

If you configure both a liveness and readiness probe, then the liveness probe does not wait for a first successful response from a readiness probe during the start of an app instance. If you configure both a liveness and readiness probe and you want to wait for a successful response from a liveness probe before a readiness probe request is sent, you can use the initial delay property to delay the first liveness probe request by the specified number of seconds. 


## Why use liveness and readiness probes with my apps? 
{: #app-probes-why}

When you implement probes in your {{site.data.keyword.codeengineshort}} applications, liveness and readiness probes give you more fine-grained control of your running application to check for *alive* and *ready* conditions of your application. 

For example, your app might have a startup delay. The app process might begin before the app is entirely ready, which can affect responses especially when the app scales up across many instances. By setting liveness and readiness probes as health checks, you can let {{site.data.keyword.codeengineshort}} know whether your app is running and ready to receive requests and serve traffic. By setting these probes, you can also help prevent downtime when you perform a rolling update of your app. 

Liveness and readiness probes apply for application instances. Each instance of an application is probed by the system. 

Liveness and readiness probes serve different purposes. 

* You can use a *liveness probe* to trigger an app instance restart, which basically stops the current app instance and starts a new instance. Use this probe for situations where your application cannot recover from an internal failure and the app needs to be restarted. 

* In contrast, if a *readiness probe* fails, this probe causes {{site.data.keyword.codeengineshort}} to temporarily stop routing requests to the app instance until the instance recovers. A readiness probe is useful in situations where your application encounters a problem that is recoverable without restarting the instance. During the recovery time, the app is not able to serve user requests. When the readiness probe is successful, the instance can serve user requests again. 


## Implementing a readiness or liveness probe in your code
{: #app-probes-implement}

Before you configure a readiness or liveness probe in {{site.data.keyword.codeengineshort}}, you must first implement the probe within the source code image that is referenced by your {{site.data.keyword.codeengineshort}} application.

If you do not first implement the probe in your code, then the probes that you configure in {{site.data.keyword.codeengineshort}} always fail, which causes your application to fail.

Consider the following points when you implement a readiness or liveness probe in your code.

* Determine the type of connection to use for a readiness or liveness probe. You can specify a probe of type `HTTP` or `TCP`. 
    * A probe of type `HTTP` provides an endpoint to return the probe status with an HTTP GET method. This type of probe is considered successful if the probe responds within the timeout limit, and the HTTP return code is greater than or equal to 200, but less than 400. Any value outside of this range is considered a probe failure. 
    * A probe of type `TCP` checks only that the port is open. This type of probe is considered successful if the port is open. If the port is not open, this probe type is considered failed.  

* Determine the port to which your source code responds to the probe. 
    * In general, if your app source code is opening only one port, the port configuration for the readiness or liveness probe is usually the same value as the configured listening port of your {{site.data.keyword.codeengineshort}} application. If you set the readiness or liveness probe port in {{site.data.keyword.codeengineshort}} to `0`, the port for the probe defaults to the configured listening port of the application. 
    * If your app source code listens on multiple ports simultaneously, you can use a different port in your source code to respond to readiness or liveness probe requests. In this case, you must specify the correct port for your probe when you configure the readiness or liveness probe configuration in {{site.data.keyword.codeengineshort}}.

* Because probes determine whether an app instance is available to serve requests, make sure that your code responds to probe requests quickly. 

* Make sure that your code safely handles a SIGTERM signal. When a liveness probe fails, a SIGTERM signal is sent, and your code must handle this signal to avoid unresponsive app instances. See [Why aren't my app instances scaling down as expected](/docs/codeengine?topic=codeengine-ts-app-domain-notscaledown)? 

## Configuring liveness and readiness probes in {{site.data.keyword.codeengineshort}} 
{: #app-probes-config}

You can use liveness and readiness probes as health checks for your applications. You can customize readiness probes, which are set by default, and optionally configure a liveness probe. Liveness and readiness probes are sent to application instances at the configured interval while the instances are running. 
{: shortdesc}

Before you configure a liveness probe or customize a readiness probe for your {{site.data.keyword.codeengineshort}} app, you must first implement the probes within your code; else your application might fail. 
{: important}

### Properties for liveness and readiness probes
{: #app-probes-properties}

The following table summarizes the properties that are used with liveness and readiness probes for an app. 

| Property | Description |
| --- | --- |
| Type | The type of check that the probe performs. Valid values are `tcp` and `http`. This property is required. |
| Path | The path of the HTTP request to the application. This property is required only if type is `http`. |
| Port | The port to which the probe connects. If set to `0`, the port for the probe defaults to the configured listening port of the application. |
| Interval | The amount of time in seconds between probe requests. |
| Initial delay | The amount of time in seconds to wait before the first liveness probe check is performed. |
| Timeout | The amount of time in seconds that the probe waits for a response from the app before it times out and is considered failed. |
| Failure threshold | The number of consecutive, unsuccessful checks for the probe to be considered failed. |
{: caption="Properties for liveness and readiness probes" caption-side="bottom"}


### Configuring probes from the console
{: #app-probes-config-ui}

After you implement probes in your code image that is referenced by your {{site.data.keyword.codeengineshort}} application, you can configure liveness and readiness probes from the console to perform health checks on your application. 
{: shortdesc}

Before you begin

* [Implement a probe in your code](#app-probes-implement). (*outside of {{site.data.keyword.codeengineshort}}*)

* [Create a project](/docs/codeengine?topic=codeengine-manage-project). (*from {{site.data.keyword.codeengineshort}}*)
 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. [Create an application](/docs/codeengine?topic=codeengine-cli#cli-application-create). For example, create an application that is called `myapp` that uses the `icr.io/codeengine/helloworld` image. This image is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/cron){: external}. You can configure liveness and readiness probes when you create an application. Or, you can view and update settings for liveness and readiness probes when you update an application from the **Configuration** > **Image start options** tab on your application page. 
2. To view the configured probes and their properties for an app, go to the **Configuration** > **Image start options** tab on your application page. 
3. Edit the liveness and readiness probe settings from the **Image start options** tab. Modifying a probe creates a new application revision. For example, edit the default readiness probe to change the connection type from TCP to HTTP, and set the path for the readiness probe to `/readinessprobe`. See [properties](#app-probes-properties) for more information about the probe properties. Click **Done** when finished. 
4. Click **Deploy** to save your change and deploy the app revision with the configured probe settings.

Use the view on the **Instances** tab to check the application instances. 
{: tip}

### Configuring probes with the CLI
{: #app-probes-config-cli}

You can work with liveness and readiness probes with the {{site.data.keyword.codeengineshort}} CLI. Specify the `--probe-live` or `--probe-ready` option with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command to configure the probe that you want. 
{: shortdesc}

For more information about the properties that you can configure with a readiness or liveness probe, see [Liveness and readiness probe properties](#app-probes-properties).


Before you begin

* [Implement a probe in your code](#app-probes-implement). After you implement a probe in your code (*outside of {{site.data.keyword.codeengineshort}}*), you can configure your {{site.data.keyword.codeengineshort}} application to work with the probe. 

* From {{site.data.keyword.codeengineshort}}:
    * Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
    * [Create a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create an application with the [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. In the following example, use `myapp` as the name of the application and specify `icr.io/codeengine/helloworld` as the image to reference. 

    ```txt
    ibmcloud ce application create --name myapp --image icr.io/codeengine/helloworld
    ```
    {: pre}

2. Run the **`application get`** command to display the details about the app. Notice that the readiness probe is configured by default. 

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Readiness Probe:    
        Type:              tcpsocket  
        Port:              0  
    [...]
    ```
    {: screen}

3. Update the `myapp` application with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command to configure a liveness probe. For example, specify the `--probe-live` option to configure a liveness probe of type HTTP such that the connection uses port 8080, and the path to the home directory of your referenced code image** is `/`. 

    When you configure properties for a readiness or liveness probe on the **`application create`** or **`application update`** commands, you must provide the option `--probe-live` or `--probe-ready` before each property that you set. 
    {: note}

    ```txt
    ibmcloud ce application update --name myapp --probe-live type=http --probe-live path=/ --probe-live port=8080
    ```
    {: pre}

4. Run the **`application get`** command to display the details about the updated `myapp` application. The details include information about the configured liveness probe.

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Liveness Probe:     
        Type:              httpget  
        Path:              /  
        Port:              8080  
        Interval:          10  
        Timeout:           1  
        FailureThreshold:  1  

    Readiness Probe:    
        Type:              tcpsocket  
        Port:              0  
    [...]
    ```
    {: screen}

Now that you configured both a liveness and readiness probe for your `myapp` application, the system constantly performs both probes according to their configuration.

## Viewing probe settings in {{site.data.keyword.codeengineshort}} 
{: #app-probes-view}

You can view information about liveness and readiness probes that are set in {{site.data.keyword.codeengineshort}} from the console and with the CLI.

### Viewing probe settings from the console
{: #app-probes-view-ui}

To view details about your configured liveness and readiness probes in the console, go to the **Configuration** > **Image start options** tab on your application page. 


### Viewing probe settings with the CLI
{: #app-probes-view-cli}

To view details about your application with the CLI, including information about configured liveness and readiness probes, run the **`application get`** command. 

```txt
ibmcloud ce application get --name myapp
```
{: pre}

Example output 

```txt
[...]
OK

Name:               myapp
ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:       myproject
[...]
Liveness Probe:     
    Type:              httpget  
    Path:              /  
    Port:              8080  
    Interval:          10  
    Timeout:           1  
    FailureThreshold:  1  

Readiness Probe:    
    Type:              tcpsocket  
    Port:              0  
[...]
```
{: screen}


## Updating probes
{: #app-probes-update}

You can modify the properties for liveness and readiness probes for your applications. When you update the properties of a probe, a new application revision is created. liveness and readiness probes are sent to application instances at the configured interval while the instances are running.
{: shortdesc}

### Updating probes from the console
{: #app-probes-update-ui}

You can modify or edit a readiness or liveness probe in the console, from the **Configuration** > **Image start options** tab on your application page. 

1. Go to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. From the application page, click the  **Configuration** > **Image start options** tab on your application page. 
3. Edit the liveness and readiness probe settings from the **Image start options** tab. Modifying a probe creates a new application revision. Click **Edit** to modify the readiness or liveness probe that you want to change. 
4. From the **Readiness probe** page or the **Liveness probe** page, update the [properties](#app-probes-properties) of your probe. Click **Done** when finished. 
5. Click **Deploy** to save your change and deploy the app revision with the configured probe settings.

Use the view on the **Instances** tab to check the application instances. 
{: tip}


### Updating probes with the CLI
{: #app-probes-update-cli}

Suppose that you want to update the liveness probe for `myapp` such that the connection type is HTTP and the failure threshold is 3 and the interval between probe requests is 5 seconds. 

1. Update the `myapp` application with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command to update the liveness probe such that the connection type is HTTP, the failure threshold is 3, and the interval between probe requests is 5 seconds.  

    When you configure properties for a readiness or liveness probe on the **`application create`** or **`application update`** commands, you must provide the option `--probe-live` or `--probe-ready` before each property that you set. 
    {: note}

    ```txt
    ibmcloud ce application update --name myapp --probe-live type=http --probe-live interval=5 --probe-live failure-threshold=3
    ```
    {: pre}

2. Run the **`application get`** command to display the details about the updated `myapp` application. The details include information about the current configuration for the liveness probe.

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Liveness Probe:     
        Type:              httpget  
        Path:              /  
        Port:              8080  
        Interval:          5  
        Timeout:           1  
        FailureThreshold:  3  

    Readiness Probe:    
        Type:              tcpsocket  
        Port:              0  
    [...]
    ```
    {: screen}
   
3. Update the `myapp` application with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command to update the readiness probe such that the connection type is HTTP, the port is 8080, the failure threshold is 3, and the interval between probe requests is 5 seconds. 

    When you configure properties for a readiness or liveness probe on the **`application create`** or **`application update`** commands, you must provide the option `--probe-live` or `--probe-ready` before each property that you set. 
    {: note}

    ```txt
    ibmcloud ce application update --name myapp --probe-ready type=http --probe-ready port=8080 --probe-ready interval=5 --probe-ready failure-threshold=3
    ```
    {: pre}

4. Run the **`application get`** command to display the details about the updated `myapp` application. The details include information about the updated setting for the readiness probe. 

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Liveness Probe:     
        Type:              httpget  
        Path:              /  
        Port:              8080  
        Interval:          5  
        Timeout:           1  
        FailureThreshold:  3  

    Readiness Probe:    
        Type:              httpget  
        Path:              /  
        Port:              8080  
        Interval:          5  
        Timeout:           1  
        FailureThreshold:  3  
    [...]
    ```
    {: screen}


## Deleting probes
{: #delete-probes}

You can remove (delete) a liveness probe. However, because a readiness probe is always set by default, you can only edit to update the properties of a readiness probe. 


### Deleting probes from the console
{: #app-probes-delete-ui}

From the console, you can remove a liveness probe from the **Configuration** > **Image start options** tab on your application page. 

1. Go to your application page. One way to navigate to your application page is to 
    * Locate the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
    * Click the name of your project to open the Overview page.
    * Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
2. From the application page, click the  **Configuration** tab and then the **Image start options** tab on your application page. 
3. To remove a liveness probe, you must create a new application revision. 
    1. Click **Delete** to remove the liveness probe. 
    2. Click **Deploy** to save your change and deploy the app revision.

While you cannot delete a readiness probe, you can [update](#app-probes-update-ui) it. 


### Deleting probes with the CLI
{: #app-probes-delete-cli}


1. To remove the liveness probe, update the `myapp` application with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command with the `--probe-live-clear` option. 

    ```txt
    ibmcloud ce application update --name myapp --probe-live-clear
    ```
    {: pre}

2. Run the **`application get`** command to display the details about the updated `myapp` application. The liveness probe is deleted. 

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Readiness Probe:    
        Type:              httpget  
        Path:              /  
        Port:              8080  
        Interval:          5  
        Timeout:           1  
        FailureThreshold:  3   
    [...]
    ```
    {: screen}
   
3. To reset the readiness probe to the default configuration, update the `myapp` application with the [**`ibmcloud ce application update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command with the `--probe-ready-reset` option.  

    ```txt
    ibmcloud ce application update --name myapp --probe-ready-reset
    ```
    {: pre}

4. Run the **`application get`** command to display the details about the updated `myapp` application. The readiness probe is reset to the default configuration. 

    ```txt
    ibmcloud ce application get --name myapp
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Readiness Probe:    
        Type:              tcpsocket  
        Port:              0  
    [...]
    ```
    {: screen}
