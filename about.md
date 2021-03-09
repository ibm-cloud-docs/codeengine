---

copyright:
  years: 2021
lastupdated: "2021-03-08"

keywords: about code engine, benefits for code engine, terminology for code engine, developers for code engine, capabilities of code engine

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


# About {{site.data.keyword.codeengineshort}}
{: #about}

{{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}") was developed by IBM with the goal of helping you create modern, source-centric, containerized, and serverless apps and jobs. The platform is designed to address the needs of developers who just want their code to run. {{site.data.keyword.codeengineshort}} abstracts the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code. 
{: shortdesc}

## Benefits of {{site.data.keyword.codeengineshort}}
{: #benefits}
Review the capabilities that {{site.data.keyword.codeengineshort}} provides to run your workloads.

| Capability | Description |
| --------- | ------------------- |
| Runs your workloads | {{site.data.keyword.codeengineshort}} runs your HTTP-driven applications and your run-to-completion batch jobs.  |
| Fully managed service | {{site.data.keyword.codeengineshort}} takes care of all the cluster management, including provisioning, configuring, scaling, and managing servers so you do not need to worry about the underlying infrastructure.  |
| Builds your code | {{site.data.keyword.codeengineshort}} pulls your source code and creates the container image for you. {{site.data.keyword.codeengineshort}} supports both Dockerfile and Cloud Native Buildpack. |
| Private workloads | Store your source code in private repositories and push your images to private registries and {{site.data.keyword.codeengineshort}} can access them. |
| Fully integrated | {{site.data.keyword.codeengineshort}} is fully integrated into IBM Cloud so that you can take advantage of the full catalog of IBM Cloud services. |
| Event-driven workloads | Extend the functionality of your applications with messages (events) from event producers. Your application can then react to those events and perform actions based on them. |
| Auto-scales - even to zero | {{site.data.keyword.codeengineshort}} automatically scales your workloads up and down, and even down to zero when no requests are active. You pay for only the resources that you consume. |
| Control access | Assign platform and services access permissions to your projects in IBM Cloud Identity and Access Management to control who can provision and manage resources in your IBM Cloud account. |
| Based on open source | {{site.data.keyword.codeengineshort}} is built on a set of open source technologies such as Kubernetes, Knative, Istio, and Tekton, keeping your apps and jobs portable. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} benefits" caption-side="bottom"}

## {{site.data.keyword.codeengineshort}} terminology
{: #terminology}

Learn the basics about {{site.data.keyword.codeengineshort}} by reviewing the following key terms. Afterward, you can test your knowledge and [take a quiz!](https://ibm.biz/BdfFxR){: external}
  
| Term | Description |
| --------- | ------------------- |
| Application | An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeengineshort}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app.  |
| Build | A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpacks. |
| Code repository | A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build. |
| Configmap | A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app or job portable. A configmap contains information in key-value pairs. |
| Container image registry | A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private. With {{site.data.keyword.codeengineshort}}, you can add access to your private container image registries. |
| Job | A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. |
| Project | A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. A project provides the following items:<ul><li>Provides a unique namespace for entity names.</li><li> Manages access to project resources (inbound access).</li><li> Manages access to backing services, registries, and repositories (outbound access).</li><li> Has an automatically generated certificate for Transport Layer Service (TLS).</li></ul> |
| Secret | A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs. |
| Service binding | Service bindings provide applications and jobs access to {{site.data.keyword.cloud_notm}} services. |
| Subscription | A subscription provides a way of signing up to receive events from a particular event producer. For more information about the different types of event producers and how to subscribe to them, see [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events). |
{: caption="Table 2. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}
