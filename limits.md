---

copyright:
  years: 2021
lastupdated: "2021-03-18"

keywords: limits for code engine, limitations for code engine, quotas for code engine, project quotas in code engine, app limits in code engine, job limits in code engine, limits, limitations, quotas

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


# Limits and quotas for {{site.data.keyword.codeengineshort}}
{: #limits}

The following sections provide technical details about the {{site.data.keyword.codeengineshort}} limitation and quota settings.
{: shortdesc}

## Beta release limitations
{: #beta-limits}

Beta releases are not intended for production and any projects, apps, or jobs that you create during Beta will not carry over to other releases.

## Project quotas
{: #project_quotas}

The following table lists the quotas for projects.

| Category  |   Description      | 
| --------- | -----------        | 
| Apps | You are limited to 100 apps per project. |
| App revisions | You are limited to a total of 100 revisions for all apps per project. |
| Builds | You are limited to 100 build configurations per project. |
| Build runs | You are limited to 100 build runs per project before you need to remove or cleanup old ones. |
| Configmaps | You are limited to 100 configmaps per project. |
| CPU | All of the apps and jobs combined cannot exceed 64 vCPUs. |
| Ephemeral storage | All of the apps and jobs combined cannot exceed 256 G of ephemoral storage. |
| Instances (active) | The number of app instances, running job instances, and running build instances cannot exceed 250. |
| Instances (total)  | The number of active instances and the number of completed job and build instances cannot exceed 2500. |
| Jobs | You are limited to 100 jobs per project. |
| Job runs | You are limited to 100 job runs per project before you need to remove or cleanup old ones. |
| Memory | All of the apps and jobs combined cannot exceed 256 G of memory. |
| Secrets | You are limited to 100 secrets per project. |
| Subscriptions ({{site.data.keyword.cos_full_notm}}) | You are limited to 100 ({{site.data.keyword.cos_short}}) subscriptions per project. |
| Subscriptions (ping) | You are limited to 100 ping subscriptions per project. |
{: caption="Project quotas"}

<br />

## Application limits
{: #limits_application}

The following table lists the limits for applications.

| Category                    |         Minimum         |         Maximum           |        Default         |
| --------------------------- | ----------------------- | ------------------------- | ---------------------- |
| CPU                         |                    0.01 |                       8.0 |             0.1 (100m) |
| Ephemeral storage           |	                   40 M |                      32 G |                  400 M |
| Max scale                   |                       0 |                       250 |                     10 |
| Memory                      |                    40 M |                      32 G |                  400 M |
| Min scale                   |                       0 |                       250 |                      0 |
| Concurrency                 |                       1 |                      1000 |                    100 |
| Timeout                     |                       0 |                600 seconds|            300 seconds |
{: caption="Application limits"}

{{site.data.keyword.codeengineshort}} does not support overcommitment for application resources. Therefore, if you create an application by using the API or with `kubectl apply -f <yaml>`, the values for `Resource.Requests` and `Resource.Limits` for `CPU`, `Memory`, and `Ephemeral Storage` must be specified and must be the same.

<br />

## Job limits
{: #limits_job}

Job definitions, as templates for jobs, reflect the same limits as jobs. 

The following table lists the limits for jobs. 

| Category                    |    Minimum    |         Maximum           |        Default         |
| --------------------------- | ------------- | ------------------------- | ---------------------- |
| Array: Array indices        |             0 |                   9999999 |                      0 |
| Array: Number of instances  |             1 |                      1000 |                      1 |
| CPU                         |          0.01 |                       8.0 |             0.1 (100m) |
| Ephemeral storage           |	         40 M |                      32 G |                  400 M |
| Memory                      |          40 M |                      32 G |                  400 M |
| Retries                     |             0 |                         5 |                      3 |
| Timeout                     |      1 second |  43200 seconds (12 hours) | 7200 seconds (2 hours) |
{: caption="Job limits"}

*Array indices* is a comma-separated list or hyphen-separated range of indices, which specifies the job instances to run; for example, `1,3,6,9` or `1-5,7-8,10`. 

*Number of instances* is the number of job instances to run in parallel. 

### Job size limit
{: #job_size_limit}

{{site.data.keyword.codeengineshort}} limits the size of jobs and job runs with a maximum of 10 KiB. When creating or updating jobs and job runs with the console, CLI, or API, {{site.data.keyword.codeengineshort}} checks the size of the job or job run. If the operation exceeds the limit, you will receive a size limit exceeded error. If you receive this error, try reducing the size of your job or job run in one of the following ways:

* If you are using commands and arguments, try reducing the use of these, make them shorter, or move them into the container image that is used by your job or job run. 

* If you are using environment variables, try using fewer environment variables or make them shorter. You can use secrets or configmaps to define environment variables and import them into the job by using the ` --env-from-secret` or ` --env-from-configmap` options with the [`job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create), [`job update`](/docs/codeengine?topic=codeengine-cli#cli-job-update), [`jobrun submit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), and [`jobrun resubmit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

