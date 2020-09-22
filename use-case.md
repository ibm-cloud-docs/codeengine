---

copyright:
  years: 2020
lastupdated: "2020-09-22"

keywords: code engine, use case

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# {{site.data.keyword.codeenginefull_notm}} service use cases
{: #use-cases}

Is the {{site.data.keyword.codeenginefull_notm}} service right for you? Read the following use cases.
{: shortdesc}

## Experienced with containers, but no skill or budget for managing clusters
{: #use-cases-containers}

Maria is a developer who is knowledgeable about containers. However, they don't want the complexity or time consumption of managing a cluster. With {{site.data.keyword.codeengineshort}}, they does not need to worry about the skills that are required to manage a cluster or the time it takes to do so. Instead, {{site.data.keyword.codeengineshort}} takes these complexities away and the IBM team manages your infrastructure as part of the IBM Cloud service. 

## Workloads with intermittent spikes
{: #use-cases-small-workloads}

Alexander has a website that is busy on the weekends, but experiences less traffic during the week. Because this website experiences these bursts of activity followed by periods of inactivity, {{site.data.keyword.codeengineshort}} is a good solution. With {{site.data.keyword.codeengineshort}}, Alexander's website application automatically scales up the application instances for the increase in traffic, and then back down again for the periods of inactivity (even down to zero). With a dedicated cluster, Alexander must first size the Kubernetes cluster for the workload spikes and then pay for it, even when it’s not being fully leveraged. 

## Batch workloads integrated with storage
{: #use-cases-batch-workloads}

Arpana has a batch job that processes employee salaries at the end of every month. Because this job runs monthly, it is idle most of the time, but consumes a high amount of CPU and memory when it runs. The batch job needs to integrate with storage in order to store the results. By using {{site.data.keyword.codeengineshort}}, Arpana can integrate the batch job with {{site.data.keyword.cos_full_notm}} and is charged only for the resources that the job uses when it is running. When the job is idle, it isn't consuming any resources and therefore she is not charged. However, the job might incur costs with the {{site.data.keyword.cos_full_notm}} instance.

## Bring your workload
{: #use-cases-bring-your-workloads}

Part of Tache's job is to create images and deploy them. They are experienced with creating container images and with deploying them but would like to simplify this process so that they can concentrate on other tasks. With {{site.data.keyword.codeengineshort}}, Tache is able to build images and deploy them, directly from the same interface, thus simplifying daily tasks and freeing up time to develop more code.

## Testing, proof-of-concepts, or "tire kicking”
{: #use-cases-testing}

Enrico is interested in learning more about container-based architecture. He developed an application, but wants to test it out before presenting it to the managers. This application is small, so they do not want to pay for a small, dedicated cluster. In this case, {{site.data.keyword.codeengineshort}} is the perfect choice, allowing Enrico to test the application and to provide a proof-of-concept of the design to the managers without the cost that a dedicated cluster might require.

