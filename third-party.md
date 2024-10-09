---

copyright:
  years: 2024
lastupdated: "2024-10-09"

keywords: third party, ibm cloud integrations, integrations, code engine, third-party

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

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
| {{site.data.keyword.la_full_notm}} | Add log management capabilities to your project by creating a {{site.data.keyword.la_short}} instance. For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-logging). |
| {{site.data.keyword.registrylong_notm}} | Set up your own container registry to safely store and share images. For more information, see [Getting started with {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started). |
| {{site.data.keyword.cos_full_notm}} | Subscribe to Object storage event producers from your application or job. For more information, see [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer). |
| {{site.data.keyword.messagehub_full}} | Subscribe to Kafka and {{site.data.keyword.messagehub}} event producers from your application or job. For more information, see [Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer). |
|{{site.data.keyword.cloud_notm}} {{site.data.keyword.contdelivery_short}} | Automate your app and job builds by using a toolchain. For more information about the setup, see [Integrating {{site.data.keyword.codeengineshort}} workloads with {{site.data.keyword.contdelivery_short}}](/docs/codeengine?topic=codeengine-toolchain-ce). |
{: caption="Table 1. {{site.data.keyword.cloud_notm}} integrations" caption-side="bottom"}

## Third-party integrations
{: #supported-third-integrations}

{{site.data.keyword.codeengineshort}} is supported by the following third-party integrations. For issues in open source projects that are used by {{site.data.keyword.cloud_notm}}, see the [IBM open source and third-party policy](https://www.ibm.com/support/pages/node/737271){: external}.

| Integration | Description |
|-----------|------------------|
| Lithops | [Lithops](https://lithops-cloud.github.io/) is an open source framework that designed to massively scale your Python applications. See [Running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops). |
| Ray | [Ray](https://www.ray.io/){: external} is an open technology that enables data scientists and application developers to run their code in a distributed fashion. It also provides a lean and easy interface for distributed programming with many different libraries, best suited to perform machine learning and other intensive compute tasks. See [Ray on IBM Cloud Code Engine: Boost Your Serverless Compute](https://www.ibm.com/blog/ray-on-ibm-cloud-code-engine){: external}. |
| Iter8 | [Iter8](https://iter8.tools){: external} is the release engineering tool for Kubernetes that enables SLO validation, A/B testing, and progressive rollouts for Kubernetes applications. You can use Iter8 to validate your {{site.data.keyword.codeengineshort}} applications. See [Validating your application code and latency with Iter8](/docs/codeengine?topic=codeengine-slovalidationtut). |
| Guard | [Guard](https://pkg.go.dev/knative.dev/security-guard#section-readme){: external} is a workload runtime-security solution, well-equipped to protect Serverless Services. {{site.data.keyword.codeengineshort}} users may use Guard as a security layer to protect {{site.data.keyword.codeengineshort}} applications. See [Securing your application with Guard](/docs/codeengine?topic=codeengine-getting-started-with-guard). |
{: caption="Table 2. Third-party integrations" caption-side="bottom"}
