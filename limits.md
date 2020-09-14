---

copyright:
  years: 2020
lastupdated: "2020-09-14"

keywords: code engine

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


# Limits and quotas for {{site.data.keyword.codeengineshort}}
{: #limits}

The following sections provide technical details about the {{site.data.keyword.codeengineshort}} limit settings.
{: shortdesc}

## Beta release limitations
{: #beta-limits}

During the Beta release of {{site.data.keyword.codeenginefull_notm}}, be aware of the following limitations.

- One project per location
- After 7 days, your project and everything that the project contains will be deleted.

Experimental releases are not intended for production and any projects, apps, or jobs that you create during Experimental will not carry over to other releases.

## Project quotas
{: #kn-project_quotas}

The following table lists the limits for applications.

| Category  |   Description      | 
| --------- | -----------        | 
| `requests.cpu` | The sum of CPU requests in a project cannot exceed 64. |
| `requests.memory` | The sum of memory requests in a project cannot exceed 256 Gi. |
| `requests.ephemeral-storage` | The sum of local ephemeral storage requests in a project cannot exceed 128 Gi. |
| `limits.cpu` | The sum of CPU limits in a project cannot exceed 64. |
| `limits.memory` | The sum of memory limits in a project cannot exceed 256 Gi. |
| `limits.ephemeral-storage` | The sum of local ephemeral storage limits in a project cannot exceed 128 Gi. |
| Pod instances | You are limited to 250 pod instances per project. |
| Secrets | You are limited to 10 secrets per project. This total does not include image pull secrets. |
| Configmaps | You are limited to 20 configmaps per project.|
{: caption="Project quotas"}

<br />

## Application limits
{: #kn-limits_application}

The following table lists the limits for applications.

| Category           |   Default   |   Maximum  |  Minimum  |
| ---------          | ----------- | ---------- | --------- |
| CPU                |         0.1 |          8 |      0.01 |
| Ephemeral storage  |	     0.5 G |        2 G |     0.5 G |
| Max scale          |          10 |        250 |         0 |
| Memory             |         1 G |       32 G |     128 M |
| Min scale          |           0 |        250 |         0 |
| Parallel           |          10 |       1000 |         0 |
| Timeout            | 300 seconds | 600 seconds|         0 |
{: caption="Application limits"}

Note that {{site.data.keyword.codeengineshort}} does not support overcommitment for application resources. Therefore, if you create an application by using the API or with `kubectl apply -f <yaml>`, the values for `Resource.Requests` and `Resource.Limits` for `CPU`, `Memory`, and `Ephemeral Storage` must be the same. If you do not specify any values, the defaults are used:

Defaults

```
resources:
         limits:
           cpu: 500m
           memory: 1000Mi
           ephemeral-storage: 500Mi
         requests:
           cpu: 500m
           memory: 1000Mi
           ephemeral-storage: 500Mi
```

<br />

## Job limits
{: #kn-limits_job}

Job definitions, as templates for jobs, reflect the same limits as jobs. 

The following table lists the limits for jobs. 

| Category          |         Default         |         Maximum           |  Minimum  |
| -----------       | ----------------------- | ------------------------- | --------- |
| Array size        |                       1 |                      1000 |         1 |
| CPU               |                     0.1 |                         8 |      0.01 |
| Ephemeral storage |	                  0.5 G |                       2 G |     0.5 G |
| Memory            |                    1 Gi |                     32 Gi |    128 Mi |
| Retries           |                       3 |                         5 |         0 |
| Timeout           |  7200 seconds (2 hours) |    7200 seconds (2 hours) |  1 second |
{: caption="Job limits"}
