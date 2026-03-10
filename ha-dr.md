---

copyright:
  years: 2026
lastupdated: "2026-03-09"

keywords: HA for Code Engine, DR for Code Engine, high availability for Code Engine, disaster recovery for Code Engine, failover for Code Engine, backing up code engine, availability of code engine, code engine regions, backing up your Code Engine instance

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}
{: #ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible despite unexpected failures. [Disaster recovery](#x2113280){: term} is the process of restoring service operations after a major disruption.
{: shortdesc}

{{site.data.keyword.codeengineshort}} is a highly available regional service designed to maintain availability during zonal outages. {{site.data.keyword.codeengineshort}} meets the [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo) with the Standard plan.

For more information about high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}, see [How IBM Cloud ensures high availability and redundancy](/docs/resiliency?topic=resiliency-ha-redundancy). You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas).

## Availability of {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-availability}

{{site.data.keyword.codeenginefull}} is offered in multiple locations (regions). Each region contains three data centers (zones) for redundancy.

When you provision a {{site.data.keyword.codeengineshort}} project, you select the location (MZR) where the instance is created. The region determines where your workloads - such as apps, jobs, functions, and fleets - are hosted.

By default, your workload is deployed within a single zone. If the hosting zone fails, the workload is automatically re-created in one of the remaining zones.

The service performs controlled workload moves between zones during normal operations, such as service maintenance and software upgrades. These rollout restarts are performed gracefully to minimize disruption.
Unplanned failovers may occur during unexpected events in the operating environment.

{{site.data.keyword.codeengineshort}} stores metadata (including your project, app, function, job, fleet, and image build definitions) and replicates it across all zones within a region for availability.
As a compute-only service, {{site.data.keyword.codeengineshort}} is not responsible for ensuring high availability of your workload data or container images. Consult the documentation of the respective cloud services for guidance on ensuring high availability.
For container image availability, follow the guidance in [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-ha-dr) to ensure your workload remains operational during a zonal outage. If you read or store data in {{site.data.keyword.cos_full_notm}} or any other {{site.data.keyword.cloud_notm}} database or storage service, refer to each service's documentation for high availability features.

![{{site.data.keyword.codeengineshort}} regional topology](images/ha_diagram_ce.svg "{{site.data.keyword.codeengineshort}} regional topology"){: caption="{{site.data.keyword.codeengineshort}} regional topology" caption-side="bottom"}

## {{site.data.keyword.codeengineshort}} regions
{: #ha-dr-regions}

The following table lists the regions where {{site.data.keyword.codeengineshort}} is available and their high-availability status.

| Geography | Region | High availability |
|-------|-------|-------|
| Asia Pacific | Australia (`au-syd`) | MZR |
| Asia Pacific | Osaka (`jp-osa`) | MZR |
| Asia Pacific | Tokyo (`jp-tok`) | MZR |
| Europe | Frankfurt (`eu-de`) | MZR |
| Europe | Madrid (`eu-es`) | MZR | 
| Europe | London (`eu-gb`) | MZR | 
| North America | Dallas (`us-south`) | MZR |
| North America | Toronto (`ca-tor`) | MZR |
| North America | Washington (`us-east`) | MZR |
| South America | Brazil Sao Paulo (`br-sao`) | MZR |
{: caption="Highly available {{site.data.keyword.codeengineshort}} regions" caption-side="bottom"}

A geography is a geographic area that contains one or more regions. Each region contains [multiple availability zones](https://www.ibm.com/solutions/cloud-data-centers) to meet local access, low latency, and security requirements. Each [multizone region (MZR)](/docs/overview?topic=overview-locations#table-mzr) consists of 3 or more independent zones, ensuring that single failure events impact only one zone.

## Disaster Recovery for {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-disaster}

In a major regional disaster - such as an earthquake, flood, or severe weather event - an entire region may be impacted. To ensure your workloads are resilient to such events, deploy them across multiple MZRs and implement an automatic failover mechanism using an Edge Proxy service. For example, you can use [{{site.data.keyword.cis_full}}](/docs/cis?topic=cis-getting-started). For more information about deploying an application across multiple regions, see [Deploying an application across multiple regions with a custom domain name](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

![{{site.data.keyword.codeengineshort}} global topology](images/dr_diagram_ce.svg "{{site.data.keyword.codeengineshort}} global topology"){: caption="{{site.data.keyword.codeengineshort}} global topology" caption-side="bottom"}

### How IBM helps ensure disaster recovery
{: #ha-dr-ibm-how}

#### Backing up your {{site.data.keyword.codeengineshort}} instances
{: #ha-dr-backup}

{{site.data.keyword.cloud_notm}} automatically backs up {{site.data.keyword.codeengineshort}} project metadata and stores it in cross-regional storage for disaster recovery purposes.

| {{site.data.keyword.codeengineshort}} region  | Cross-regional endpoint |
|-------|-------|
| `au-syd` | `AP` |
| `br-sao` | `BR` |
| `ca-tor` | `CA` |
| `eu-de` | `EU` |
| `eu-es` | `EU` |
| `eu-gb` | `EU` |
| `jp-osa` | `AP` |
| `jp-tok` | `AP` |
| `us-east` | `US` |
| `us-south` | `US` |
{: caption="Cross-regional endpoints" caption-side="bottom"}

To avoid unintended impacts on your workloads - such as job duplication or deploying unwanted application instances - {{site.data.keyword.codeengineshort}} does not automatically restore your workloads. Restoring your workloads is your responsibility. For more information, see [Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce).

#### Recovery Time Objective (RTO) and Recovery Point Objective (RPO)
{: #ha-dr-rto-rpo}

* The **Recovery Time Objective** (RTO) is the maximum acceptable time a system, application, or business process can be offline before causing significant business impact.

* The **Recovery Point Objective** (RPO) defines the maximum acceptable amount of data loss (measured in time) after an HA or DR event.

IBM conducts regular HA/DR tests that include HA failover, isolated DR scenarios (excluding customer-owned data and workload definitions), data restoration, and simulation of non-technical parameters.

During these tests, RTO (recovery time) and RPO (recovery point) objectives are measured and verified.

| Objective  | Target |
|-------|-------|
| Automatic failover during zonal outage | RTO = seconds , RPO = 0 |
| Disaster Recovery excluding recovery of customer-owned artefacts| RTO = hours , RPO = 1 day |
{: caption="RTO/RPO targets" caption-side="bottom"}

### Planning for disaster recovery
{: #ha-dr-planning}

In addition to IBM's HA/DR testing, you must practice your disaster recovery procedures regularly. As you build your plan, consider the following failure scenarios and resolutions.

| Event                           | Resolution                                |
|---------------------------------|-------------------------------------------|
| Hardware failure (compute infrastructure) | IBM provides infrastructure that is resilient to single-point hardware failures within a zone - no configuration required. |
| Zone failure | Automatic failover (see [Availability of {{site.data.keyword.codeengineshort}} instances](#ha-dr-availability)). The workload is automatically moved to an available zone. |
| Data corruption | You are responsible for creating backups of your data. |
| Regional failure | No automatic failover. As described in [Disaster Recovery for {{site.data.keyword.codeengineshort}} instances](#ha-dr-disaster), you should deploy your workload in a second multi-zone region. |
| Workload availability | You are responsible for implementing your business applications to recover state from external storage or databases. |
| HA/DR resiliency | You are responsible for ensuring trained staff is available to manage your components and restore your workloads and customer-owned data during an outage. |
{: caption="HA/DR events and resolution" caption-side="bottom"}

#### Your responsibilities for HA and DR
{: #ha-dr-responsibilities}

Use the following checklists associated with each feature to help you create and practice your plan.

* **Container images** used for {{site.data.keyword.codeenginefull}} apps, jobs, and fleets

  Verify that your container images are available in your {{site.data.keyword.registrylong_notm}} backup region.

* **Code bundles** used for {{site.data.keyword.codeenginefull}} functions

  Verify that your code bundles are available in your {{site.data.keyword.registrylong_notm}} backup region.

A comprehensive High Availability (HA) and Disaster Recovery (DR) test plan includes defining your RTO and RPO targets, identifying critical systems, and validating backup integrity, network failover, and data synchronization. Key steps involve simulating failures (such as node failure or site outage), executing failover procedures, verifying system functionality, and documenting the fallback process.

* **Test preparation**

  * **Define objectives**: Confirm your Recovery Time Objective (RTO) and Recovery Point Objective (RPO).
  * **Identify critical systems**: List all systems, data, and applications that require failover.
  * **Establish team roles**: Define responsibilities for the DR team and assign a key contact person.
  * **Backup verification**: Confirm that backups are valid and accessible.
  * **Environment isolation**: Isolate test systems to prevent accidental impact on production environments.

* **Test execution**

  * **Simulate failure scenario**: Initiate a planned failure, such as cutting network connectivity, stopping a service, or shutting down a primary server.
  * **Failover execution**: Execute the documented failover procedure to the secondary/DR site.
  * **Verify data integrity**: Use checksums or hash values to ensure data is not corrupted.
  * **Application validation**: Test the functionality of applications on the DR site.
  * **DNS/Traffic rerouting**: Validate that user traffic is redirected to the new active node.

* **Post-test and documentation**

  * **Perform failback**: Gracefully bring the primary site back online and re-synchronize data.
  * **Document results**: Record timings, successes, and any deviations from the plan.
  * **Identify gaps**: Identify deficiencies in the plan and update procedures accordingly.
  * **Communication audit**: Verify that notifications were sent to all stakeholders.

* **Common test scenarios**

  * **HA test**: Local failover to a standby node (for example, within the same data center).
  * **DR test**: Full failover to a geographically separate location.
  * **Data restoration**: Complete restoration of customer-owned data and workload artifacts from a backup datastore to the primary or selected backup location.
  * **Staff availability**: Test the operational impact if key personnel are unavailable or unable to connect to your systems.
	
