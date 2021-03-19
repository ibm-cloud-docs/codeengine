---

copyright:
  years: 2021
lastupdated: "2021-03-19"

keywords: beta code engine

subcollection: codeengine

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


# Code Engine beta phase ending March 30
{: #retain-projects}

Code Engine beta phase will end March 30.
{: shortdesc}

Code Engine beta phase is ending March 30. All projects will be auto-deleted. If you want to keep your beta project(s), take action to keep your project(s).
{: important}

As we prepare for the full release, we will be removing resources from Code Engine to avoid unwanted charges. All Code Engine projects and all their contained entities such as applications, jobs and builds will be deleted automatically on March 30.

You have the option to keep your project(s) as chargeable under the terms of the generally available Code Engine service for resources consumed by running instances of your applications, jobs, and builds. For more information, see [{{site.data.keyword.codeengineshort}} pricing](https://www.ibm.com/cloud/code-engine/pricing){: external}.

## Keep a project by using the console
{: #retain-projects-console}

To keep a project and agree to the charges from the console,

1. Open [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.

2. Select **Projects** from navigation and then select a project that you want to keep from the list of projects.

3. Click **Keep this project for GA**.

4. Check to agree to the terms to keep the project and click **Confirm**.

If you change your mind and want to opt out again, you can do so before March 30 by navigating to the Project overview page and clicking **Unmark this project**. Click **Confirm**.

## Keep a project with the CLI
{: #retain-projects-cli}

To keep a project and agree to the charges from the CLI,

1. Select the project that you want to keep as current context in the CLI.

   ```
   ibmcloud ce project select --name PROJECT_NAME
   ```
   {: pre}

2. Create a configmap named `keep4ga` in that project.

   ```
   ibmcloud ce configmap create --name keep4ga --from-literal foo=bar
   ```
   {: pre}
   
The existence of a configmap with the name `keep4ga` indicates your intent to opt in and accept the charges. If you change your mind and want to opt out again, you can do so before March 30 by deleting the configmap.

```
ibmcloud ce configmap delete --name keep4ga
```
{: pre}
