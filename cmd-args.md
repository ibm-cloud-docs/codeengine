---

copyright:
  years: 2022
lastupdated: "2022-11-17"

keywords: commands, arguments, cmd, workloads, application, job

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Defining commands and arguments for your workloads
{: #cmd-args}

When you create a container image for your {{site.data.keyword.codeenginefull}} workloads, you can define commands and arguments for your job or application to use at run time.
{: shortdesc}

Container images include two pieces of metadata that tell the container runtime what command, inside the image to run when the container is created. These metadata fields are called `Entrypoint` and `Command`. For those users who are familiar with Dockerfile, the fields equate to the `ENTRYPOINT` and `CMD` commands. These two fields contain arrays of strings that are combined to create the command line that is used when you run your container. 

For example, if your container image has an `Entrypoint` value of `/myapp` and a `Command` value of `--debug`, then the full command that is run is `/myapp --debug` (an array of two strings). Notice that because this action is a concatenation of two arrays, if `Entrypoint` is an empty array then the `Command` array's first array element is the executable that is run in your container.

When you create a {{site.data.keyword.codeengineshort}} application or job, you can provide values for both the `Entrypoint` and `Command` arrays. 

| Description    | Docker name    | {{site.data.keyword.codeengineshort}} name |
| ---------- |  ------ | ------ | 
| The command that is run by the container. | `ENTRYPOINT` | `command` |
| The arguments that are passed to the command.    | `CMD`    | `args` |
{: caption="Docker and {{site.data.keyword.codeengineshort}} names" caption-side="top"}

- If `--command` is used, then any image `Entrypoint` value is overwritten and any image `cmd` values are ignored.
- If `--argument` is used, then any image `Command` value in overwritten.

To better understand this process, let's look at a few examples,

| Image `Entrypoint` | Image `Cmd` |    {{site.data.keyword.codeengineshort}} `command` |    {{site.data.keyword.codeengineshort}} `args` |    Command that is run |
| ------ |  ------ | ------ | ------ | ------ |
| `/myapp` |    `--debug` |    `<not set>` |    `<not set>` |    `/myapp --debug` |
| `/myapp` |    `--debug` |    `/myapp2` |    `<not set>` |    `/myapp2` |
| `/myapp` |    `--debug` |    `<not set>` |    `-d` |    `/myapp -d` |
| `/myapp` |    `--debug` |    `/myapp2` |    `-d` |    `/myapp2 -d` |
{: caption="Images and {{site.data.keyword.codeengineshort}} examples" caption-side="top"}

You can specify these values by using the `--command` and `--argument` options in the CLI for apps and jobs and the `Command` and `Arguments` entry boxes in the console for jobs. For more information, see [Deploying your app with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args) and [Running your job with commands and arguments](/docs/codeengine?topic=codeengine-job-plan#job-cmd-args).


