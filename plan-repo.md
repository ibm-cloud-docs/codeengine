---

copyright:
  years: 2023
lastupdated: "2023-09-06"

keywords: repository access for code engine, source code access for code engine, access to source code in code engine, access keys in code engine, ssh key access in code engine, github repo access in code engine, gitlab repo access in code engine, code repository access for code engine, code repositories, Git repository access secret, code repository, private git repository, private repository, SSH secret

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

When you create access to a private code repository, you are saving credentials in {{site.data.keyword.codeengineshort}}. In the console, these credentials are called *Code repo access*. In the CLI, these credentials are called *SSH secrets*.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Choose an SSH key to use](#choose-ssh-key).

### Choosing an SSH key for code repository
{: #choose-ssh-key}

For both GitHub and GitLab, you can decide between two kinds of SSH keys to connect to your source repository.

1. An SSH key associated with the source code repository, this key has access to only those repositories where you register the SSH key. This access is read only, by default, which is the level that is required by {{site.data.keyword.codeengineshort}} to download the source code. You can select write access, if needed. Consider choosing this option to set an SSH key that is scoped to specific repositories to control access to only the specified repositories.  
    - [GitHub - Deployment keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys){: external}
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

### Adding private repository access with the CLI
{: #create-code-repo-console}

Beginning with CLI version 1.42.0, defining and working with secrets in the CLI is unified under the **`secret`** command group. See [**`ibmcloud ce secret`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) commands. Use the `--format` option to specify the category of secret, such as `basic_auth`, `generic`, `ssh`, `tls`, or `registry`. While you can continue to use the **`repo`** command group, take advantage of the unified **`secret`** command group. To create a secret to access a service with an SSH key, such as to authenticate to a Git repository like GitHub or GitLab, use the [**`ibmcloud ce secret create --format ssh`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. An SSH secret is also used as a Git repository access secret. To learn more about working with secrets in {{site.data.keyword.codeengineshort}}, see [Working with secrets](/docs/codeengine?topic=codeengine-secret).
{: important}


An SSH secret contains the credentials to access the private repository that contains the source code to build your container image. An SSH secret is also used as a Git repository access secret.

To create an SSH secret with the CLI, use the **`secret create --format ssh`** command. This command requires a name and a key path, and also allows other optional arguments such as the path to the known hosts file. For a complete listing of options, see the [**`ibmcloud ce secret create --format ssh`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. 

For example, the following command creates an SSH secret that is called `myrepossh` to a repository at `github.com` that uses your personal SSH private key that is found at the default location on your system.

Mac OS or Linux&reg;

```txt
ibmcloud ce secret create --format ssh --name myrepossh --key-path $HOME/.ssh/id_rsa --known-hosts-path $HOME/.ssh/known_hosts
```
{: pre}

Windows

```txt
ibmcloud ce secret create --format ssh --name myrepossh --key-path "%HOMEPATH%\.ssh\id_rsa" --known-hosts-path "%HOMEPATH%\.ssh\known_hosts"
```
{: pre}

The following table summarizes the options that are used with the **`repo create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce repo create`**](/docs/codeengine?topic=codeengine-cli#cli-repo-create) command.


| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the SSH secret. Use a name that is unique within the project. This value is required.  \n - The name must begin and end with a lowercase alphanumeric character.  \n - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-). |
| `--key-path` | The local path to the unencrypted private SSH key. If you use your personal private SSH key, then this file is usually at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa`(Windows). This value is required. |
| `--known-hosts-path` | The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). |
{: caption="Table 1. Command description" caption-side="bottom"}


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

### Referencing an SSH secret in a build with the CLI
{: #referencing-coderepo}

To use an SSH secret in a build, use the `--git-repo-secret` option when you run the **`build create`** or the **`build update`** command. An SSH secret is also used as a Git repository access secret. 

If you have an existing build, then you can update it by using the [**`build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command,

```txt
ibmcloud ce build update --name mybuild --git-repo-secret myrepossh
```
{: pre}

If you want to create a new build, then see [Creating a build configuration with the CLI](/docs/codeengine?topic=codeengine-build-create-config1#build-create-cli).

## Next steps for Git repository access 
{: #nextsteps-coderepo}

After you create your SSH secret to access a Git repository, you can [build images](/docs/codeengine?topic=codeengine-plan-build) from source code in your private repository. Specify your SSH secret when you run the **`build create`** command with the `--git-repo-secret` option.


