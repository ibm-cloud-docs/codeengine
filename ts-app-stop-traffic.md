---

copyright:
  years: 2023, 2023
lastupdated: "2023-05-31"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, stopping app, preventing traffic

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Can I stop my app?   
{: #ts-app-stop-traffic}
{: troubleshoot}

You want to stop your app to prevent it from receiving traffic.
{: tsSymptoms}

You can stop your app by setting your app visibility to `project` and allowing it to scale to `0`.
{: tsCauses}


To prevent traffic from reaching your app, follow these steps.
{: tsResolve}

1. Change the minimum scale of the app to `0`. For more information, see [Setting the number of minimum and maximum instances for your app](/docs/codeengine?topic=codeengine-app-scale#scale-app-min-max).
2. Change the visibility of the app to `project` so that your app is not accessible from the public internet and network access is possible only from other Code Engine components that are running in the same project. For more information, see [Deploying your app with a project endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly).
3. Remove any custom domain mapping from your app. For more information, see [Deleting domain mappings](/docs/codeengine?topic=codeengine-domain-mappings#delete-custom-domain).
4. Remove any event subscriptions that target the app. For more information, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events). You can find information about your subscriptions by looking in the console or by running the **`sub get`** for each subscription.
5. Check your source code to make sure that traffic between components in the {{site.data.keyword.codeengineshort}} project does not target the application. 

When you complete these steps, your app does not receive traffic and scales to zero. Your app can be restarted at any time by reverting these steps. 


