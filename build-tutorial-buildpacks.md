---

copyright:
  years: 2021
lastupdated: "2021-01-12"

keywords: code engine, tutorial, build, source, application

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


# Tutorial: Building applications using buildpacks
{: #build-app-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

In this tutorial, a container image is built from source using the {{site.data.keyword.codeengineshort}} CLI. The buildpacks strategy automatically detects how the application is to be created.
{: shortdesc}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpacks.

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

## Setup registry access
{: #setup-registry-access}
{: step}

The final image is stored in a container registry. For this, the registry access needs to be configured in {{site.data.keyword.codeengineshort}}. For example, in case the created container image is suppose to be stored in DockerHub, the `username` is the DockerHub account username. The `password` can either be the user account password, or a personal access token. In the example, the name `dockerhub` is only used to later better recognize which container registry is configured.

   ```
   ibmcloud ce registry create --name dockerhub --server https://index.docker.io/v1/ --username username --password password
   ```
   {: pre}

   **Example output**

   ```
   Creating image registry access secret 'dockerhub'...
   OK
   ```
   {: screen}

   For more information, see [add registry access documentation](/docs/codeengine?topic=codeengine-codeengine-add-registry#add-registry-access-ce).

## Create a build
{: #create-a-build}
{: step}

Create a build that contains all necessary pieces of information regarding your application code, i.e. where it is located and how it can accessed. This does not start any build process, it serves as the configuration for the build process. It may look effortful at first, but this build configuration makes it easier for later subsequent builds of the application, for example when changes were applied to the source repository.

   ```
   ibmcloud ce build create \
       --name tutorial-build \
       --source https://github.com/IBM/CodeEngine \
       --revision master \
       --context-dir /s2i-buildpacks \
       --image docker.io/twinpinesmall/tutorial \
       --registry-secret dockerhub \
       --size small \
       --strategy buildpacks
   ```
   {: pre}

   **Example output**

   ```
   Creating build 'tutorial-build'...
   OK
   ```
   {: screen}

The `--size` flag configures the sizing of the build container and can be one off either `small`, `medium`, `large`, or `xlarge`. This needs to be matched against the respective application build requirements. Use a larger size when the build exceeds the available resources, for example system memory. On the other side, the smaller the size, the faster the build process can be scheduled in the system.

## Submit buildrun
{: #submit-buildrun}
{: step}

1. Submit a buildrun by referencing the build configuration. If a specific name for this buildrun request is omitted, an unique name is used instead. The name of the buildrun is required for obtaining buildrun details, for example the logs of the buildrun.

    ```
    ibmcloud ce buildrun submit --build tutorial-build
    ```
    {: pre}

   **Example output**

   ```
   Submitting build run 'tutorial-build-run-851026-090000000'...
   OK
   ```
   {: screen}

1. Once submitted, the current status of the build run can be checked.

    ```
    ibmcloud ce buildrun get --name tutorial-build-run-851026-090000000
    ```
    {: pre}

   **Example output**

   ```
   Getting build run 'tutorial-build-run-851026-090000000'...
   OK
   
   Name:          tutorial-build-run-851026-090000000
   ID:            1648de3e-bfoo-4700-ae15-b69088d5d2f8
   Project Name:  tutorial-project
   Project ID:    0t6a35u9-9t76-4o56-r152-6ib0a36el7d2
   Age:           42s
   Created:       1985-10-26T09:00:00-08:00
   Status:
     Reason:     Running
     Succeeded:  Unknown
   ```
   {: screen}

   The build is complete when the `Succeeded` status is `True`.

1. In case of an issue with the buildrun, the log files of the actual build can be obtained.

    ```
    ibmcloud ce buildrun logs --buildrun tutorial-build-run-851026-090000000
    ```
    {: pre}

   **Example output**

   ```
   Getting build run 'tutorial-build-run-851026-090000000'...
   Getting instances of build run 'tutorial-build-run-851026-090000000'...
   Getting logs for build run 'tutorial-build-run-851026-090000000'...
   OK
   
   tutorial-build-run-851026-090000000-7vlrw-pod-c9t6g/step-git-source-source-7tbwh:
   {"level":"info","ts":1610378702.42616,"caller":"git/git.go:165","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 6b66f2bc3e1277c2e6475608a9c50335712116e0 (grafted, HEAD, origin/master) in path /workspace/source"}
   {"level":"info","ts":1610378703.5453625,"caller":"git/git.go:203","msg":"Successfully initialized and updated submodules in path /workspace/source"}
   [...]
   ```
   {: screen}

You have successfully built a container image from source code using the buildpacks build strategy!

## Work with created container image
{: #use-container-image}
{: step}

As part of the build process, the created container image is pushed to the configured container registry location. In this tutorial, the application is a web application and therefore can easily be brought online in {{site.data.keyword.codeengineshort}}.

   ```
   ibmcloud ce application create --name tutorial-app --image twinpinesmall/tutorial
   ```
   {: pre}

   **Example output**

   ```
   Creating application 'tutorial-app'...
   [...]
   ```
   {: screen}

## Next steps

For more information, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
