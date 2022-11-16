---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-16"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Build fails when the memory limit is exceeded
{: #ts-build-memory-limit}
{: troubleshoot}

After you create and run a build, your build does not complete successfully and you receive a message that the memory limit is exceeded.
{: tsSymptoms} 

If you receive a message that the memory limit is exceeded, then your build size is too small.
{: tsCauses}

When a build runs, it is running steps, which include code compilations or container image packaging. These steps require memory. Depending on whether you choose a `small`, `medium`, `large`, or `xlarge` size for your build, a maximum amount of memory is available to a build run. When the maximum memory is reached, the build run is stopped with an error message; for example,

Example error message 

```txt
Summary: Failed
Reason:  OOMKilled
```
{: screen}

Try using the following information to resolve your problem.
{: tsResolve}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

To resolve this problem, use a larger size for the build. 

A larger build size also means that more memory and CPU cores are assigned to the build runs. Increasing this size will probably speed up the build runs, but also increases their cost.
{: important}

For more information about build sizes, see [Determining build sizes](/docs/codeengine?topic=codeengine-plan-build#build-size).

1. Use the [**`ibmcloud ce build update`**](/docs/codeengine?topic=codeengine-cli#cli-build-update) command to update the build configuration to use a larger size; for example,

    ```txt
    ibmcloud ce build update --name <BUILD_NAME> --size <SIZE>
    ```
    {: pre}

2. Use the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command to submit a new build run. For the **`buildrun submit`** command, you must specify the `--build` option to provide the name of your build configuration. You can optionally specify the `--name` option to provide the name for this build run. If you specify the `--name` option, make sure that you use a different build run name from the failed build run, or ensure that you delete the failed build run by using the [**`ibmcloud ce buildrun delete`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete) command. For example,

    ```txt
    ibmcloud ce buildrun submit --build <BUILD_NAME> --name <BUILDRUN_NAME>
    ```
    {: pre}



