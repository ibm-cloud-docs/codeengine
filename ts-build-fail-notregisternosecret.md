---

copyright:
  years: 2020, 2023
lastupdated: "2023-03-09"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Build fails when the build did not register correctly and a secret does not exist
{: #ts-build-notreg-nosecret}
{: troubleshoot}

After you create and run a build, your build does not complete successfully and you receive a message that the build is not registered correctly and a secret does not exist. 
{: tsSymptoms}

If you receive a message that the build is not registered correctly and a secret does not exist, then the `BUILD_NAME` build was not correctly defined.
{: tsCauses}

Example error message 

```txt
The Build is not registered correctly, build: <BUILD_NAME>, registered status: False, reason: SpecSourceSecretNotFound|SpecOutputSecretRefNotFound|MultipleSecretRefNotFound
```
{: screen}

The `BUILD_NAME` build references a secret that does not exist. If the reason is `SpecOutputSecretRefNotFound`, then a registry secret does not exist. If it is `SpecSourceSecretNotFound`, then a secret to access the Git repository is missing. The reason is `MultipleSecretRefNotFound` if both secrets do not exist. Correct the build to reference existing secrets.


Try using the following information to resolve your problem.
{: tsResolve}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

Take the following steps to help you resolve the problem with your build.

1. Check your secrets. In a build, secrets are used for the following purposes:
    * To authenticate at the container registry. A registry secret stores credentials to access a container registry. To list all secrets in your project, including existing registry secrets, run the [**`ibmcloud ce secret list`**](/docs/codeengine?topic=codeengine-cli#cli-secret-list) command. To create a registry secret, run the [**`ibmcloud ce secret create --format registry`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. For more information about registry secrets, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).
    * To authenticate at a private source code repository. An SSH secret stores credentials to authenticate to a service with an SSH key, such as authenticating to a Git repository, such as GitHub or GitLab. To list all secrets in your project, including existing SSH secrets, run the [**`ibmcloud ce secret list`**](/docs/codeengine?topic=codeengine-cli#cli-secret-list) command. To create an SSH secret, run the [**`ibmcloud ce secret create --format ssh`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) command. For more information about SSH secrets to access repositories, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

2. After secrets are defined, use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration. If you are referencing an registry secret, specify the name of the secret by using the `--registry-secret` option with the **`build update`** command. If you are referencing an SSH secret to access a private repository that contains the source code to build your container image, specify the `--git-repo-secret` option with the **`build update`** command. For example,

    ```txt
    ibmcloud ce build update --name <BUILD_NAME> [--registry-secret <REGISTRY_ACCESS_SECRET>] [--git-repo-secret <GIT_REPO_SECRET>] 
    ```
    {: pre}

3. Use the  [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```txt
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}



