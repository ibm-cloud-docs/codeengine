---

copyright:
  years: 2021
lastupdated: "2021-09-10"

keywords: code engine, architecture, workload isolation, isolation, workload

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


# Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation 
{: #architecture}

{{site.data.keyword.codeenginefull}} is the {{site.data.keyword.cloud_notm}} platform that unifies container images, 12-factor-apps, functions, and batch jobs as a one-stop-shop. It's a multi-tenant system that consists of three major building blocks: A control plane, a (set of) shard (or shards), and a routing layer. The control plane and the shards are realized as separate multi-zone Kubernetes clusters. The following diagram gives a graphical overview of the architecture.

![Code Engine architecture diagram.](images/codeengine-architecture.svg "Code Engine architecture diagram"){: caption="Figure 1. Code Engine architecture diagram" caption-side="bottom"}

{{site.data.keyword.codeengineshort}} is based on {{site.data.keyword.containerlong_notm}} clusters and depends on the components and workload isolation of the {{site.data.keyword.containerlong_notm}}. For more information, see [{{site.data.keyword.containerlong_notm}} VPC cluster architecture](/docs/containers?topic=containers-service-arch#architecture_vpc).

All components are managed and owned by IBM and run in the {{site.data.keyword.cloud_notm}} account. Each cluster is running in its own VPC and separated from other clusters.

The {{site.data.keyword.codeengineshort}} control plane runs the components that are shared among all {{site.data.keyword.codeengineshort}} users and make the Kubernetes cluster a true multi-tenant system. The control-plane consists of four microservices that are deployed on it.

| Component | Purpose |
| ---- | ------------------- |
| Resource broker |    Creates and deletes {{site.data.keyword.codeengineshort}} project resources in the {{site.data.keyword.cloud_notm}} resource controller and requests the placement of the project on a shard. |
| Project placement controller | Selects a shard and requests the creation, deletion, and isolation of the project on the shard. |
| API server |    Provides the target information (`KUBECONFIG` file) for the selected project. It also performs IAM access policy checks and writes audit records. |
| `Kube API proxy` | Proxies each API request to the proper shard cluster, perform IAM policy checks, and writes audit records. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} control-plane microservices" caption-side="bottom"}

The shards are running the customer workload, such as builds, batch jobs, or apps. Therefore, the shard cluster runs the following microservices to control the customer workloads.

| Component | Purpose |
| ---- | ------------------- |
| Project isolation controller | Manages and isolates the Kubernetes namespace corresponding to the {{site.data.keyword.codeengineshort}} project resource. It monitors and ensures the isolation aspects like role-based-access-control (RBAC), pod security policies, resource quota, and network policies are enforced.  |
| Project domain and cert controller |  Manages the domain and certificates for the route endpoint of the project. The endpoint consists of a DNS entry and a wildcard certificate. |
| Knative and Istio |  Manage the lifecycle of applications. Knative is responsible for scaling the application. Istio is responsible for routing the traffic to the proper revision and container of the application. |
| Batch controller | Manages the lifecycle and containers for jobs and job runs.  |
| Build controller |  Manages the lifecycle and containers for builds and build runs. |
| Service binding and {{site.data.keyword.cloud_notm}} operator | Manage the lifecycle of secrets that are associated to bindings of {{site.data.keyword.cloud_notm}} services to applications and jobs. |
| {{site.data.keyword.cos_full_notm}} event source controller | Manage the lifecycle of event subscriptions from the {{site.data.keyword.cos_full_notm}} service. |
| Cluster node autoscaler | Scales the shard by adding and removing worker nodes based on capacity demand.  |
| {{site.data.keyword.mon_full_notm}} | Sends service metrics to {{site.data.keyword.mon_full_notm}}. For more information about these metrics, see [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor).|
| {{site.data.keyword.la_full}} | Forward platform logs and metrics to {{site.data.keyword.la_full_notm}}. For more information, see [Auditing events for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-at_events). |
{: caption="Table 2. Shard cluster microservices" caption-side="bottom"}

## {{site.data.keyword.codeengineshort}} workload isolation
{: #workload-isolation}

{{site.data.keyword.codeengineshort}} is a multi-tenant, regional service that supports the following workload isolation characteristics.

- {{site.data.keyword.codeengineshort}} project resources are isolated within a secured Kubernetes environment that is running in an {{site.data.keyword.cloud_notm}} multi-zone region.
- {{site.data.keyword.codeengineshort}} projects and its containing resources, such as application, builds, and jobs that run on shared clusters that use shared management components.
- To isolate the access to project resources, {{site.data.keyword.codeengineshort}} performs several levels of authentication and authorization checks within the `apiserver` and `kube-api-proxy` components (see previous table),
    - IAM authentication and access policies checks are performed on a project level.
    - In order to manage multi-tenant access to the underlying Kubernetes API, direct access to the API server is not allowed. Instead, use the {{site.data.keyword.codeengineshort}} custom `Kube-api-proxy` API for access.
    - Role-based access control checks are performed on a resource level to allow only authorized users to perform certain operations on project resources. 
- The authorization is controlled by the customer by assigning `manager`, `reader`, or `writer` roles to users for a {{site.data.keyword.codeengineshort}} project resource within IAM.
- To isolate customer workload, {{site.data.keyword.codeengineshort}} enforces the following concepts,
    - Container isolation through various Linux isolation techniques. These techniques ensure multiple layers of security to prevent the privilege escalation of containers and to restrict containers to use a limited set of system privileges.
    - Resource quota and `LimitRange` to prevent excessive resource consumption.
    - Network policies to prevent access to other customer containers.
- Shared multi-tenant components are secured, for example, by disabling reverse lookup in `KubeDNS`.
- To limit the blast radius, each shard cluster is running in its own VPC, which is isolated from other shard VPCs.


