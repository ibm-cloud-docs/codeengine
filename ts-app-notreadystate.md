---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-15"

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

1. Your app is deployed from repository source code and the app displays a `waiting` status.
2. Your app is deployed from local source code and the app displays a `waiting` status.
3. By default, {{site.data.keyword.codeengineshort}} apps listen for incoming connections on port `8080`. Your app might listen on a different port if you receive the following error message,

    ```txt
    Internal error:
    RevisionFailed: Revision "myapp-1" failed with message: Initial scale was never achieved
    ```
    {: screen}

Try using the following information to resolve your problem.
{: tsResolve}

1. If your app is deployed from repository source code, check the status of the image build. The image build completes before the app is deployed. From the app page in the console, click **View build** to view information about your build from repository source. If you are using the CLI, use the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command to view information about your build. 

2. If your app is deployed from local source code, check the status of the image build. The image build completes before the app is deployed. Use the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command from the CLI to view information about your build. 

3. If your app listens on a port other than port `8080`, deploy your app by using the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command in the CLI and use the `--port` option on this command to specify the port. Note that the following ports are reserved by {{site.data.keyword.codeengineshort}}:  `8022`, `8008`, `8012`, `9090`, `9091`, and `15090`.  




