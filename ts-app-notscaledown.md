---

copyright:
  years: 2023, 2023
lastupdated: "2023-07-19"

keywords: troubleshooting for code engine, troubleshooting domain mapping in code engine, tips for custom domain mapping in code engine, debugging custom domain mapping in code engine, custom domain mapping and code engine, application scaling in code engine, scaling http requests in code engine, scaling, latency, concurrency, app, app instances

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why aren't my app instances scaling down as expected?
{: #ts-app-domain-notscaledown}
{: troubleshoot}

When traffic to your application slows down such that your app begins to scale down, you observe that instances do not go away. 
{: tsSymptoms}

When the incoming workload is slows to your application, {{site.data.keyword.codeengineshort}} starts to automatically scale down an application based on its configured scaling values. {{site.data.keyword.codeengineshort}} sends a SIGTERM message to your application. Your code must react to this signal and gracefully shut down. If your code does not do handle the SIGTERM message, your application instances remain in `Terminating` status for the duration of the configured request time out value (default: 300 seconds). 
{: tsCauses}


Try one of these solutions. 
{: tsResolve}

* Review the documentation about how scaling works. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

* Review the values configured for autoscaling for your application. 
    * From the console, go to the page for your application. The autoscaling settings are on the **Configuration > Runtime** tab.
    * With the CLI, run the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display details of your app. 

* Ensure that your code handles SIGTERM messages. For applications to scale down cleanly, your application code must handle a SIGTERM signal. When {{site.data.keyword.codeengineshort}} automatically scales down, a SIGTERM signal is sent to your application. 

  The following code example handles a SIGTERM message because it closes the connection to the HTTP server that was started by the app after the app receives a signal that the instance ends.

    ```javascript
    const server = // start the HTTP server

    process.on('SIGTERM', () => {
      console.info('SIGTERM signal received.');
      server.close(() => {
        console.log('Http server closed.');
      });
    });
    ```
    {: codeblock}


* Review the details of your app instances to help you troubleshoot your app. See [Getting details about app instances](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-instancedetails).


  
