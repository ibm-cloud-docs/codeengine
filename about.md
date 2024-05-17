---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-14"

keywords: benefits, terminology, developers, capabilities, code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Learn about {{site.data.keyword.codeengineshort}}
{: #about}

{{site.data.keyword.codeenginefull}} (or "{{site.data.keyword.codeengineshort}}") was developed by IBM with the goal of helping you create modern, source-centric, containerized, and serverless apps and jobs. The platform is designed to address the needs of developers who just want their code to run. {{site.data.keyword.codeengineshort}} abstracts the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code.
{: shortdesc}


## Benefits of {{site.data.keyword.codeengineshort}}
{: #benefits}

Review the capabilities that {{site.data.keyword.codeengineshort}} provides to run your workloads.

| Capability | Description |
| --------- | ------------------- |
| Runs your workloads | {{site.data.keyword.codeengineshort}} runs your HTTP-driven applications and your run-to-completion batch jobs.  |
| Fully managed service | {{site.data.keyword.codeengineshort}} takes care of all the cluster management, including provisioning, configuring, scaling, and managing servers so you do not need to worry about the underlying infrastructure.  |
| Builds your code | {{site.data.keyword.codeengineshort}} pulls your source code and creates the container image for you. {{site.data.keyword.codeengineshort}} supports both Dockerfile and Cloud Native Buildpack. |
| Private workloads | Store your source code in private repositories and push your images to private registries and {{site.data.keyword.codeengineshort}} can access them. |
| Fully integrated | {{site.data.keyword.codeengineshort}} is fully integrated into IBM Cloud so that you can take advantage of the full catalog of IBM Cloud services. |
| Event-driven workloads | Extend the functionality of your applications with messages (events) from event producers. Your application can then react to those events and perform actions based on them. |
| Autoscales - even to zero | {{site.data.keyword.codeengineshort}} automatically scales your workloads up and down, and even down to zero when no requests are active. You pay for only the resources that you consume. |
| Control access | Assign platform and services access permissions to your projects in IBM Cloud Identity and Access Management to control who can provision and manage resources in your IBM Cloud account. |
| Based on open source | {{site.data.keyword.codeengineshort}} is built on a set of open source technologies such as Kubernetes, Knative, Istio, and Tekton, keeping your apps and jobs portable. |
| DDoS protection | {{site.data.keyword.codeengineshort}} provides immediate DDoS protection for your application. {{site.data.keyword.codeengineshort}}'s DDoS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you. DDoS protection covers System Interconnection (OSI) Layer 3 and Layer 4 (TCP/IP) protocol attacks, but not Layer 7 (HTTP) attacks. See [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos). |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} benefits" caption-side="bottom"}


## {{site.data.keyword.codeengineshort}} terminology
{: #terminology}

Learn the basics about {{site.data.keyword.codeengineshort}} by reviewing the following key terms. Afterward, you can test your knowledge and [take a quiz!](https://ibm.biz/BdfFxR){: external}

| Term | Description |
| --------- | ------------------- |
| Application | An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming requests and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app.  |
| Build | A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks. |
| Code bundle | A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image. |
| Code repository | A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build. |
| Configmap | A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app, job, or function portable. A configmap contains information in key-value pairs. |
| Container image registry | A container registry, or registry, is a service that stores container images. For example, {{site.data.keyword.registryfull_notm}} and Docker Hub are container registries. A container registry can be public or private. A container registry that is public does not require credentials to access. In contrast, accessing a private registry does require credentials. |
| Function | A function is a stateless code snippet that performs tasks as it is invoked by HTTP requests. With IBM Code Engine functions, you can run your business logic in a scalable and serverless way. IBM Code Engine functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your function code can be written in a managed runtime that includes specific [Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime) versions. |
| Job | A job runs one or more instances of your executable code in parallel. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. |
| Project | A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. A project provides the following items. \n - Provides a unique namespace for entity names. \n - Manages access to project resources (inbound access). \n - Manages access to backing services, registries, and repositories (outbound access). \n - Has an automatically generated certificate for Transport Layer Service (TLS). |
| Secret | A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app, function, or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs. |
| Service binding | Service bindings provide applications, jobs, and functions access to {{site.data.keyword.cloud_notm}} services. |
| Subscription | A subscription provides a way of signing up to receive events from a particular event producer. For more information about the different types of event producers and how to subscribe to them, see [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events). |
{: caption="Table 2. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}
