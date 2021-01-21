---

copyright:
  years: 2021
lastupdated: "2021-01-21"

keywords: repository access for code engine, source code access for code engine, access to source code in code engine, access keys in code engine, ssh key access in code engine, github repo access in code engine, gitlap repo access in code engine, code repository  access for code engine

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


# Accessing private code repositories
{: #code-repositories}

A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build.
{: shortdesc}

After you create access to your private code repository, you can pull code from repo, build it, and deploy an app or job with {{site.data.keyword.codeengineshort}}. 

## Create code repository access
{: #create-code-repo}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Choose an SSH key to use](#choose-ssh-key).

### Choosing an SSH key
{: #choose-ssh-key}

For both GitHub as well as GitLab, you can decide between two kinds of SSH keys to connect to your source repository.

1. An SSH key associated with a user, for example, your own user account or a functional ID that is available in your organization. This SSH key has the repository permissions from the user account. {{site.data.keyword.codeengineshort}} requires read access to download the source code. For more information about setting up this type of SSH key.
   - [Adding an SSH key to your GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account){: external}.
   - [Adding an SSH key to your GitLab account](https://docs.gitlab.com/ee/ssh/#adding-an-ssh-key-to-your-gitlab-account){: external}.
   
2. An SSH key associated with the source code repository, this key has access to only those repositories where you register the SSH key. This access is read only, which is the level that is required by {{site.data.keyword.codeengineshort}} to download the source code. For more information, see the documentation about setting up a deployment key. 
   - [GitHub - Deployment keys](https://docs.github.com/en/developers/overview/managing-deploy-keys){: external}
   - [GitLab - Deployment keys](https://docs.gitlab.com/ee/user/project/deploy_keys/){: external}
   
Do not create your SSH key file with a secure passphrase as this action causes your `build` command to fail.
{: tip}

### Creating a Git repository access secret with the CLI
{: #create-code-repo-console}

To create a Git repository access secret with the CLI, use the `repo create` command.

```
ibmcloud ce repo create --name REPO_NAME --key-path SSH_KEY_PATH --host HOST_ADDRESS [--known-hosts-path KNOWN_HOSTS_PATH]
```
{: pre}
<table>
  <caption><code>repo create</code> command components</caption>
   <thead>
    <col width="25%">
    <col width="75%">
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>repo create</code></td>
   <td>The command to create your Git repository access secret.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the Git repository access secret. Use a name that is unique within the project. This value is required.
     <ul>
     <li>The name must begin and end with a lowercase alphanumeric character.</li>
     <li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   <tr>
   <td><code>--key-path</code></td>
   <td>The local path to the unencrypted private SSH key. If you use your personal private SSH key, then this file is usually located at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa` (Windows).</td>
   </tr>
      <tr>
   <td><code>--host</code></td>
   <td>The Git repository hostname; for example, `github.com`.</td>
   </tr>
   <tr>
   <td><code>--known-hosts-path</code></td>
   <td>The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). </td>
   </tr>
   </tbody></table>
   
   For example, create a Git repository access secret that is called `myrepo` to a repository at `github.com` that uses your personal SSH private key that is found at the default location on your system.

   Mac OS or Linux:
   
   ```
   ibmcloud ce repo create --name myrepo --key-path $HOME/.ssh/id_rsa --host github.com --known-hosts-path $HOME/.ssh/known_hosts
   ```
   {: pre}

   Windows: 
   
   ```
   ibmcloud ce repo create --name myrepo --key-path "%HOMEPATH%\.ssh\id_rsa" --host github.com --known-hosts-path "%HOMEPATH%\.ssh\known_hosts"
   ```
   {: pre}

## Next steps

After you create your Git repository access secret, you can [build images](/docs/codeengine?topic=codeengine-plan-build) from source code in your private repository. Specify your Git repository access secret when you run the `build create` command.
