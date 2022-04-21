---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-21"

keywords: code engine, getting started, migrating, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Scaling, high availability, and traffic management
{: #migrate-cf-ce-scale}

When your app is deployed to {{site.data.keyword.codeengineshort}}, it is accessible and available for tests and even production. Because {{site.data.keyword.codeengineshort}} provides a serverless platform for containerized workloads, most of your runtime details are managed automatically by {{site.data.keyword.codeengineshort}}. You can, however, control many of the details.

## Scaling your app
{: #migrate-scale-app}

When working with Cloud Foundry, you might have used the [autoscaling feature](https://cloud.ibm.com/docs/cloud-foundry-public?topic=cloud-foundry-public-autoscale_cloud_foundry_apps){: external}. With this feature, you can automatically add and remove app instances, depending on performance metrics or date and time. By default, autoscaling is set to `off`, and some setup work is required to use it. In contrast, {{site.data.keyword.codeengineshort}} autoscales your application by default. {{site.data.keyword.codeengineshort}} scales an app up to 10 runtime instances (by default) and down to zero (meaning that the app does not consume any resources when not in use).

You can edit these settings within the [limits and quotas of the {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). A max scale of 0 (zero) scales your app to the maximum possible, if necessary. By adjusting the concurrency and request timeout, you can tune the autoscaler to your needs. For more information, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale)

## High availability
{: #migrate-ha}

For aspects of high availability (and disaster recovery), Cloud Foundry and {{site.data.keyword.codeengineshort}} are similar.

- Follow best practices for handling concurrent requests.
- Make sure to have at least two or even three instances of the app up and running.
- Run app instances in the available zones of a multi-zone region (MZR). 
- Use a [global load balancer (GLB)](/docs/codeengine?topic=codeengine-deploy-multiple-regions) in front of app instances deployed to multiple MZRs for high availability on a global level.

## Traffic management and rolling updates
{: #migrate-traffic-mgmt}

To keep your app available when deploying a new version on Cloud Foundry, you use special CLI command options for [rolling updates or zero-downtime deployments](https://docs.cloudfoundry.org/devguide/deploy-apps/rolling-deploy.html){: external}. With {{site.data.keyword.codeengineshort}}, the rolling updates are performed automatically. After the new app revision is ready, the traffic is moved from the old app to the new revision.

Performing blue-green deployments and gradually moving traffic from the old app to the new revision [required some manual intervention](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: external} in Cloud Foundry. With {{site.data.keyword.codeengineshort}}, you can use the capabilities built into its underlying Kubernetes and Knative layers. The blog post, [Blue-green deployment with IBM Cloud {{site.data.keyword.codeengineshort}} and Knative](https://blog.4loeser.net/2022/03/blue-green-deployment-ibm-cloud-code-engine-knative.html){: external}, shows how the Knative CLI command to update the app so that the traffic is configured to split between revisions. Given an app named `bluegreen` and two revisions `rev-old` and `rev-new`, the following command splits the traffic 80/20 between them.

```sh 
kn service update bluegreen --traffic rev-old=80 --traffic rev-new=20
```
{: pre}

By adjusting the assigned percentages, you can test new code version with some traffic first and, when your code is ready, run the revision in production.

## Next steps
{: #migrate-cf-ce-next-scale}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. [Try out {{site.data.keyword.codeengineshort}} with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. **Scaling, high availability, and traffic management**
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).

