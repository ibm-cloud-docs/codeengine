---
copyright:
  years: 2020
lastupdated: "2020-09-15"

keywords: code engine, tutorial, application

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Planning your build
{: #plan-build}

You can use {{site.data.keyword.codeengineshort}} to build container images that you can deploy as applications or jobs. Before you start building images, however, learn about the different options you have for your build.
{: shortdesc}

## Prepare your source repository
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository, for example in [GitHub](https://github.com/){: external} or [GitLab](https://gitlab.com){: external}. If your source repository is not public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories).

## Choose a build strategy
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image by using one of two strategies:

- [Dockerfile](https://docs.docker.com/engine/reference/builder/){: external} build that uses the [Kaniko](https://github.com/GoogleContainerTools/kaniko){: external} tool. To use this strategy, add a Dockerfile your source repository. This Dockerfile describes the steps needed to build a container image from your source repository. The Dockerfile might contain steps that copy static files from your sources into the container to be hosted by a web service, for example. It might compile source code that is written in the language of your choice and add the resulting binary to your container image.

- [Cloud Native Buildpack](https://buildpacks.io/){: external} that uses [Paketo](https://paketo.io/){: external} to inspect your source repository and detect which runtime environment that your code is based on and how a container image is built from your sources. Buildpack makes assumptions about the directory structure of your source repositories. For more information about how to structure your source repository correctly, see the samples provided for your runtime.

| Runtime   | Version | Samples |
| --------- | ------- | ------- |
| Go        | 1.13.12 | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go){: external} |
| Java      | 11      | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java){: external} |
| Node.js   | 10.21.0 | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs){: external} |
| PHP       | 7.2.31  | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php){: external} |
| .NET Core | 3.1.212 (.NET Core SDK),</br> 3.1.4 (.NET Core Runtime) | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core){: external} |
{: caption="Runtime sample files" caption-side="top"}

## Determine the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large`, and `xlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build. A smaller build is less expensive, but typically also slower due to the lower number of CPU cores. Also, the memory and disk requirements of your build might cause the build to fail with a smaller size.

| Size | Dockerfile | Buildpacks |
| --------- | -------- | -------- |
| small | <ul><li>CPU: 0.53</li><li>Memory: 896 Mi</li></ul> | <ul><li>CPU: 0.57</li><li>Memory: 1408 Mi</li></ul> |
| medium | <ul><li>CPU: 1.03</li><li>Memory: 1408 Mi</li></ul> | <ul><li>CPU: 1.07</li><li>Memory: 1920 Mi</li></ul> |
| large | <ul><li>CPU: 2.03</li><li>Memory: 2432 Mi</li></ul> | <ul><li>CPU: 2.07</li><li>Memory: 2944 Mi</li></ul> |
| xlarge | <ul><li>CPU: 3.03</li><li>Memory: 3456 Mi</li></ul> | <ul><li>CPU: 3.07</li><li>Memory: 3992 Mi</li></ul> |
{: caption="Build size values" caption-side="top"}

If you are uncertain about which size to choose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}

## Choose your container image registry
{: #build-registry}

After your container image is built, store it in a container image repository. A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private. With {{site.data.keyword.codeengineshort}}, you can [add access to your private container image registries](/docs/codeengine?topic=codeengine-plan-image).

## Next steps
When your planning is complete, [build your container image](/docs/codeengine?topic=codeengine-build-image).
