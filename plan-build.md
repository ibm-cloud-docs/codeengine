---

copyright:
  years: 2021
lastupdated: "2021-01-27"

keywords: build for code engine, planning for code engine, source code building for code engine, source code repositories and code engine, image builds for code engine, container image builds for code engine, build strategy for code engine, build size for code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
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
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Planning your build
{: #plan-build}

Before you start building images, learn about the different options you have for your build.
{: shortdesc}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpacks.

## Prepare your source repository
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository, for example in [GitHub](https://github.com/){: external} or [GitLab](https://gitlab.com){: external}. If your source repository is not public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories).

## Choose a build strategy
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image by using one of following strategies:

- [Dockerfile](https://docs.docker.com/engine/reference/builder/){: external} build that uses the [Kaniko](https://github.com/GoogleContainerTools/kaniko){: external} tool. To use this strategy, add a Dockerfile to your source repository. This Dockerfile describes the steps that are needed to build a container image from your source repository. The Dockerfile might contain steps that copy static files from your sources into the container to be hosted by a web service, for example. It might compile source code that is written in the language of your choice and add the resulting binary to your container image. For more information about Dockerfile builds, see [Writing a Dockerfile for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-dockerfile).

- [Cloud Native Buildpack](https://buildpacks.io/){: external} that uses [Paketo](https://paketo.io/){: external} to inspect your source repository and detect which runtime environment that your code is based on and how a container image is built from your sources. Buildpacks make assumptions about the directory structure of your source repositories. For more information about how to structure your source repository correctly, see the samples that are provided for your runtime.

| Runtime   | Version | Samples |
| --------- | ------- | ------- |
| Go        | 1.15.7  | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go){: external}. |
| Java      | 11.0.9  | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java){: external}. |
| Node.js   | 14.15.1 | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs){: external}. |
| PHP       | 7.4.13  | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php){: external}. |
| Ruby      | 2.7.2   | [Ruby samples](https://github.com/paketo-buildpacks/samples/tree/main/ruby){: external}. |
| .NET Core | 5.0.100 (.NET Core SDK),</br> 5.0.0 (.NET Core Runtime) | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core){: external}. |
{: caption="Runtime sample files" caption-side="top"}

## Determine the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large`, and `xlarge` size. The size of the build defines how CPU cores, memory, and disk space are assigned to the build. A smaller build is less expensive, but typically also slower due to the lower number of CPU cores. Also, the memory and disk requirements of your build might cause the build to fail with a smaller size.

| Size | Dockerfile | Buildpacks |
| --------- | -------- | -------- |
| `small` | <ul><li>**CPU** 0.5</li><li>**Memory** 2 GB</li></ul> | <ul><li>**CPU** 0.5</li><li>**Memory** 2 GB</li></ul> |
| `medium` | <ul><li>**CPU** 1</li><li>**Memory** 4 GB</li></ul> | <ul><li>**CPU** 1</li><li>**Memory** 4 GB</li></ul> |
| `large` | <ul><li>**CPU** 2</li><li>**Memory** 8 GB</li></ul> | <ul><li>**CPU** 2</li><li>**Memory** 8 GB</li></ul> |
| `xlarge` | <ul><li>**CPU** 3</li><li>**Memory** 12 GB</li></ul> | <ul><li>**CPU** 3</li><li>**Memory** 12 GB</li></ul> |
{: caption="Build size values." caption-side="top"}

If you are uncertain about which size to choose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}

## Choose your container image registry
{: #build-registry}

After your container image is built, store it in a container image repository. With {{site.data.keyword.codeengineshort}}, you can [add access to your private container image registries](/docs/codeengine?topic=codeengine-plan-image).

## Next steps
When your planning is complete, [build your container image](/docs/codeengine?topic=codeengine-build-image).
