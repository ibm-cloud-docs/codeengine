---

copyright:
  years: 2021
lastupdated: "2021-08-12"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, cron, ping, object storage, 

subcollection: codeengine

content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note .note}
{:note: .note}
{:note:.deprecated}
{:objectc data-hd-programlang="objectc"}
{:objectc: .ph data-hd-programlang='Objective C'}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Why does my subscription show errors when trying to deliver the events?
{: #ts-subscription-deliveryerrors}
{: troubleshoot}

Subscription events were created, but errors are received when trying to deliver the events to your {{site.data.keyword.codeengineshort}} application or job.
{: tsSymptoms} 

Check to see whether one of the following cases is true.
{: tsCauses}

1. Does the subscription destination application or job exist? 
2. Is the destination app or job prepared and looking for HTTP POST messages?

Look at the subscription source to see whether any error messages are returned. For {{site.data.keyword.cos_full_notm}} subscriptions, use the [**`ibmcloud ce sub cos get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command. For cron subscriptions, use [**`ibmcloud ce sub cron get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-get) command.
{: tsResolve}

1. Confirm that your subscription destination exists. 
* If your subscription destination is an application, use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to confirm that your application exists and that it wasn't deleted. Check that the status of your application is `Ready`. You can also use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to display the current status of the application. 
* If your subscription destination is an job, use the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to confirm that your job exists. You can also use the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to display the current status of the job. 


For more information about {{site.data.keyword.cos_short}} subscriptions, see [Working with the {{site.data.keyword.cos_short}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

For more information about cron subscriptions, see [Working with the cron event producer](/docs/codeengine?topic=codeengine-subscribe-cron).

2. The error message that your subscription source receives might include a `404 Not Found` error or a `5xx HTTP` error. If you receive either of these errors, then confirm that your destination application is expecting to receive event information as POST HTTP requests. Event information is received as POST HTTP requests for applications and as environment variables for jobs.

If these solutions do not solve your issue, retrieve the logs of your subscription destination application or job. For apps, use the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command. For jobs, use the  [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command to obtain the logs for your specific jobrun. 

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).
