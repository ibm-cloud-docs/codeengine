---

copyright:
  years: 2022
lastupdated: "2022-02-10"

keywords: HA for Code Engine, DR for Code Engine, high availability for Code Engine, disaster recovery for Code Engine, failover for Code Engine, backing up code engine, availability of code engine, code engine regions, backing up your Code Engine instance

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

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
| Asia Pacific | Australia (`au-syd`) | MZR |
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
| `au-syd` | `AP` |
| `ca-tor` | `CA` |
| `eu-de` | `EU` |
| `eu-gb` | `EU` |
| `jp-osa` | `AP` |
| `jp-tok` | `AP` |
| `us-south` | `US` |
{: caption="Table 2. Cross-regional endpoints" caption-side="top"}

To avoid impacts on your workloads, such as duplication of jobs or deploying unwanted application instances, {{site.data.keyword.codeengineshort}} does not restore your workloads directly. Instead, restoring your workloads is you (the customer's) responsibility. For more information, see [Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce).


