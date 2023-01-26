<staging>---

copyright:
  years: 2023
lastupdated: "2023-01-26"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my service binding to a DB2 Enterprise instance fail?n cos create` command failing?
{: #ts-sb-db2createfails}
{: troubleshoot}

You cannot create a {{site.data.keyword.codeengineshort}} service binding with a DB2 Enterprise service instance by using the console or CLI. You receive a failed error message.
{: tsSymptoms}

DB2 Enterprise does not support the IBM writer role that is used by default for {{site.data.keyword.codeengineshort}} service bindings.
{: tsCauses}


Try one of these solutions.
{: tsResolve}

If you are using the CLI to create the service binding with the DB2 Enterprise service instance to your {{site.data.keyword.codeengineshort}} app or job, use the `--role Manager` option when you run the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command or the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

If you are using the console to create the service binding with the DB2 Enterprise service instance to your {{site.data.keyword.codeengineshort}} app or job, specify the role of `Manager`. 




