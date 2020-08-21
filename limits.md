---

copyright:
  years: 2020
lastupdated: "2020-08-18"

keywords: code engine

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Limits and quotas for {{site.data.keyword.codeengineshort}}
{: #kn-limits}

The following sections provide technical details about the {{site.data.keyword.codeengineshort}} limit settings.
{: shortdesc}

## Experimental release limitations
{: #kn-limits_experimental}

During the Experimental release of {{site.data.keyword.codeenginefull_notm}}, be aware of the following limitations.

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
