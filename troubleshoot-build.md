---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-20"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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


# Debugging builds 
{: #troubleshoot-build}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} builds and runs of your build.
{: shortdesc}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

When your build isn't behaving as expected, looking at logs and system events can provide information that might help you debug the problem. 

## Build limits to consider 
{: #ts-build-limits}

The maximum number of build configurations that you can have per project is 100. You are limited to a total of 100 build runs per project before you need to remove or clean up old ones.

For more information about limits for builds including memory and cpu, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Getting logs for my builds
{: #ts-build-gettinglogs}

Logs can be helpful to troubleshoot problems when you run builds. You can view logs for builds with the CLI. 
{: shortdesc}

Use the [**`ibmcloud ce buildrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command to display logs about the build run. Use this command to display logs of all of the instances of a build run based on the name of the build run.

To view the logs for all instances of the `mybuildrun` build run, specify the name of the build run with the `--name` option; for example,  

```
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

**Example output**

```
Getting build run 'mybuildrun'...
Getting instances of build run 'mybuildrun'...
Getting logs for build run 'mybuildrun'...
OK

mybuildrun-bvzbg-pod-tppvg/step-source-default:
{"level":"info","ts":1625216559.539348,"logger":"git","msg":"ssh","path":"/usr/bin/ssh","version":"OpenSSH_8.0p1, OpenSSL 1.1.1g FIPS  21 Apr 2020"}
{"level":"info","ts":1625216559.5415168,"logger":"git","msg":"git","path":"/usr/bin/git","version":"git version 2.27.0"}
{"level":"info","ts":1625216559.5584946,"logger":"git","msg":"git-lfs","path":"/usr/bin/git-lfs","version":"git-lfs/2.11.0 (GitHub; linux amd64; go 1.14.4)"}
{"level":"debug","ts":1625216559.5586145,"logger":"git","msg":"/usr/bin/git clone --quiet --no-tags --branch main --depth 1 --single-branch -- https://github.com/IBM/CodeEngine /workspace/source"}
{"level":"debug","ts":1625216560.6602066,"logger":"git","msg":"/usr/bin/git -C /workspace/source submodule update --init --recursive"}
{"level":"debug","ts":1625216560.7951796,"logger":"git","msg":"/usr/bin/git -C /workspace/source rev-parse --verify HEAD"}

mybuildrun-bvzbg-pod-tppvg/step-build-and-push:
INFO[0000] Retrieving image manifest golang:alpine
INFO[0000] Retrieving image golang:alpine from registry index.docker.io
INFO[0001] Retrieving image manifest alpine
INFO[0001] Retrieving image alpine from registry index.docker.io
INFO[0003] Built cross stage deps: map[0:[/codeengine]]
INFO[0003] Retrieving image manifest golang:alpine
INFO[0003] Returning cached image manifest
INFO[0003] Executing 0 build triggers
INFO[0003] Unpacking rootfs as cmd COPY ./helloworld /helloworld requires it.
INFO[0009] COPY ./helloworld /helloworld
INFO[0009] Taking snapshot of files...
INFO[0009] COPY codeengine.go /
INFO[0009] Taking snapshot of files...
INFO[0009] RUN go build -o /codeengine /codeengine.go
INFO[0009] Taking snapshot of full filesystem...
INFO[0017] cmd: /bin/sh
INFO[0017] args: [-c go build -o /codeengine /codeengine.go]
INFO[0017] Running: [/bin/sh -c go build -o /codeengine /codeengine.go]
INFO[0018] Taking snapshot of full filesystem...
INFO[0018] Saving file codeengine for later use
INFO[0018] Deleting filesystem...
INFO[0019] Retrieving image manifest alpine
INFO[0019] Returning cached image manifest
INFO[0019] Executing 0 build triggers
INFO[0019] Unpacking rootfs as cmd COPY --from=0 /codeengine /codeengine requires it.
INFO[0019] COPY --from=0 /codeengine /codeengine
INFO[0019] Taking snapshot of files...
INFO[0019] CMD /codeengine
INFO[0019] Pushing image to us.icr.io/acme-namespace/codeengine-sample
INFO[0023] Pushed image to 1 destinations
```
{: screen}

## Getting system event information for my builds
{: #ts-build-gettingevent}

System event information can be helpful to troubleshoot problems when you run builds. You can view system event information for builds with the CLI. 
{: shortdesc}

1. Use the [**`ibmcloud ce buildrun list`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-list) command to list all of your build runs in a project; for example,

    ```
    ibmcloud ce buildrun list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command to get the details of your a build run, for example,

    ```
    ibmcloud ce buildrun get --name mybuildrun  
    ```
    {: pre}

    **Example output** 

    ```
    Getting build run 'mybuildrun'...
    OK

    Name:          mybuilddrun
    [...]

    Created:       2021-06-01T11:43:24-04:00

    Summary:  Succeeded
    Status:   Succeeded
    Reason:   All Steps have completed executing

    Image:  us.icr.io/mynamespace/codeengine-codeengine-200
    ```
    {: screen}

3. Display the system events of your build run. Use the [**`ibmcloud ce buildrun events`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-events) command; for example,

    ```
    ibmcloud ce buildrun events --name mybuildrun 
    ```
    {: pre} 

    **Example output** 

    ```
    Getting build run 'mybuildrun'...
    Getting instances of build run 'mybuildrun'...
    Getting events for build run 'mybuildrun'...
    OK

    mybuildrun-bvzbg-pod-tppvg:
        Type    Reason     Age    Source                Messages
        Normal  Scheduled  4m43s  default-scheduler     Successfully assigned 62ckpsxlh7x/mybuildrun-bvzbg-pod-tppvg to 10.242.0.17
        Normal  Pulled     4m42s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/tekton-pipeline/entrypoint-bff0a22da108bc2f16c818c97641a296:v0.23.0-rc6@sha256:43dd56a6c7c10f80300a861615f6f8d91c026deba744f81553a4e536b301b322" already present on machine
        Normal  Created    4m42s  kubelet, 10.242.0.17  Created container place-tools
        Normal  Started    4m41s  kubelet, 10.242.0.17  Started container place-tools
        Normal  Pulled     4m40s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/git:v0.8.100" already present on machine
        Normal  Created    4m40s  kubelet, 10.242.0.17  Created container step-source-default
        Normal  Started    4m40s  kubelet, 10.242.0.17  Started container step-source-default
        Normal  Pulled     4m40s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/kaniko/executor:v1.6.0-rc1" already present on machine
        Normal  Created    4m40s  kubelet, 10.242.0.17  Created container step-build-and-push
        Normal  Started    4m40s  kubelet, 10.242.0.17  Started container step-build-and-push
    ```
    {: screen}

    Events are only stored for one hour in the system.
    {: tip}


