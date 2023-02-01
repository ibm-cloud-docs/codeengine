---

copyright:
  years: 2023
lastupdated: "2023-02-01"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my service binding to a Db2 Enterprise instance fail?
{: #ts-sb-db2createfails}
{: troubleshoot}

You cannot create a {{site.data.keyword.codeengineshort}} service binding with a Db2 Enterprise service instance when you use the CLI or API. You receive a failed error message.
{: tsSymptoms}

Db2 Enterprise does not support the IBM writer role that is used by default for {{site.data.keyword.codeengineshort}} service bindings.
{: tsCauses}


Try one of these solutions.
{: tsResolve}

1. If you are using the CLI to create the service binding with the Db2 Enterprise service instance to your {{site.data.keyword.codeengineshort}} app or job, use the `--role Manager` option when you run the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command or the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

2. Use the console to create the service binding with the Db2 Enterprise service instance to your {{site.data.keyword.codeengineshort}} app or job, and specify the role of `Manager`. 



