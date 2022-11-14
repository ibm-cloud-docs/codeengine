---

copyright:
  years: 2022
lastupdated: "2022-11-14"

keywords: repository access for code engine, source code access for code engine, access to source code in code engine, access keys in code engine, ssh key access in code engine, github repo access in code engine, gitlab repo access in code engine, code repository access for code engine, code repositories, Git repository access secret, code repository, private git repository, private repository

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Accessing private code repositories
{: #code-repositories}

A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build.
{: shortdesc}

After you create access to your private code repository, you can pull code from repo, build it, and deploy an app or job with {{site.data.keyword.codeenginefull}}. 

## Create code repository access
{: #create-code-repo}

When you create access to a private code repository, you are saving credentials in {{site.data.keyword.codeengineshort}}. In the console, these credentials are called *Code repo access*. In the CLI, these credentials are called *Git repository access secrets*.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Choose an SSH key to use](#choose-ssh-key).

### Choosing an SSH key for code repository
{: #choose-ssh-key}

For both GitHub and GitLab, you can decide between two kinds of SSH keys to connect to your source repository.

1. An SSH key associated with the source code repository, this key has access to only those repositories where you register the SSH key. This access is read only, by default, which is the level that is required by {{site.data.keyword.codeengineshort}} to download the source code. You can select write access, if needed. Consider choosing this option to set an SSH key that is scoped to specific repositories to control access to only the specified repositories.  
    - [GitHub - Deployment keys](https://docs.github.com/en/developers/overview/managing-deploy-keys#deploy-keys){: external}
    - [GitLab - Deployment keys](https://docs.gitlab.com/ee/user/project/deploy_keys/){: external}

2. An SSH key associated with a user, for example, your own user account or a functional ID that is available in your organization. This SSH key has the repository permissions from the user account. {{site.data.keyword.codeengineshort}} requires read access to download the source code.

    Because setting an SSH key that is scoped to a user account provides access to the full account, it is important to be aware of security implications when you choose this option.
    {: important}

    - [Adding an SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account){: external}.
    - [Adding an SSH key to your GitLab account](https://docs.gitlab.com/ee/user/ssh){: external}.

Do not create your SSH key file with a secure passphrase as this action causes your `build` command to fail.
{: tip}

### Adding private repository access from the console
{: #add-repo-access-ce-console}

To add private repository access from the console,

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Code repo access**.
4. Click **Create**.
5. Specify a name, Code repo server, and the [SSH key](#choose-ssh-key).

You can create access when you build an image.
{: tip}

### Creating a Git repository access secret with the CLI
{: #create-code-repo-console}

To create a Git repository access secret with the CLI, use the **`repo create`** command. This command requires a name, a key path, and the address of the Git repository host and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce repo create`**](/docs/codeengine?topic=codeengine-cli#cli-repo-create) command. 
{: shortdesc}

For example, the following **`repo create`** command creates a Git repository access secret that is called `myrepo` to a repository at `github.com` that uses your personal SSH private key that is found at the default location on your system.

Mac OS or Linux&reg;

```txt
ibmcloud ce repo create --name myrepo --key-path $HOME/.ssh/id_rsa --host github.com --known-hosts-path $HOME/.ssh/known_hosts
```
{: pre}

Windows

```txt
ibmcloud ce repo create --name myrepo --key-path "%HOMEPATH%\.ssh\id_rsa" --host github.com --known-hosts-path "%HOMEPATH%\.ssh\known_hosts"
```
{: pre}

The following table summarizes the options that are used with the **`repo create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce repo create`**](/docs/codeengine?topic=codeengine-cli#cli-repo-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the Git repository access secret. Use a name that is unique within the project. This value is required.  \n - The name must begin and end with a lowercase alphanumeric character.  \n - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-). |
| `--key-path` | The local path to the unencrypted private SSH key. If you use your personal private SSH key, then this file is usually at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa`(Windows). This value is required. |
| `--host` | The Git repository hostname; for example, `github.com`. This value is required. |
| `--known-hosts-path` | The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). |
{: caption="Table 1. repo create command components" caption-side="top"}


## Referencing a private Git repository in a build
{: #referencing-coderepo-build}

You can reference existing access or create access when you build an image from the console.

### Referencing a private Git repository in a build from the console
{: #referencing-coderepo-build-ui}

To reference your private Git repository in a build,

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Image builds**.
4. Click **Create**.
5. To specify a private repository and add access, enter the URL to the repository in the **Code repo URL** field and then select either your existing code repo access or to [create access](#add-repo-access-ce-console).
6. Finish specifying information for your build and click **Done**.

For more information about building images, see [Building a container image](/docs/codeengine?topic=codeengine-build-image).

### Referencing the Git repository access secret in a build with the CLI
{: #referencing-coderepo}

To use the Git repository access secret in a build, use the `--git-repo-secret` option when you run the **`build create`** or the **`build update`** command.  

If you have an existing build, then you can update it by using the [**`build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command,

```txt
ibmcloud ce build update --name mybuild --git-repo-secret myrepo
```
{: pre}

If you want to create a new build, then see [Creating a build configuration with the CLI](/docs/codeengine?topic=codeengine-build-image#build-create-cli).

## Next steps for Git repository access secret
{: #nextsteps-coderepo}

After you create your Git repository access secret, you can [build images](/docs/codeengine?topic=codeengine-plan-build) from source code in your private repository. Specify your Git repository access secret when you run the **`build create`** command.


