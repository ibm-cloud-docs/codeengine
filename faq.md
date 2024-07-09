---

copyright:
  years: 2020, 2024
lastupdated: "2024-07-09"

keywords: faq for code engine, project faq for code engine, feedback for code engine, code samples for code engine, terms of service for code engine, faq, feedback, terms, code samples, project, code engine, limits

subcollection: codeengine

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.codeenginefull}} service.
{: shortdesc}

## What is {{site.data.keyword.codeenginefull_notm}}?
{: #what-is-codeengine}
{: faq}
{: support}

{{site.data.keyword.codeengineshort}} is developed by IBM and it is built with many open source components. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps that run on your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. For more information, see [About {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about).

With {{site.data.keyword.codeengineshort}}, you can deploy applications, run jobs, and even build source code from a single dashboard.

## What is a project?
{: #what-is-project}
{: faq}
{: support}

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. 

A project provides the following items. 

- Provides a unique namespace for entity names.
- Manages access to project resources (inbound access).
- Manages access to backing services, registries, and repositories (outbound access).
- Has an automatically generated certificate for Transport Layer Service (TLS).

For more information about projects, see [Manage projects](/docs/codeengine?topic=codeengine-manage-project).

## Where can I find code samples?
{: #find-code-samples}
{: faq}
{: support}

You can find code samples to help you explore the capabilities of {{site.data.keyword.codeengineshort}}. Visit our [{{site.data.keyword.codeengineshort}} code samples repository on GitHub](https://github.com/IBM/CodeEngine){: external}.

## I need more memory! Can I increase my limits?
{: #increase-ce-limits}
{: faq}
{: support}

Yes, you can increase your {{site.data.keyword.codeengineshort}} [limits](/docs/codeengine?topic=codeengine-limits) by contacting [IBM support](/docs/codeengine?topic=codeengine-get-support).

## Do I need a Docker Hub account to use {{site.data.keyword.codeengineshort}}?
{: #dockerhub-options}
{: faq}
{: support}

{{site.data.keyword.codeengineshort}} does not require a Docker Hub account. Although {{site.data.keyword.codeengineshort}} does run containers, you do not need to understand container technology to deploy workloads on {{site.data.keyword.codeengineshort}}. You can start with source code and {{site.data.keyword.codeengineshort}} builds the container image for you and stores it in an {{site.data.keyword.registrylong_notm}} namespace that is owned by your account. Although {{site.data.keyword.registrylong_notm}} is used as the default container registry, {{site.data.keyword.codeengineshort}} can push and pull images from any other public and private registry that is accessible from {{site.data.keyword.cloud_notm}}.

## What is the difference between a Docker build on my system and a build in {{site.data.keyword.codeengineshort}}?
{: #dockerbld-cebuild}
{: faq}
{: support}

The result of a Docker build that you run on your local system is the same container image that you get if you run a build with the same Dockerfile in {{site.data.keyword.codeengineshort}}. However, the build in {{site.data.keyword.codeengineshort}} is not running on your local system, but instead in the {{site.data.keyword.codeengineshort}} system. This build in {{site.data.keyword.codeengineshort}} gives you several advantages.

1. You are not required to install software, such as Docker Desktop, locally.
2. You can use the resources that are provided by {{site.data.keyword.codeengineshort}}. For example, you can take advantage of the speed of {{site.data.keyword.cloud_notm}} to push and pull container registry images for you.
3. You can build your container image by using the [Buildpacks build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy) instead of Dockerfile, which detects your sources for various languages and automatically builds a container out of it.
4. If you have an image that was built with a non-Intel based processor, {{site.data.keyword.codeengineshort}} can rebuild it for you.

## Why do images that are built with non-Intel processors not work with {{site.data.keyword.codeengineshort}}?
{: #buildimage-nonintel}
{: faq}
{: support}

If you have an image that exists in a container registry and the image was built with a non-Intel based processor, {{site.data.keyword.codeengineshort}} cannot run your container image. {{site.data.keyword.codeengineshort}} uses Intel-based processing. You can build your own image if you use Intel processing (x86 processor). You can also choose to let {{site.data.keyword.codeengineshort}} handle the build process for you. For more information, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build).

## Do {{site.data.keyword.codeengineshort}} apps support WebSockets?
{: #app-websockets}
{: faq}
{: support}

Yes! You can find a [sample app that uses WebSockets](https://github.com/IBM/CodeEngine/tree/main/websocket){: external} by visiting our {{site.data.keyword.codeengineshort}} samples repository on GitHub.

The maximum time for any connection to an application is 10 minutes, even if the connection is not idle. With {{site.data.keyword.codeengineshort}}, you can configure this connection time with the `timeout` value. With the CLI, use the `--timeout` option with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or the [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. From the console, you can set the `Timeout` value for your app from the **Resources & scaling** tab. For an app that use WebSockets, the client must reconnect to the app after the connection is closed. So, if your app needs a persistent connection, create a new connection before the `timeout` value is reached.
{: note}

## Do {{site.data.keyword.codeengineshort}} apps support gRPC?
{: #app-grpc-supported}
{: faq}
{: support}

Yes! You can find a [sample app that uses gRPC](https://github.com/IBM/CodeEngine/tree/main/grpc){: external} by visiting our {{site.data.keyword.codeengineshort}} samples repository on GitHub.

Because gRPC depends on HTTP/2, you must set the port name to `h2c` and the port value to `8080`, and then your {{site.data.keyword.codeengineshort}} application can support HTTP/2 traffic. Use the {{site.data.keyword.codeengineshort}} CLI to configure the `--port h2c:8080` option with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command or the [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command to configure your application to use gRPC. See [Implementing applications with gRPC](/docs/codeengine?topic=codeengine-app-grpc).

## Does {{site.data.keyword.codeengineshort}} provide a way to limit access to a particular entity within a {{site.data.keyword.codeengineshort}} project?
{: #limit-access-fun}
{: faq}
{: support}

No, in {{site.data.keyword.codeengineshort}}, roles that are applied to any {{site.data.keyword.codeengineshort}} entity are only scoped to the project that is selected as the current context. Thus, you cannot control permissions on individual resources within a {{site.data.keyword.codeengineshort}} project.

## Does {{site.data.keyword.codeengineshort}} provide an OpenAPI specification for the deployed function?
{: #openapi-spec-fun}
{: faq}
{: support}

No, {{site.data.keyword.codeengineshort}} does not generate or provide an OpenAPI specification for the functions you deploy. There are packages and tools available for many programming languages to generate an OpenAPI specification from code.



## How can I review the {{site.data.keyword.codeengineshort}} service terms?
{: #review-service-terms}
{: faq}
{: support}

For the latest service level agreement terms, see the [terms of service](/docs/overview?topic=overview-terms).

## How can I give feedback?
{: #give-feedback}
{: faq}
{: support}

Your feedback on {{site.data.keyword.codeengineshort}} is important to us and helps us improve. You can provide feedback in multiple ways:

* Click **Open doc issue** at the end of a documentation page to open an issue  and provide your comments.
* Share feedback through Slack. You can [register](https://cloud.ibm.com/kubernetes/slack){: external} and join the discussion in the [#code-engine channel](https://ibm-cloud-success.slack.com){: external}.
