---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-20"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}}: Getting started
{: #migrate-cf-ce-getstart}

{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads. {{site.data.keyword.codeengineshort}} even builds container images for you from your source code. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on writing code and not on the infrastructure that is needed to host it.
{: shortdesc}

{{site.data.keyword.codeengineshort}} was designed with the following key goals in mind.

- Provide a first class, simplified developer experience where the developer does not need to learn about or manage the underlying infrastructure.
- Support the modern runtime characteristics that people expect today, such as autoscaling, scaling to zero when idle, and seamless integration with managed services and security.
- Support all your Cloud-native based applications, whether they are [12-factor apps](https://12factor.net/){: external}, event-driven functions, or run-to-completion batch-jobs. If it can be containerized, {{site.data.keyword.codeengineshort}} can run it.
- Pay for only the resources that you actually use.

If you are coming from a Cloud Foundry background, many of these features sound familiar. However, {{site.data.keyword.codeengineshort}} also includes some new capabilities that allow you to go beyond even what Cloud Foundry offers, including applications that can scale to zero and incur no charges. So, after you're past the syntactical difference of the user experience, you and your applications will feel right at home in {{site.data.keyword.codeengineshort}}.

