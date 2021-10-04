---

copyright:
  years: 2021
lastupdated: "2021-10-01"

subcollection: codeengine

keywords: code engine, responsibilities, compliance, management, app, data, job, disaster recovery

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}
{: #responsibilities-ce}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.codeenginefull_notm}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.codeenginefull_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

If you use other {{site.data.keyword.cloud_notm}} products such as {{site.data.keyword.cos_short}}, responsibilities that are marked as yours in the following table, such as disaster recovery for Data, might be IBM's or shared. Consult those products' documentation for your responsibilities.
{: note}

## Tasks for shared responsibilities by area
{: #task-responsibilities}

See what tasks you and IBM share responsibility for each area and resource when you use {{site.data.keyword.codeengineshort}}.
{: shortdesc}

In the following tables, {{site.data.keyword.codeengineshort}} entities include apps, jobs, and builds, as well as any other workload configuration artifacts.
{: note}

### Incident and operations management
{: #incident-and-ops}

You and IBM share responsibilities for the set-up and maintenance of your {{site.data.keyword.codeengineshort}} environment for your {{site.data.keyword.codeengineshort}} projects and entities. You are responsible for incident and operations management of your workloads and data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| {{site.data.keyword.codeengineshort}} projects and entities | - Deploy a fully managed, highly available platform in a secured, IBM-owned account to host projects. \n - Fulfill requests for more infrastructure, such as adding, reloading, updating, and removing worker nodes. \n - Fulfill automation requests to help recover projects. |- Use the provided CLI or console tools to adjust the runtime options (including scaling characteristics) of your workload. |
| Observability | - Provide {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} to enable observability of your {{site.data.keyword.codeengineshort}} projects and entities. \n - Provide integration with {{site.data.keyword.at_short}} and send {{site.data.keyword.codeengineshort}} events for auditability. | - Set up and monitor the health of your {{site.data.keyword.codeengineshort}} projects and entities. \n - Set up and send logs to [{{site.data.keyword.at_short}}](/docs/codeengine?topic=codeengine-at_events).|
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 2. Responsibilities for incident and operations management" caption-side="top"}

### Change management
{: #change-management}

You and IBM share responsibilities for keeping your images at the latest container platform and operating system versions, along with recovering infrastructure resources that might require changes. You are responsible for change management of your application data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| {{site.data.keyword.codeengineshort}} projects and entities | - Provide infrastructure operating system (OS), version, and security updates. | - Use the CLI or console tools to apply any app or job required updates. |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 3. Responsibilities for change management" caption-side="top"}

### Identity and access management
{: #iam-responsibilities}

You and IBM share responsibilities for controlling access to your {{site.data.keyword.codeengineshort}} projects. For {{site.data.keyword.iamlong}} responsibilities, consult that product's documentation. You are responsible for identity and access management to your application data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | - Create projects with a service ID so that your deployments in the project can pull images from {{site.data.keyword.registrylong_notm}}. | - Maintain responsibility for any service roles that you create. |
| Observability | - Provide integration of {{site.data.keyword.at_full_notm}} with your  {{site.data.keyword.codeengineshort}} project entities to audit any activity. | - Set up {{site.data.keyword.at_full_notm}} or other capabilities to track user activity. |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 4. Responsibilities for identity and access management" caption-side="top"}


### Security and regulation compliance
{: #security-compliance}

IBM is responsible for the security and compliance of {{site.data.keyword.codeengineshort}}. You are responsible for the security and compliance of any {{site.data.keyword.codeengineshort}} entities that run in the {{site.data.keyword.codeengineshort}} environment and your associated data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | - Maintain controls commensurate to various industry compliance standards. \n - Monitor, isolate, and recover user projects. \n - Provide highly available replicas of your projects and entities. \n - Monitor and report the health of the project and entities in the various interfaces. \n - Automatically apply security patch updates for infrastructure. \n - Enable certain security settings, such as encrypted disks. \n - Disable certain insecure actions, such as not permitting users to SSH into the host. \n - Encrypt communication with TLS. \n - Continuously monitor {{site.data.keyword.codeengineshort}} projects and entities to detect vulnerability and security compliance issues. \n - Provide options for network connectivity. \n - Integrate {{site.data.keyword.codeengineshort}} with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). | - Set up and maintain security and regulation compliance for your {{site.data.keyword.codeengineshort}} entities and data. \n - As part of your incident and operations management responsibilities for {{site.data.keyword.codeengineshort}} entities and data, apply any security updates. \n -  Do not include sensitive or private information in {{site.data.keyword.codeengineshort}} resource metadata, including configuration values. |
| Building from source | - Continuously update the build tools, including BuildKit, and Paketo buildpacks to the latest version. | - Resubmit builds to pick up fixes in the base image of your Dockerfile-based builds and to pick up operating system and runtime environment fixes in your Buildpacks-based builds. |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 5. Responsibilities for security and regulation compliance" caption-side="top"}


### Disaster recovery
{: #disaster-recovery}

IBM is responsible for the recovery of {{site.data.keyword.codeengineshort}} projects and entities in case of disaster. You are responsible for the recovery of the workloads and your workload data. If you integrate with other {{site.data.keyword.cloud_notm}} services such as file, block, object, cloud database, logging, or audit event services, consult those services' disaster recovery information.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | - Maintain service availability across [worldwide regions](/docs/codeengine?topic=codeengine-regions) so that customers can deploy projects across zones and regions for higher DR tolerance. \n - Provision projects with three replicas in the same region for high availability. \n - Continuously monitor {{site.data.keyword.codeengineshort}} infrastructure to ensure the reliability and availability of the service environment by site reliability engineers. \n - Update and recover operational {{site.data.keyword.codeengineshort}} entities. \n - Back up and recover {{site.data.keyword.codeengineshort}} infrastructure data, as well as your {{site.data.keyword.codeengineshort}} entity configuration files. \n - Provide integration with other {{site.data.keyword.cloud_notm}} services such as storage providers so that data can be backed up and restored. | - Set up and maintain disaster recovery capabilities for your {{site.data.keyword.codeengineshort}} entities and data. For example, to prepare your project for HA/DR scenarios, follow the guidance in [High availability for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-ha-dr). Note that persistent storage of data such as logs and metrics is not set up by default.  |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 6. Responsibilities for disaster recovery" caption-side="top"}

