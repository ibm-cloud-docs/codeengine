---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-20"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Comparing Cloud Foundry and {{site.data.keyword.codeengineshort}} terms
{: #migrate-cf-ce-terms}

Before getting started with deploying apps in {{site.data.keyword.codeengineshort}}, learn the basics about {{site.data.keyword.codeengineshort}}. The following table describes some high level terminology differences between Cloud Foundry and {{site.data.keyword.codeengineshort}}.

| Cloud Foundry | {{site.data.keyword.codeengineshort}} | Description |
| -------------- | -------------- | -------------- |
| `Org` and `Space` | Resource group and projects | A grouping of workloads. The specific choice of which workload goes into each grouping is user defined. "Resource groups" are an {{site.data.keyword.cloud_notm}} concept, while "projects" are {{site.data.keyword.codeengineshort}} specific. Projects provide a level of isolation between workloads. See [Creating a project](#create-project). |
| Application | Application (app) | A workload that responds to HTTP requests regardless of the semantics, or purpose behind the request be it a REST API call, a web page request, or an event. {{site.data.keyword.codeengineshort}} requires that applications include the HTTP server as part of the code. Applications automatically scale (up and down) based on the incoming load. You can configure the minimum and maximum scale if needed. By default, the application listens on port 8080 by default. You can override this behavior by using the console or with the CLI `--port` flag. See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads). |
| N/A | Job or batch job | Any workload that does not listen for HTTP requests, but instead is invoked on-demand, and then exits when completed. Batch jobs can be scaled, but they are not scaled automatically. Instead, you can specify the number of instances that you want when you run your job. Jobs are often called "run to completion" workloads. See [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). |
| `cf push` | Build | Process of building a container image from source code. You can build code based on a Dockerfile or use a Paketo buildpack. Building source code in {{site.data.keyword.codeengineshort}} is a distinct step from deploying a workload in the CLI, unlike `cf push` which does it all in one step. You can build and deploy an application from a single step from the {{site.data.keyword.codeengineshort}} console. See [Planning your build](/docs/codeengine?topic=codeengine-plan-build). |
| Service binding | Service binding | Attach a workload to an {{site.data.keyword.cloud_notm}} managed service. The credentials and connection information is exposed to the workload through environment variables. The `CF_SERVICES` environment variable in Cloud Foundry is called `CE_SERVICES` in {{site.data.keyword.codeengineshort}}. See [Integrating {{site.data.keyword.cloud_notm}} services with service bind](/docs/codeengine?topic=codeengine-service-binding). |
| Routes and domains | N/A | Define and manage external URLs to your workloads. {{site.data.keyword.codeengineshort}} provides this capability implicitly. You can add [custom domains](/docs/codeengine?topic=codeengine-deploy-multiple-regions) through {{site.data.keyword.cis_full_notm}}. |
{: caption="Table 1. Terminology" caption-side="bottom"}

For additional terms and capabilities for {{site.data.keyword.codeengineshort}}, see [Learn about {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about).

