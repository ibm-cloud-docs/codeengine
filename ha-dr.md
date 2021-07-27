---

copyright:
  years: 2021
lastupdated: "2021-07-21"

keywords: HA for Code Engine, DR for Code Engine, high availability for Code Engine, disaster recovery for Code Engine, failover for Code Engine, backing up code engine, availability of code engine, code engine regions, backing up your Code Engine instance

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
{:terraform: .ph data-hd-interface='terraform'}
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


# Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}
{: #ha-dr}

All {{site.data.keyword.cloud_notm}} general availability (GA) offerings have a Service Level Agreement of 99.99% availability. {{site.data.keyword.codeenginefull}} is a GA service that is offered in several locations. Each location has three different data centers for redundancy.
{: shortdesc}

For more information about high availability and disaster recovery standards in {{site.data.keyword.Bluemix_notm}}, see [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime). You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas).  

## {{site.data.keyword.codeengineshort}} regions
{: #ha-dr-regions}

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.codeengineshort}} service is available.

| Geography | Region | High availability |
|-------|-------|-------|
| Asia Pacific | Osaka (`jp-osa`) | MZR |
| Asia Pacific | Tokyo (`jp-tok`) | MZR |
| Europe | Frankfurt (`eu-de`) | MZR | 
| Europe | London (`eu-gb`) | MZR | 
| North America | Dallas (`us-south`) | MZR |
| North America | Toronto (`ca-tor`) | MZR |
{: caption="Table 1. Highly available {{site.data.keyword.codeengineshort}} regions" caption-side="top"}

A geography is a geographic area or larger political body that contains one or more regions. A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region. Each [multizone region (MZR)](/docs/overview?topic=overview-locations#mzr-table) is composed of 3 or more zones that are independent from each other to ensure that single failure events affect only a single zone.


## Availability of {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-availability}

When you provision a {{site.data.keyword.codeengineshort}} project, you select the location (MZR) where the instance is created. The region determines where your workloads, such as apps and jobs, are hosted. By default, your workload is deployed within a zone. If a failure of the hosting zone occurs, the workload is automatically re-created in one of the remaining zones. 

For more information about deploying apps across multiple regions with a custom domain name, see [Deploying an application across multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

 
## Disaster Recovery for {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-disaster}

In a major regional disaster, such as an earthquake, flood, or tornado, an entire region might be impacted. To ensure that your workloads are resilient to such events, deploy your workloads across multiple MZRs and implement an automatic failover mechanism by leveraging an Edge Proxy service. For example, you can use the service that is provided by [{{site.data.keyword.cis_full}}](/docs/cis?topic=cis-getting-started). For more information about deploying an application across multiple regions, see [Deploying an application across multiple regions with a custom domain name](/docs/codeengine?topic=codeengine-deploy-multiple-regions).
  
## Backing up your {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-backup}

{{site.data.keyword.cloud_notm}} performs a system backup of service instances metadata and stores this backup data in a cross-regional storage instance.

| {{site.data.keyword.codeengineshort}} region  | Cross-regional endpoint |
|-------|-------|
| `ca-tor` | `CA` |
| `eu-de` | `EU` |
| `eu-gb` | `EU` |
| `jp-osa` | `AP` |
| `jp-tok` | `AP` |
| `us-south` | `US` |
{: caption="Table 2. Cross-regional endpoints" caption-side="top"}
 
In order to avoid impacts on your workloads, such as duplication of jobs or deploying unwanted application instances, {{site.data.keyword.codeengineshort}} does not restore your workloads directly. Instead, restoring your workloads is you (the customer's) responsibility. For more information, see [Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce).
