---

copyright:
  years: 2020
lastupdated: "2020-07-07"

keywords: knative

subcollection: code-engine

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

# Limits
{: #kn-limits}

The following sections provide technical details about the {{site.data.keyword.codeengineshort}} limit settings.
{: shortdesc}

## Experimental release limitations
{: #kn-limits_experimental}

During the Experimental release of {{site.data.keyword.codeenginefull_notm}}, be aware of the following limitations:

- One project per location
- After 7 days, your project and everything that the project contains will be deleted.

Be aware that Experimental releases are not intended for production and any projects, apps, or jobs that you create during Experimental will not carry over to other releases.

## Application limits
{: #kn-limits_application}

The following table lists the limits for Applications.

| Category  |   Default   |   Maximum  |  Minimum  |
| --------- | ----------- | ---------- | --------- |
| CPU       |         0.1 |          8 |      0.01 |
| Max scale |          10 |        250 |         0 |
| Memory    |         1 G |       32 G |     128 M |
| Min scale |           0 |        250 |         0 |
| Parallel  |          10 |       1000 |         0 |
| Timeout   | 300 seconds | 600 seconds|         0 |
{: caption="Application limits"}

<br />

## Job limits
{: #kn-limits_job}

Job definitions, as templates for jobs, reflect the same limits as jobs. 

The following table lists the limits for jobs. 

| Category    |         Default         |         Maximum           |  Minimum  |
| ----------- | ----------------------- | ------------------------- | --------- |
| Array size  |                       5 |                       250 |         1 |
| CPU         |                       1 |                         8 |         1 |
| Memory      |                      1G |                       32G |      128M |
| Retries     |                       2 |                         5 |         0 |
| Timeout     | 300 seconds (5 minutes) |  86400 seconds (24 hours) |         0 |
{: caption="Job limits"}
