---

copyright:
  years: 2021
lastupdated: "2021-09-01"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, ping, object storage

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
{:audio: .audio}
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
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
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


# Why does my {{site.data.keyword.cos_short}} subscription never become ready?
{: #ts-cossub-notready}
{: troubleshoot}

A `cos` subscription was created, but it does not have a `ready` status.
{: tsSymptoms}

Check to see whether one of the following cases is true.
{: tsCauses}

1. The Notifications Manager role is not set for your account nor project. 
2. The {{site.data.keyword.cos_short}} bucket doesn't exist, is not set to `regional` resiliency, or exists in a different region as the project.
3. An application or job is missing.

Look at the subscription source to see whether any error messages returned by running the [**`ibmcloud ce sub cos get --name SUB_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command.
{: tsResolve}

1. If the error message includes `Verify you have assigned the Notifications Manager role to your project`,
    1. Go to [Manage access and users](https://cloud.ibm.com/iam/overview) and click **Authorizations**.
    2. Click **Create**.
    3. Select `Code Engine` as the Source Service and `Cloud Object Storage` as the Target Service. 
    4. Be sure to select the **Notifications Manager** service access checkbox.
    5. Click **Authorize**.

2. If the error message includes `Error accessing bucket in region`, check the region that your project is in by running [`ibmcloud ce project current`](/docs/codeengine?topic=codeengine-cli#cli-project-current). Find your bucket region by running [`ibmcloud cos bucket-location-get --bucket BUCKET_NAME`](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-find-bucket). Both the project and bucket must be in the same region. In addition, be sure that the resiliency is set to `regional`.

3. If the error message shows `NotFound : Sink not found`, then your destination app or job is not available. Run the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command or the [**`ibmcloud ce job list`**](/docs/codeengine?topic=codeengine-cli#cli-job-list) command to make sure that your destination app or job exists. If the app or job doesn't exist, create the application with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or create the job with the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.

If these solutions do not solve your issue, retrieve the logs of the {{site.data.keyword.cos_short}} subscription for further debugging by using [{{site.data.keyword.la_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration) for log management capabilities.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).


