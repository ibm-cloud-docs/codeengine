---

copyright:
  years: 2021
lastupdated: "2021-08-19"

keywords: third party, ibm cloud integrations, integrations, code engine, third-party

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


# Supported integrations for {{site.data.keyword.codeengineshort}}
{: #supported-integrations}

{{site.data.keyword.codeenginefull}} supports or is supported by the following {{site.data.keyword.cloud_notm}} and third-party integrations.
{: shortdesc}

## {{site.data.keyword.cloud_notm}} integrations
{: #supported-cloud-integrations}

| Integration | Description | 
|-----------|------------------|
| {{site.data.keyword.at_full_notm}} | View, manage, and audit user-initiated activities made in your {{site.data.keyword.codeengineshort}} service instance (project). For more information, see [Auditing events for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-at_events). |
| {{site.data.keyword.mon_full_notm}} | Use the {{site.data.keyword.mon_full}} service to monitor your {{site.data.keyword.codeengineshort}} workloads. For more information, see [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor). |
| {{site.data.keyword.la_full_notm}} | Add log management capabilities to your project by creating a {{site.data.keyword.la_short}} instance. For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs). |
| {{site.data.keyword.registrylong_notm}} | Set up your own container registry to safely store and share images. For more information, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started). |
| {{site.data.keyword.cos_full_notm}} | Subscribe to Object storage event producers from your application or job. For more information, see [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer). |
{: caption="Table 1. {{site.data.keyword.cloud_notm}} integrations" caption-side="top"}

## Third-party integrations
{: #supported-third-integrations}

{{site.data.keyword.codeengineshort}} is supported by the following third-party integrations. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM open source and third-party policy](https://www.ibm.com/support/pages/node/737271){: external}.

| Integration | Description | 
|-----------|------------------|
| Lithops | [Lithops](https://lithops-cloud.github.io/) is an open source framework that designed to massively scale your Python applications. See [Running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops). | 
| Ray | [Ray](https://ray.io/){: external} is an open technology that enables data scientists and application developers to run their code in a distributed fashion. It also provides a lean and easy interface for distributed programming with many different libraries, best suited to perform machine learning and other intensive compute tasks. See [Ray on IBM Cloud Code Engine: Boost Your Serverless Compute](https://www.ibm.com/cloud/blog/ray-on-ibm-cloud-code-engine){: external}. |
| Iter8 | [Iter8](https://iter8.tools){: external} is the release engineering tool for Kubernetes that enables SLO validation, A/B testing, and progressive rollouts for Kubernetes applications. You can use Iter8 to validate your {{site.data.keyword.codeengineshort}} applications. See [Validating your application code and latency with Iter8](/docs/codeengine?topic=codeengine-slovalidationtut). |
{: caption="Table 2. Third-party integrations" caption-side="top"}


