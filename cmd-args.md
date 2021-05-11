---

copyright:
  years: 2021
lastupdated: "2021-05-11"

keywords: commands, arguments, cmd, workloads, application, job

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


# Defining commands and arguments for your workloads
{: #cmd-args}

When you create a container image for your {{site.data.keyword.codeenginefull}} workloads, you can define commands and arguments for your job or application to use at run time.
{: shortdesc}

Container images include two pieces of metadata that tell the container runtime what command, inside the image to run when the container is created. These metadata fields are called `Entrypoint` and `Command`. For those users who are familiar with Dockerfile, the fields equate to the `ENTRYPOINT` and `CMD` commands. These two fields contain arrays of strings that are combined to create the command line that is used when you run your container. 

For example, if your container image has an `Entrypoint` value of `/myapp` and a `Command` value of `--debug`, then the full command that is run is `/myapp --debug` (an array of two strings). Notice that because this action is a concatenation of two arrays, if `Entrypoint` is an empty array then the `Command` array's first array element is the executable that is run in your container.

When you create a {{site.data.keyword.codeengineshort}} application or job, you can provide values for both the `Entrypoint` and `Command` arrays. 

| Description	| Docker name	| {{site.data.keyword.codeengineshort}} name |
| ---------- |  ------ | ------ | 
| The command that is run by the container. | entrypoint |	command |
| The arguments that are passed to the command.	| `cmd`	| `args` |
{: caption="`cmd` and `args` names" caption-side="top"}

- If `--command` is used, then any image `Entrypoint` value is overwritten and any image `cmd` values are ignored.
- If `--argument` is used, then any image `Command` value in overwritten.

To better understand this process, let's look at a few examples,

| Image `Entrypoint` | Image `Cmd` |	{{site.data.keyword.codeengineshort}} `command` |	{{site.data.keyword.codeengineshort}} `args` |	Command that is run |
| ------ |  ------ | ------ | ------ | ------ |
| `/myapp` |	`--debug` |	`<not set>` |	`<not set>` |	`/myapp --debug` |
| `/myapp` |	`--debug` |	`/myapp2` |	`<not set>` |	`/myapp` |
| `/myapp` |	`--debug` |	`<not set>` |	`-d` |	`/myapp -d` |
| `/myapp` |	`--debug` |	`/myapp2` |	`-d` |	`/myapp2 -d` |
{: caption=" Command and `args` examples" caption-side="top"}

You can specify these values by using the `--command` and `--argument` options in the CLI for apps and jobs and the `Command` and `Arguments` entry boxes in the console for jobs. For more information, see [Deploying your app with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args) and [Running your job with commands and arguments](/docs/codeengine?topic=codeengine-job-deploy#job-cmd-args).
