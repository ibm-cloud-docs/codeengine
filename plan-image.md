---

copyright:
  years: 2021
lastupdated: "2021-05-19"

keywords: planning for repositories in code engine, images in code engine, container registry in code engine, planning for registries in code engine, container images in code engine, image registries, container registry

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



# Planning image registries
{: #plan-image}

Images that are used by {{site.data.keyword.codeenginefull}} are typically stored in a registry that can either be accessible by the public (public registry) or set up with limited access for a small group of users (private registry).
{: shortdesc}

A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private.

You can access images from multiple types of registries.

| Registry | Description | Benefit |
|--------|-----------|-------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started)| With this option, you can set up your own secured image repository in {{site.data.keyword.registrylong_notm}} where you can safely store and share images between users.|<ul><li>Manage access to images in your account.</li><li>Use {{site.data.keyword.IBM_notm}} provided images and sample apps, such as {{site.data.keyword.IBM_notm}} Liberty, as a parent image and add your own app code to it.</li><li>Automatic scanning of images for potential vulnerabilities by Vulnerability Advisor, including OS-specific recommendations to fix them.</li></ul> |
|Any other private registry | Connect any existing private registry to {{site.data.keyword.codeengineshort}} by adding access. Adding access  securely saves your registry URL and credentials in a Kubernetes secret. | <ul><li>Use existing private registries independent of their source (Docker Hub, organization-owned registries, or other private Cloud registries).</li></ul> |
| [Public Docker Hub](https://hub.docker.com/){: external}{: #dockerhub}| Use this option to pull existing public images from Docker Hub directly in your {{site.data.keyword.codeengineshort}} applications or jobs. <p>**Important**</p> <ul><li>This option might not meet your organization's security requirements such as access management, vulnerability scanning, or app privacy.</li><li>When you pull an image from Docker Hub to use with apps or jobs in Code Engine, be aware of [Docker rate limits](https://docs.docker.com/docker-hub/download-rate-limit){: external} for free plan (anonymous) users. You might experience pull limits if you receive a `429` error indicating you have reached your pull rate limit. To [increase rate limits ](https://www.docker.com/increase-rate-limits){: external}, you can upgrade your account to a Docker `Pro` or `Team` subscription.</li></ul> | <ul><li>These images can be referred to directly when you create an app or job, no additional setup is required.</li><li>Includes various open source applications.</li></ul> |
{: caption="Public and private image registry options" caption-side="top"}

After you [set up access](/docs/codeengine?topic=codeengine-add-registry) to an image registry, you can deploy the images as applications or jobs in {{site.data.keyword.codeengineshort}}.


## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}: Container registry implementation
{: #private-registry-imp}

To pull images from a registry, {{site.data.keyword.codeengineshort}} uses a special type of Kubernetes secret that is called an `imagePullSecret`. This image pull secret stores the credentials to access a container registry. When you add access to a container registry with {{site.data.keyword.codeengineshort}}, you are creating an image pull secret. For more information about image pull secrets, see [Kubernetes documentation](https://kubernetes.io/docs/home/){: external}.
