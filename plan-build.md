---
copyright:
  years: 2020
lastupdated: "2020-09-11"

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

You can use {{site.data.keyword.codeengineshort}} to build container images that you can deploy as applications or jobs.
{: shortdesc}

## Prepare your source repository
{: #build-plan-repo}

To give {{site.data.keyword.codeengineshort}} access to your source code, you need to make it available in a Git repository, for example in [GitHub](https://github.com/) or [GitLab](https://gitlab.com). If your source repository is public, you must add [access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-code-repositories.

## Decide which build strategy to use
{: #build-strategy}

{{site.data.keyword.codeengineshort}} can build your container image using two strategies:

- [Dockerfile](https://docs.docker.com/engine/reference/builder/) build using the [Kaniko](https://github.com/GoogleContainerTools/kaniko) tool. To use this strategy, you must add a Dockerfile your source repository that describes the steps to build a container image from your source repository. The Dockerfile may contain steps that copy static files from your sources into the container, for example to host them by a web service, or compile source code written in the language of your choice and add the resulting binary to your container image. 
- [Paketo Buildpacks](https://paketo.io/) inspect your source repository to detect which runtime environment your code is based on and how a container images is built from your sources. Buildpacks make assumptions on the directory structure of your source repositories. You should check the samples provided for you runtime to learn how to structure your source repository correctly. Optionally, you can add a `buildpack.yml` file to your source repository to configure the runtime environment version. The supported runtimes are:

  | Runtime   | Samples | `buildpack.yml` settings  |
  | --------- | ------------------------- | ------- |
  | Go        | [Go samples](https://github.com/paketo-buildpacks/samples/tree/main/go) | [Go version](https://github.com/paketo-buildpacks/go-dist#buildpackyml-configurations) |
  | Java      | [Java samples](https://github.com/paketo-buildpacks/samples/tree/main/java) | |
  | Node.js   | [Node.js samples](https://github.com/paketo-buildpacks/samples/tree/main/nodejs) | [Node.js version](https://github.com/paketo-buildpacks/node-engine#buildpackyml-configurations) |
  | PHP       | [PHP samples](https://github.com/paketo-buildpacks/samples/tree/main/php) | [PHP version](https://github.com/paketo-buildpacks/php-dist#buildpackyml-configurations) and [web server kind](https://github.com/paketo-buildpacks/php-web/tree/main#build) |
  | .NET Core | [.NET Core samples](https://github.com/paketo-buildpacks/samples/tree/main/dotnet-core) | [.NET Core SDK version](https://github.com/paketo-buildpacks/dotnet-core-sdk#buildpackyml-configurations) and [.NET Core Runtime version](https://github.com/paketo-buildpacks/dotnet-core-runtime#buildpackyml-configurations) |

  Consider to always specify the runtime version wherever possible in the `buildpack.yml` file. Specify the runtime ensures that your builds continue to run even if {{site.data.keyword.codeengineshort}} updates to the latest Paketo Buildpacks version including a newer default runtime version.
{: tip}

## Decide on the size of the build
{: #build-size}

{{site.data.keyword.codeengineshort}} classifies builds into `small`, `medium`, `large` and `xlarge` size. The size of the build defines how many CPU cores, memory and disk space is assigned to the build. A smaller build is cheaper, but typically also slower due to the lower number of CPU cores than a larger build. Also, the memory and disk requirements of your build might not be satisfiable with small builds.

If you are uncertain about which size to chose, consider starting with `small` or `medium`. If the build fails due to lack of memory or disk space, or is not fast enough, then switch to larger sizes.
{: tip}
