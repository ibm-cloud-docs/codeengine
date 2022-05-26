---

copyright:
  years: 2022
lastupdated: "2022-05-26"

keywords: troubleshooting, issues, status, get help, code engine, getting help

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting overview
{: #troubleshooting_over}

Review some general help for troubleshooting issues with {{site.data.keyword.codeenginefull}}.
{: shortdesc}

## General ways to resolve issues
{: #help-general}

* Make sure that your command-line tools are up-to-date.
    * In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and options.
    * Update the `ibmcloud ce` CLI plug-in whenever an update is available. For more information, see [Updating the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli#update-cli)
    * When you use any of the CLI `get` commands, such as the **`app get`**, **`job get`**, **`jobrun get`**, **`build get`**, or **`buildrun get`** commands, you can specify the `--o yaml` option to obtain more fine-grained details about your {{site.data.keyword.codeengineshort}} component, which can be helpful in troubleshooting. For more information about the `get` commands, see [CLI Reference](/docs/codeengine?topic=codeengine-cli).
* Review the other troubleshooting issues for {{site.data.keyword.codeengineshort}}.
* Review the [FAQs](/docs/codeengine?topic=codeengine-faqs).
* Enable and review [logging](/docs/codeengine?topic=codeengine-view-logs) and [monitoring](/docs/codeengine?topic=codeengine-monitor) details to troubleshoot your {{site.data.keyword.codeengineshort}} components.

## Reviewing Cloud issues and status
{: #help-cloud-status}

1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Code Engine** component and review any cloud status issue.
3. Review the [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
4. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM open source and third-party policy](https://www.ibm.com/support/pages/node/737271){: external}.

## Getting help
{: #help-functions}

If you still cannot resolve your issue, see [Getting support](/docs/codeengine?topic=codeengine-get-support). For any general questions or feedback, post in Slack.



