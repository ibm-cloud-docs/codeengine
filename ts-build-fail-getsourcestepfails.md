---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-02"

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


# Build fails in the source step
{: #ts-build-gitsource-stepfail}
{: troubleshoot}

{: tsSymptoms}
After you create and run a build, your build does not complete successfully and you receive a message that the build fails in the source step.

{: tsCauses}
If you receive a message that source step fails during a build, then check the logs of the build to determine the root cause of the problem. 

**Example error message** 

```
Summary:  Failed to execute build run
Status:   Failed
Reason:   buildrun step step-source-default failed in pod <BUILDRUN_NAME>-zvcc9-pod-trsq2, for detailed information: ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: screen}

Run the [**`ibmcloud ce buildrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command. Focus on the logs for the failed step,

```
ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: pre}

```
[...]

<BUILDRUN_NAME>-zvcc9-pod-trsq2/step-source-default:
{"level":"info","ts":1625217529.370393,"logger":"git","msg":"ssh","path":"/usr/bin/ssh","version":"OpenSSH_8.0p1, OpenSSL 1.1.1g FIPS  21 Apr 2020"}
{"level":"info","ts":1625217529.3847454,"logger":"git","msg":"git","path":"/usr/bin/git","version":"git version 2.27.0"}
{"level":"info","ts":1625217529.3940003,"logger":"git","msg":"git-lfs","path":"/usr/bin/git-lfs","version":"git-lfs/2.11.0 (GitHub; linux amd64; go 1.14.4)"}
{"level":"debug","ts":1625217529.3940916,"logger":"git","msg":"/usr/bin/git clone --quiet --no-tags --branch main --depth 1 --single-branch -- https://github.com/IBM/CodeEngineX /workspace/source"}
{"level":"error","ts":1625217529.58695,"logger":"git","msg":"git command failed","command":"/usr/bin/git clone --quiet --no-tags --branch main --depth 1 --single-branch -- https://github.com/IBM/CodeEngineX /workspace/source","output":"fatal: could not read Username for 'https://github.com': terminal prompts disabled","error":"fatal: could not read Username for 'https://github.com': terminal prompts disabled (exit code 128)","stacktrace":"main.git\n\tgithub.com/shipwright-io/build/cmd/git/main.go:324\nmain.clone\n\tgithub.com/shipwright-io/build/cmd/git/main.go:277\nmain.runGitClone\n\tgithub.com/shipwright-io/build/cmd/git/main.go:115\nmain.Execute\n\tgithub.com/shipwright-io/build/cmd/git/main.go:98\nmain.checkAndRun\n\tgithub.com/shipwright-io/build/cmd/git/main.go:90\nmain.main\n\tgithub.com/shipwright-io/build/cmd/git/main.go:70\nruntime.main\n\truntime/proc.go:204"}
{"level":"error","ts":1625217529.587297,"logger":"git","msg":"program failed with an error","error":"fatal: could not read Username for 'https://github.com': terminal prompts disabled (exit code 128)","stacktrace":"main.Execute\n\tgithub.com/shipwright-io/build/cmd/git/main.go:100\nmain.checkAndRun\n\tgithub.com/shipwright-io/build/cmd/git/main.go:90\nmain.main\n\tgithub.com/shipwright-io/build/cmd/git/main.go:70\nruntime.main\n\truntime/proc.go:204"}
[...] 
```
{: screen}
<br />

The error text is different based on what went wrong. The following table describes error text and potential root causes for this scenario.

| Error message contains | Potential root causes |
| --------- | -------- |
| <code>terminal prompts disabled</code> | <ul><li>The repository does not exist.</li><li>The source URL was provided by using HTTPS protocol, but the repository is private and therefore requires the SSH protocol. The wrong protocol was used.</li></ul>|
| <code>Host key verification failed</code>  | <ul><li>The source URL was provided by using SSH protocol, but no secret was provided. The wrong protocol was used or a secret is missing or incorrect.</li></ul> |
| <code>Permission denied (publickey)</code>  | <ul><li>The source URL was provided by using SSH protocol, but a secret is missing or incorrect.</li></ul> |
| <code>Couldn't find remote ref</code> | <ul><li>The revision (branch name, tag name, commit ID) specified in the build does not exist.</li></ul> |
{: caption="Error text and root cases for Git source failed step."}

<br />

{: tsResolve}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

After you check the logs and identify potential root causes, use the following resolution actions to help you resolve the problem. 

## Resolution for a non-existent repository during build
{: #ts-build-noexistrepo}

Use the following commands to update the existing build to reference your Git repository source and submit the build run.

1. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration; for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> 
    ```
    {: pre}
     
2. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

## Resolution for a wrong protocol or missing secret during build
{: #ts-build-wrongprotocol}

The URL to a Git repository can be specified by using either the HTTPS or SSH protocol. GitHub and GitLab provide a way to toggle the URL format in the Git UI. The HTTPS protocol requires no authentication but can be used only if the repository is public. For private repositories, you must use the SSH protocol and provide a secret for the repository. Repositories in a GitHub Enterprise setup can be public but still require authentication, and those GitHub Enterprise repositories can also be used only by using SSH protocol.

### For public repositories
{: #ts-build-wrongprotocol-public}

<br />
If the failure happened for a public repository, then update the existing build to use the HTTPS URL of the Git repository, and run the build.

1. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the HTTPS URL of the Git repository; for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> 
    ```
    {: pre}
     
2. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

### For private repositories
{: #ts-build-wrongprotocol-private}

<br />
If the failure happened for a private repository, then create a Git repository access secret and use the SSH protocol. The Git repository access secret contains a private key while the corresponding public key is stored with your Git repository provider. For more information about creating a key pair and store the public part in GitHub or GitLab, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories). It is important that your private key file is not encrypted with a passphrase before you can upload it to {{site.data.keyword.codeengineshort}}. The format of the private key file can vary, which makes it complicated to assess if the file is encrypted. Depending on the version of the `ssh-keygen` tool that was used to create the key pair, the file might have one of the following headers:

- If the file starts with `-----BEGIN RSA PRIVATE KEY-----`, then it uses the PEM format and was created with an older version of `ssh-keygen`. If the file is encrypted with a passphrase, then it typically contains a line like this: `Proc-Type: 4,ENCRYPTED`.

- If the file starts with `-----BEGIN OPENSSH PRIVATE KEY-----`, then it was created with a newer version of `ssh-keygen`. To verify whether it is encrypted with a passphrase, run the following command:

  ```
  ssh-keygen -p -f <ID_FILE>
    Enter old passphrase:
  ```
  {: codeblock}
  
  ```
  ssh-keygen -p -f <ID_FILE>
    Key has comment '<COMMENT>'
    Enter new passphrase (empty for no passphrase): 
  ```
  {: codeblock}
  
  You can escape the command by using `Ctrl+C`. If the command requires the old passphrase (first example), then the original file was encrypted, otherwise it directly asks for the passphrase of the new file (second example).
  
  To decrypt an encrypted private key file, run the following command and leave the new passphrase empty.

  ```
  $ ssh-keygen -p -f <ID_FILE>
  
  Enter old passphrase: <PASSPHRASE>
  Key has comment '<COMMENT>'
  Enter new passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved with the new passphrase.
  ```
  {: codeblock}

  This command modifies the private key file. If you need to retain your encrypted version, create a copy first.
  {: note}

To create a Git repository access secret and use the SSH protocol,

1. Run the [**`ibmcloud ce repo create`**](/docs/codeengine?topic=codeengine-cli#cli-repo-create) command. The `SSH_KEY_PATH` needs to point to the private key file that matches the public key in your account or the deployment key in the repository. The `GIT_REPO_HOST` is the host of your Git repository, for example `github.com` or `gitlab.com`. For more information, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

    ```
    ibmcloud ce repo create --name <GIT_REPO_SECRET> --key-path <SSH_KEY_PATH> --host <GIT_REPO_HOST>
    ```
    {: pre}

2. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use the SSH URL of the Git repository and reference the Git repository access secret. For example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --source <GIT_REPO> --git-repo-secret <GIT_REPO_SECRET>
    ```
    {: pre}

    In the prior example, specify the SSH URL by using the `git@` prefix for your source, such as `--source git@github.com:IBM/CodeEngine.git`.

## Resolution for a wrong revision during build
{: #ts-build-wrongrevision}

A build configuration specifies the source repository by using its URL and optionally a revision. The revision can be either the name of a branch or tag, or a commit identifier. By default, the `main` branch is built. Review the error message for information about something that was specified but does not exist.

1. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use a correct revision (or commit); for example,

    ```
    ibmcloud ce build update --name <BUILD_NAME> --commit <COMMIT> 
    ```
    {: pre}

2. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}

