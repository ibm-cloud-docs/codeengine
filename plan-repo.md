---

copyright:
  years: 2020
lastupdated: "2020-09-14"

keywords: repository, code engine, source code

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


# Accessing private code repositories
{: #code-repositories}

Code repositories, such as GitHub, store your source code that you can build into images. If your code repository is public, you do not need to do anything else, simply provide the URL using the HTTPS protocol when you create your image build. However, if your code repository is private, you must create access.
{: shortdesc}

## Create code repository access
{: #create-code-repo}

**Before you begin**

- Create a project
- Decide on the SSH key to use

### Choosing an SSH key

For both GitHub as well as GitLab, you can decide between two kinds of SSH keys to connect to your source repository:

1. An SSH key associated with a user, for example your own user account or a functional ID that is available in your organization. This SSH key has the repository permissions from the user account. {{site.data.keyword.codeengineshort}} only requires read access to download the source code. For more information about setting up this type of SSH key:
   - [Adding a new SSH key to your GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account){: external}
   - [Adding an SSH key to your GitLab account](https://docs.gitlab.com/ee/ssh/#adding-an-ssh-key-to-your-gitlab-account){: external}
   
2. An SSH key associated with the source code repository, this key has access to only those repositories where you register the SSH key. It usually has only read access, which is enough for {{site.data.keyword.codeengineshort}} to download the source code. For more information, see the documentation about setting up an SSH:
   - [GitHub - Deploy keys](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys){: external}
   - [GitLab - Deploy keys](https://docs.gitlab.com/ee/user/project/deploy_keys/){: external}

### Creating code repository access with the CLI
{: #create-code-repo-console}

To create access to a private code reponsitory with the CLI, use the `repo create` command.

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
   <td>The command to create your respository access.</td>
   </tr>
   <tr>
   <td><code>--name</code></td>
   <td>The name of the repo access secret. Use a name that is unique within the project. This value is required.
     <ul>
     <li>The name must begin and end with a lowercase alphanumeric character.</li>
     <li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
     </ul>
   </td>
   </tr>
   <tr>
   <td><code>--key-path</code></td>
   <td>The local path to the private SSH key. If you use your personal private SSH key, then this file is usually located at `$HOME/.ssh/id_rsa`</td>
   </tr>
      <tr>
   <td><code>--host</code></td>
   <td>The address of the host, for example `github.com`.</td>
   </tr>
   <tr>
   <td><code>--known-hosts-path</code></td>
   <td>The local path to your SSH known hosts file. This file is usually located at `$HOME/.ssh/known_hosts`. Specifying this file ensures that your authentication is only used for a server with the same identity that you connected to from your machine.</td>
   </tr>
   </tbody></table>
   
   For example, create access called `myrepo` to a repository at `github.com` that uses your personal SSH private key, located at the default location on your system.
   
```
ibmcloud ce repo create --name myrepo --key-path $HOME/.ssh/id_rsa --host github.com
```
{: pre}

After you create your access, you can [build images](/docs/codeengine?topic=codeengine-plan-build) from your source code in your private repository.
