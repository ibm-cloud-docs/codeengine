---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-01"

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
{:terraform: .ph data-hd-interface='terraform'}
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


# Debugging for builds 
{: #troubleshoot-build}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} builds.
{: shortdesc}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

When your build isn't behaving as expected, looking at logs and system events can provide information that might help you debug the problem. 

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

mybuildrun-zg5rj-pod-z5gzb/step-git-source-source-r9fcf:
{"level":"info","ts":1614363665.8331757,"caller":"git/git.go:169","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 8b514ce871e50d67cfea3e344b90cade4bd26e90 (grafted, HEAD, origin/main) in path /workspace/source"}
{"level":"info","ts":1614363666.82988,"caller":"git/git.go:207","msg":"Successfully initialized and updated submodules in path /workspace/source"}

mybuildrun-zg5rj-pod-z5gzb/step-build-and-push:
INFO[0002] Retrieving image manifest node:12-alpine
INFO[0002] Retrieving image node:12-alpine
INFO[0003] Retrieving image manifest node:12-alpine
INFO[0003] Retrieving image node:12-alpine
INFO[0003] Built cross stage deps: map[]
INFO[0003] Retrieving image manifest node:12-alpine
INFO[0003] Retrieving image node:12-alpine
INFO[0004] Retrieving image manifest node:12-alpine
INFO[0004] Retrieving image node:12-alpine
INFO[0004] Executing 0 build triggers
INFO[0004] Unpacking rootfs as cmd RUN npm install requires it.
INFO[0008] RUN npm install
INFO[0008] Taking snapshot of full filesystem...
INFO[0010] cmd: /bin/sh
INFO[0010] args: [-c npm install]
INFO[0010] Running: [/bin/sh -c npm install]
npm WARN saveError ENOENT: no such file or directory, open '/package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open '/package.json'
npm WARN !invalid#2 No description
npm WARN !invalid#2 No repository field.
npm WARN !invalid#2 No README data
npm WARN !invalid#2 No license field.

up to date in 0.267s
found 0 vulnerabilities

INFO[0011] Taking snapshot of full filesystem...
INFO[0011] COPY server.js .
INFO[0011] Taking snapshot of files...
INFO[0011] EXPOSE 8080
INFO[0011] cmd: EXPOSE
INFO[0011] Adding exposed port: 8080/tcp
INFO[0011] CMD [ "node", "server.js" ]

mybuildrun-zg5rj-pod-z5gzb/step-image-digest-exporter-ngl6j:
2021/02/26 18:21:02 warning: unsuccessful cred copy: ".docker" from "/tekton/creds" to "/tekton/home": unable to open destination: open /tekton/home/.docker/config.json: permission denied
{"severity":"INFO","timestamp":"2021-02-26T18:21:26.372494581Z","caller":"logging/config.go:116","message":"Successfully created the logger."}
{"severity":"INFO","timestamp":"2021-02-26T18:21:26.372621756Z","caller":"logging/config.go:117","message":"Logging level set to: info"}
```
{: screen}

## Getting system event information for my builds
{: #ts-build-gettingevent}

System event information can be helpful to troubleshoot problems when you run builds. You can view system event information for builds with the CLI. 
{: shortdesc}

1. Use the [**`ibmcloud ce buildrun list`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-list) command to list all of your build runs in a project; for example,
 
     ```
    ibmcloud ce build run list  
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

3. Display the system events of instances of your app. 

  * To display the events of a specific instance of your app, use the [**`ibmcloud ce buildrun events --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-events) command; for example,
  
    ```
    ibmcloud ce buildrun events --buildrun mybuildrun 
    ```
    {: pre} 
      
    **Example output** 

    ```
    Getting build run 'mybuildrun'...
    Getting instances of build run 'mybuildrun'...
    Getting events for build run 'mybuildrun'...
    OK

    mybuildrun-nc9vg-pod-tqt6t:
    Type    Reason     Age    Source                  Messages
    Normal  Scheduled  2m19s  default-scheduler       Successfully assigned 8aaon2dfwa0/mybuildrun-nc9vg-pod-tqt6t to 10.240.128.61
    Normal  Pulled     2m17s  kubelet, 10.240.128.61  Container image "icr.io/obs/codeengine/tekton-pipeline/entrypoint-bff0a22da108bc2f16c818c97641a296:v0.23.0-rc5@sha256:deca8166d630a19988e38058431017c329496ed147295f1fc2c337d754b8aa43" already present on machine
    Normal  Created    2m16s  kubelet, 10.240.128.61  Created container place-tools
    Normal  Started    2m16s  kubelet, 10.240.128.61  Started container place-tools
    Normal  Pulled     2m15s  kubelet, 10.240.128.61  Container image "icr.io/obs/codeengine/git:v0.8.100" already present on machine
    Normal  Created    2m15s  kubelet, 10.240.128.61  Created container step-source-default
    Normal  Started    2m15s  kubelet, 10.240.128.61  Started container step-source-default
    Normal  Pulled     2m15s  kubelet, 10.240.128.61  Container image "icr.io/obs/codeengine/kaniko/executor:v1.6.0-rc1" already present on machine
    Normal  Created    2m15s  kubelet, 10.240.128.61  Created container step-build-and-push
    Normal  Started    2m14s  kubelet, 10.240.128.61  Started container step-build-and-push
      [...]
    ```
    {: screen}

