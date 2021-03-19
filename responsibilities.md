---

copyright:
  years: 2021
lastupdated: "2021-03-19"

subcollection: codeengine

keywords: code engine, responsibilities, compliance, management, app, data, job, disaster recovery

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


# Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}
{: #responsibilities-ce}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.codeenginefull_notm}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

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
| {{site.data.keyword.codeengineshort}} projects and entities | <ul><li>Deploy a fully managed, highly available platform in a secured, IBM-owned account to host projects.</li><li>Fulfill requests for more infrastructure, such as adding, reloading, updating, and removing worker nodes.</li><li>Fulfill automation requests to help recover projects.</li></ul> |<ul><li>Use the provided CLI or console tools to adjust the runtime options (including scaling characteristics) of your workload.</li></ul> |
| Observability | <ul><li>Provide {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} to enable observability of your {{site.data.keyword.codeengineshort}} projects and entities.</li><li>Provide integration with {{site.data.keyword.at_short}} and send {{site.data.keyword.codeengineshort}} events for auditability.</li></ul> | <ul><li>Set up and monitor the health of your {{site.data.keyword.codeengineshort}} projects and entities.</li><li>Set up and send logs to [{{site.data.keyword.at_short}}](/docs/codeengine?topic=codeengine-at_events).</li></ul>|
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 2. Responsibilities for incident and operations management" caption-side="top"}

<br />

### Change management
{: #change-management}

You and IBM share responsibilities for keeping your images at the latest container platform and operating system versions, along with recovering infrastructure resources that might require changes. You are responsible for change management of your application data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| {{site.data.keyword.codeengineshort}} projects and entities | <ul><li>Provide infrastructure operating system (OS), version, and security updates.</li></ul> | <ul><li>Use the CLI or console tools to apply any app or job required updates.</li></ul> |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 3. Responsibilities for change management" caption-side="top"}

<br />

### Identity and access management
{: #iam-responsibilities}

You and IBM share responsibilities for controlling access to your {{site.data.keyword.codeengineshort}} projects. For {{site.data.keyword.iamlong}} responsibilities, consult that product's documentation. You are responsible for identity and access management to your application data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | <ul><li>Create projects with a service ID so that your deployments in the project can pull images from {{site.data.keyword.registrylong_notm}}.</li></ul> | <ul><li>Maintain responsibility for any service roles that you create.</li></ul> |
| Observability | <ul><li>Provide integration of {{site.data.keyword.at_full_notm}} with your  {{site.data.keyword.codeengineshort}} project entities to audit any activity.</li></ul> | <ul><li>Set up {{site.data.keyword.at_full_notm}} or other capabilities to track user activity.</li></ul> |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 4. Responsibilities for identity and access management" caption-side="top"}

<br />

### Security and regulation compliance
{: #security-compliance}

IBM is responsible for the security and compliance of {{site.data.keyword.codeengineshort}}. You are responsible for the security and compliance of any {{site.data.keyword.codeengineshort}} entities that run in the {{site.data.keyword.codeengineshort}} environment and your associated data.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | <ul><li>Maintain controls commensurate to various industry compliance standards.</li><li>Monitor, isolate, and recover user projects.</li><li>Provide highly available replicas of your projects and entities.</li><li>Monitor and report the health of the project and entities in the various interfaces.</li><li>Automatically apply security patch updates for infrastructure.</li><li>Enable certain security settings, such as encrypted disks.</li><li>Disable certain insecure actions, such as not permitting users to SSH into the host.</li><li>Encrypt communication with TLS.</li><li>Continuously monitor {{site.data.keyword.codeengineshort}} projects and entities to detect vulnerability and security compliance issues.</li><li>Provide options for network connectivity.<li>Integrate {{site.data.keyword.codeengineshort}} with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).</li></li></ul> | <ul><li>Set up and maintain security and regulation compliance for your {{site.data.keyword.codeengineshort}} entities and data.</li><li>As part of your incident and operations management responsibilities for {{site.data.keyword.codeengineshort}} entities and data, apply any security updates.</li></ul>  |
| Building from source | <ul><li>Continuously update the build tools, including Kaniko, and Paketo buildpacks to the latest version.</li></ul> | <ul><li>Resubmit builds to pick up fixes in the base image of your Dockerfile-based builds and to pick up operating system and runtime environment fixes in your Buildpacks-based builds.</li></ul> |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 5. Responsibilities for security and regulation compliance" caption-side="top"}

<br />

### Disaster recovery
{: #disaster-recovery}

IBM is responsible for the recovery of {{site.data.keyword.codeengineshort}} projects and entities in case of disaster. You are responsible for the recovery of the workloads and your workload data. If you integrate with other {{site.data.keyword.cloud_notm}} services such as file, block, object, cloud database, logging, or audit event services, consult those services' disaster recovery information.
{: shortdesc}

| Task | IBM responsibilities | Your responsibilities |
| ------ | ----------------------- | ---------------------- |
| General | <ul><li>Maintain service availability across [worldwide regions](/docs/codeengine?topic=codeengine-regions) so that customers can deploy projects across zones and regions for higher DR tolerance.</li><li>Provision projects with three replicas in the same region for high availability.</li><li>Continuously monitor {{site.data.keyword.codeengineshort}} infrastructure to ensure the reliability and availability of the service environment by site reliability engineers.</li><li>Update and recover operational {{site.data.keyword.codeengineshort}} entities.</li><li>Back up and recover {{site.data.keyword.codeengineshort}} infrastructure data, as well as your {{site.data.keyword.codeengineshort}} entity configuration files.</li><li>Provide integration with other {{site.data.keyword.cloud_notm}} services such as storage providers so that data can be backed up and restored.</li></ul> | <ul><li>Set up and maintain disaster recovery capabilities for your {{site.data.keyword.codeengineshort}} entities and data. Note that persistent storage of data such as logs and metrics are not set up by default.</li></ul>  |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 6. Responsibilities for disaster recovery" caption-side="top"}
