---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-19"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Build fails when the ephemeral storage limit is exceeded
{: #ts-build-ephemeral-limit}
{: troubleshoot}

After you create and run a build, your build does not complete successfully and you receive a message that the ephemeral storage usage exceeds limits. 
{: tsSymptoms}

If you receive a message that the ephemeral storage limit is exceeded, then your build size is too small.
{: tsCauses}

When a build runs, it needs to load the source code. When you use a Docker build, the base image needs to be downloaded and the necessary steps to build the target image need to be performed. The build run needs disk space for these steps, which is released after the build run is finished. This disk space is called *ephemeral* local storage. Depending on whether you choose a `small`, `medium`, `large`, or `xlarge` size for your build, a maximum amount of ephemeral storage is available to a build run. When the maximum ephemeral storage is reached, the build run is stopped with an error message; for example,

**Example error messages** 

```txt
Summary: Failed to run build due to exceeded ephemeral storage
Reason:  Pod ephemeral local storage usage exceeds the total limit of containers <AMOUNT>.
```
{: screen}

```txt
Summary: Failed to run build due to exceeded ephemeral storage
Reason:  Container <STEP_NAME> exceeded its local ephemeral storage limit <AMOUNT>.
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



