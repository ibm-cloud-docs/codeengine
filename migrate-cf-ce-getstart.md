---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-25"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with your migration from Cloud Foundry to {{site.data.keyword.codeengineshort}}
{: #migrate-cf-ce-getstart}


{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads. {{site.data.keyword.codeengineshort}} even builds container images for you from your source code. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on **writing code** and not on the infrastructure that is needed to host it.
{: shortdesc}

{{site.data.keyword.codeengineshort}} was designed with the following key goals in mind.

- **Focus on your code**. {{site.data.keyword.codeengineshort}} provides a simplified developer experience. No need to learn about or manage the underlying infrastructure.
- **Support the modern runtime characteristics**, such as autoscaling, scaling to zero when idle, and seamless integration with managed services and security.
- **Support all your Cloud-native based applications**, whether they are 12-factor apps, event-driven functions, or run-to-completion batch-jobs. If it can be containerized, {{site.data.keyword.codeengineshort}} can run it.
- **Pay for only the resources** that you actually use.

If you are coming from a Cloud Foundry background, many of these features sound familiar. However, {{site.data.keyword.codeengineshort}} also includes some new capabilities that allow you to go beyond even what Cloud Foundry offers, including applications that can scale to zero and incur no charges. So, after you're past the syntactical difference of the user experience, you and your applications will feel right at home in {{site.data.keyword.codeengineshort}}.

## Migration considerations
{: #migrate-cf-ce-considerations}

To migrate an existing solution from Cloud Foundry to {{site.data.keyword.codeengineshort}}, consider the following aspects of your code.

- Code migration
- Service binding
- Build and deployment process (for example, commands, toolchain integration, DevOps)
- Scaling and resource management, including high availability
- Routing
- Security and compliance

All these aspects depend on the complexity of your solution, its performance and availability requirements, organizational characteristics, and more.

## Next steps
{: #migrate-cf-ce-next}

1. **Getting started (current page)**
2. [Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. [Try out {{site.data.keyword.codeengineshort}} with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).


