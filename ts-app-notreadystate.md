---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-18"

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

By default, {{site.data.keyword.codeengineshort}} apps listen for incoming connections on port `8080`.
{: tsCauses}

Your app might listen on a different port if you receive the following error message,

```txt
Internal error:
RevisionFailed: Revision "myapp-1" failed with message: Initial scale was never achieved
```
{: screen}

If your app listens on a port other than port `8080`, deploy your app by using the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command in the CLI and use the `--port` option on this command to specify the port.
{: tsResolve}



