---

copyright:
  years: 2021
lastupdated: "2021-03-09"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions

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
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
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


# Troubleshooting tips for subscriptions
{: #troubleshoot-subscriptions}

Use the tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} subscriptions.
{: shortdesc}

## Why is my `cos subscription create` command failing?
{: #ts-cossub-create}
{: troubleshoot}

{: tsSymptoms}
You cannot create an {{site.data.keyword.cos_full_notm}} subscription through the CLI by using the following command: `ibmcloud ce subscription cos create` and you receive an error that mentions various `failed` messages.

{: tsCauses}
If you cannot create an {{site.data.keyword.cos_short}} subscription, determine whether one of the following cases is true,

1. The name of your subscription is not unique within the project. 

2. The application reference doesn't exist. An error with the following message appears, `Failed to retrieve the application. View available applications by running ibmcloud ce app list`.

3. A timeout occurs. Error message mentions `Getting COS event subscription status timed out`

{: tsResolve}
Try one of these solutions,

1. Run the [`ibmcloud ce sub cos list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-list) command to list all defined {{site.data.keyword.cos_short}} subscriptions and check whether a subscription with the same name exists. If a subscription with the same name exists, run the [`ibmcloud ce sub cos delete --name SUB_NAME`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) to delete the old subscription. The name of the subscription must be unique within your project.

2. Run [`ibmcloud ce app list`](/docs/codeengine?topic=codeengine-cli#cli-application-list) to make sure that your destination app exists. If the app doesn't exist, create the application with the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

3. Try the solutions in [Why does my {{site.data.keyword.cos_short}} subscription never become ready?](#ts-cossub-notready).

## Why does my {{site.data.keyword.cos_short}} subscription never become ready?
{: #ts-cossub-notready}
{: troubleshoot}

{: tsSymptoms}
A `cos` subscription was created, but it does not have a `ready` status.

{: tsCauses}
Check to see whether one of the following cases is true,

1. The Notifications Manager role is not set for your account nor project. 
2. The {{site.data.keyword.cos_short}} bucket doesn't exist, is not set to `regional` resiliency, or exists in a different region as the project.
3. An application is missing.

{: tsResolve}
Look at the subscription source to see whether any error messages returned by running the [`ibmcloud ce sub cos get --name SUB_NAME`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command.

1. If the error message includes `Verify you have assigned the Notifications Manager role to your project`,
   1. Go to [Manage access and users](https://cloud.ibm.com/iam/overview) and click **Authorizations**.
   2. Click **Create**.
   3. Select `Code Engine` as the Source Service and `Cloud Object Storage` as the Target Service. 
   4. Be sure to select the **Notifications Manager** service access checkbox.
   5. Click **Authorize**.
   
2. If the error message includes `Error accessing bucket in region`, check the region that your project is in by running [`ibmcloud ce project current`](/docs/codeengine?topic=codeengine-cli#cli-project-current). Find your bucket region by running [`ibmcloud cos bucket-location-get --bucket BUCKET_NAME`](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-find-bucket). Both the project and bucket must be in the same region. In addition, be sure that the resiliency is set to `regional`.

3. If the error message shows `NotFound : Sink not found`, then your destination app is not available. Run [`ibmcloud ce app list`](/docs/codeengine?topic=codeengine-cli#cli-application-list) to make sure that your destination app exists. If it doesn't, create the application with the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

If these solutions do not solve your issue, retrieve the logs of the {{site.data.keyword.cos_short}} subscription for further debugging by using [{{site.data.keyword.la_full_notm}}]((/docs/codeengine?topic=codeengine-view-logs) for log management capabilities.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).

## Why is my `ping subscription create` failing?
{: #ts-pingsub-create}
{: troubleshoot}

{: tsSymptoms}
You cannot create a ping subscription through the CLI by using the `ibmcloud ce subscription ping create` command and you receive an error that mentions `failed` in the message.

{: tsCauses}
If you cannot create a ping subscription, determine whether one of the following cases is true,

1. The name of your subscription is not unique within the project. 
2. The application reference doesn't exist. An error with the following message appears: `Failed to retrieve the application. View available applications by running ibmcloud ce app list`.

{: tsResolve}
Try one of these solutions,

1. Run the [`ibmcloud ce sub ping list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-list) command to list all defined ping subscriptions and check whether a subscription with the same name exists. If a subscription with the same name  exists, use the [`ibmcloud ce sub ping delete --name SUB_NAME`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-delete) to delete the old subscription. The name of the subscription must be unique within your project.

2. Run [`ibmcloud ce app list`](/docs/codeengine?topic=codeengine-cli#cli-application-list) to make sure that your destination app exists. If the app doesn't exist, create the application with the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).

## Why does my ping subscription never become ready?
{: #ts-pingsub-notready}
{: troubleshoot}

{: tsSymptoms}
A ping subscription was created, but it does not have a `ready` status.

{: tsCauses}
The destination app does not exist.

{: tsResolve}
Look at the ping source to see whether any error messages returned by using the [`ibmcloud ce sub ping get --name SUB_NAME`](/docs/codeengine?topic=codeengine-cli#cli-subscription-ping-get). If the error message shows `NotFound : Sink not found`, then your destination app is not available. Use [`ibmcloud ce app list`](/docs/codeengine?topic=codeengine-cli#cli-application-list) to verify that your destination app exists. If the app doesn't exist, create the application with the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

If these solutions do not solve your issue, try one of the resources in [getting support](/docs/codeengine?topic=codeengine-get-support).
