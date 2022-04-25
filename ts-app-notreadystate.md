---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-25"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why doesn't my app ever become ready?   
{: #ts-app-neverready}
{: troubleshoot}

After you deploy an app, the app does not achieve a ready status.
{: tsSymptoms}

If your app is waiting and does not achieve a ready status, determine whether one of the following cases is true. 
{: tsCauses}

* Your app is deployed from repository source code and and the app displays a `waiting` status.
* By default, {{site.data.keyword.codeengineshort}} apps listen for incoming connections on port `8080`. Your app might listen on a different port if you receive the following error message,

  ```txt
  Internal error:
  RevisionFailed: Revision "myapp-1" failed with message: Initial scale was never achieved
  ```
  {: screen}



Try using the following information to resolve your problem.
{: tsResolve}

* Because your app is deployed from repository source code, check the status of the image build in the console from the app page. Click **View build** to view information about your build from repository source. The image build completes before the app is deployed. If you are using the CLI, use the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command to view imformation about your build. 

* If your app listens on a port other than port `8080`, deploy your app by using the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command in the CLI and use the `--port` option on this command to specify the port.




