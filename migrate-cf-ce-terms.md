---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-10"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Comparing Cloud Foundry and {{site.data.keyword.codeengineshort}} terms
{: #migrate-cf-ce-terms}

Before you get started with deploying apps in {{site.data.keyword.codeengineshort}}, learn the basics about {{site.data.keyword.codeengineshort}}. The following table describes some high-level terminology differences between Cloud Foundry and {{site.data.keyword.codeengineshort}}.

| Cloud Foundry | {{site.data.keyword.codeengineshort}} | Description |
| -------------- | -------------- | -------------- |
| `Org` and `Space` | Resource group and projects | A grouping of workloads. The specific choice of which workload goes into each grouping is defined by the user. "Resource groups" are an {{site.data.keyword.cloud_notm}} concept, while "projects" are {{site.data.keyword.codeengineshort}} specific. Projects provide a level of isolation between workloads. See [Managing projects](/docs/codeengine?topic=codeengine-manage-project). |
| Application | Application (app) | A workload that responds to HTTP requests from a REST API, a web page request, or an event, for example. {{site.data.keyword.codeengineshort}} requires that applications include the HTTP server as part of the code. Applications automatically scale (up and down) based on the incoming load. You can configure the minimum and maximum scale if needed. By default, the application listens on port 8080 by default. You can override this behavior by using the console or with the CLI `--port` flag. See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads). |
| N/A | Job or batch job | Any workload that does not listen for HTTP requests, but instead is invoked on demand, and then exits when completed. Batch jobs can be scaled, but they are not scaled automatically. Instead, you can specify the number of instances that you want when you run your job. Jobs are often called "run to completion" workloads. See [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). |
| `cf push` | Build and deploy | Process of building a container image from source code and deploying an app in a single step. You can build code based on a Dockerfile or use a Paketo buildpack. You can build from a single step in the CLI as well as from the {{site.data.keyword.codeengineshort}} console. See [Planning your build](/docs/codeengine?topic=codeengine-plan-build). |
| Service binding | Service binding | Attach a workload to an {{site.data.keyword.cloud_notm}} managed service. The credentials and connection information is exposed to the workload through environment variables. The `VCAP_SERVICES` environment variable in Cloud Foundry is called `CE_SERVICES` in {{site.data.keyword.codeengineshort}}. See [Integrating {{site.data.keyword.cloud_notm}} services with service bind](/docs/codeengine?topic=codeengine-service-binding). |
| Routes and domains | N/A | Define and manage external URLs to your workloads. {{site.data.keyword.codeengineshort}} provides this capability implicitly. You can add [custom domains](/docs/codeengine?topic=codeengine-deploy-multiple-regions) through {{site.data.keyword.cis_full_notm}} or any other domain provider of your choice. For more information about adding a custom domain, see the [Configuring a Custom Domain for Your IBM Cloud Code Engine Application](https://www.ibm.com/cloud/blog/configuring-a-custom-domain-for-your-ibm-cloud-code-engine-application){: external}  blog. |
{: caption="Table 1. Terminology" caption-side="bottom"}

For more terms and capabilities for {{site.data.keyword.codeengineshort}}, see [Learn about {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about).

## Next steps
{: #migrate-cf-ce-next-terms}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. **Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}} (current page)**
3. [Try out {{site.data.keyword.codeengineshort}} with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).

