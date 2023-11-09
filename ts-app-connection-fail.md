---

copyright:
  years: 2023, 2023
lastupdated: "2023-11-09"

keywords: troubleshooting for code engine, troubleshooting connections in code engine, tips for app connections in code engine, debugging connections in code engine, app connectivity and code engine, app connection fails

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my app connection fail?
{: #ts-app-connection-fail}
{: troubleshoot}

Your application connects to another service, such as a database. When your app runs, you notice that the connection ends unexpected and you receive an error similar to the following example.
{: tsSymptoms}

```txt
[IBM][CLI Driver] SQL30081N  A communication error has been detected. Communication protocol being used: "SSL". 
```
{: screen}


By default, your app times out after 5 minutes. If it does not receive any updates from the connection within this time, then your app ends the connection. For more information, see [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application).
{: tsCauses}

You can resolve this issue by changing the timeout value for your app. If your app requires a connection time that is longer than 10 minutes, configure your app to include a a heartbeat connection to the other service, which keeps your connection active. 
{: tsResolve}

You can also run a {{site.data.keyword.codeengineshort}} job and then return the output to your app. For more information about jobs, see [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).

For more information about troubleshooting app connection failures when using a proxy, see [Why does my app connection fail when using a proxy](/docs/codeengine?topic=codeengine-ts-app-connection-failwithproxy)?




## Updating your app timeout value from the console
{: #ts-app-timeout-console}

To update your app from the console,

1. Open the [Code Engine console](https://cloud.ibm.com/codeengine/overview){: external}.
2. Click the project that contains your app and then click the app to open the **Overview** page.
3. Click **Edit and create a new revision**.
4. Select **Runtime** and then change the value in the **Request timeout (seconds)** field. The maximum value is 600 seconds (10 minutes). 
5. Click **Save and create**.

## Updating your app timeout value with the CLI
{: #ts-app-timeout-cli}

To update your app with the CLI, run the [**app update**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command with the `--request-timeout` option set to the new timeout value. The maximum value is 600 seconds (10 minutes).


After your app is updated, {{site.data.keyword.codeengineshort}} creates a revision of your app. When the app revision reaches a `Ready` state, all traffic is routed to this new instance.



