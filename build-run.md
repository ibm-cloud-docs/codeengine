---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-11"

keywords: code engine, build, buildrun, running a build, building from source code

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Running a build configuration
{: #build-run}

After you create a build configuration, you can submit a run based on that build configuration. Run your build from the console or with the CLI.
{: shortdesc}

{{site.data.keyword.codeengineshort}} has quotas for builds and build runs within a project. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
{: important}

Build runs that complete are ultimately automatically deleted. When your build run is based on build configuration, this build run is deleted after 3 hours if the build run is successful. If the build run is not successful, this build run is deleted after 48 hours.  
{: note}

## Running a build from the console
{: #build-run-console}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select the project where you created your build.
3. From the project page, click **Image builds**.
4. From the **Image build** tab, select the name of the image build that you want to work with.
5. In the **Configuration** section, you can review the build configuration and change values, if needed.
6. To submit your build, click **Submit build**.
7. Verify any additional information, such as the **Image tag** to create a specific tag for this build run or overwrite the **Timeout** value.
8. Submit the build run by clicking **Submit build**.

Monitor your build progress in the **Build runs** section.

## Running a build with the CLI for source from a repository (non-local)
{: #build-run-cli}

To submit a build run from a build configuration with the CLI, use the **`buildrun submit`** command. This command requires the name of a build configuration. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.
{: shortdesc} 

The following example runs a build that is called `helloworld-build-run` and uses the `helloworld-build` build.

```txt
ibmcloud ce buildrun submit --build helloworld-build --name helloworld-build-run 
```
{: pre}

Example output

```txt
Submitting build run 'helloworld-build-run'...
Run 'ibmcloud ce buildrun get -n helloworld-build-run' to check the build run status.
OK 
```
{: screen}

The following table summarizes the options that are used with the **`buildrun submit`** command in this example. For more information about the command and its options, see the [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.


| Option | Description |
| --- | --- |
| `--build` | The name of the build configuration to use. This value is required. |
| `--name` | The name of the build run. Use a name that is unique within the project. \n - The name must begin and end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-). |
{: caption="Table 3. Command description" caption-side="bottom"}

Your build runs begins. Monitor the progress by using the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. 

For example, to check the status of the build run from the previous example,

```txt
ibmcloud ce buildrun get --name helloworld-build-run
```
{: pre}

Example output

```txt
Getting build run 'helloworld-build-run'...
[...]
OK

Name:          helloworld-build-run  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           21m  
Created:       2021-03-14T14:50:13-05:00  

Summary:  Succeeded  
Status:   Succeeded  
Reason:   Succeeded
```
{: screen}

For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).


## Running a build with the CLI for source from a local directory (local)
{: #build-run-cli-local}

To submit a build run from a build configuration with the CLI that pulls source from a local directory, use the **`buildrun submit`** command. This command requires the name of a build configuration, and the path to your local source. Other optional arguments can be specified. For a complete listing of options, see the [**`ibmcloud ce buildrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit) command.
{: shortdesc} 

The following scenario clones the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external} into a `CodeEngineLocalSample` directory on your local workstation.

1. Clone the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external} to a subdirectory that is created on your local workstation, such as the `CodeEngineLocalSamples` subdirectory. From this directory, run the `git clone` command; for example,

    ```txt
    git clone https://github.com/IBM/CodeEngine
    ```
    {: pre}

2. Go to the directory where your source code is on your workstation. For example, go to the `CodeEngine` subdirectory where the {{site.data.keyword.codeengineshort}} Samples reside.

3. From the directory where your source code resides, submit the build run. The following example runs a build that is called `buildrun-local-dockerfile`and uses the `build-local-dockerfile` build configuration. The `--source` option specifies the path to the source on the local workstation to the `helloworld` sample.

    ```txt
    ibmcloud ce buildrun submit --name buildrun-local-dockerfile --build build-local-dockerfile --source ./helloworld  
    ```
    {: pre}

    Example output

    ```txt
    Getting build 'build-local-dockerfile'
    Packaging files to upload from source path './helloworld' ...
    Submitting build run 'buildrun-local-dockerfile'...
    Run 'ibmcloud ce buildrun get -n buildrun-local-dockerfile' to check the build run status.
    OK 
    ```
    {: screen}

4. Monitor the progress of your build run by using the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-build-get) command. For example, to check the status of the build run from the previous example,

    ```txt
    ibmcloud ce buildrun get --name helloworld-build-run
    ```
    {: pre}

    Example output

    ```txt
    Getting build run 'buildrun-local-dockerfile'...
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun events -n buildrun-local-dockerfile' to get the system events of the build run.
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce buildrun logs -f -n buildrun-local-dockerfile' to follow the logs of the build run.
    OK

    Name:          buildrun-local-dockerfile
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           40s
    Created:       2022-01-19T12:22:33-05:00

    Summary:       Succeeded
    Status:        Succeeded
    Reason:        All Steps have completed executing
    Source:
      Source Image Digest:  sha256:07159930b5abcf94e1a7451ea18490d4ad1162a77c2b987da5b7493fa1f1e49d
    Image Digest:  sha256:04c7be7db438a41040ea24d646314f1c847c191d88fffdbea6f483fc443c2bbe

    Build Name:    build-local-dockerfile
    Source Image:  us.icr.io/mynamespace/codeengine-build-source
    Image:         us.icr.io/mynamespace/codeengine-build
    Timeout:       10m0s
    ```
    {: screen}

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. After the build run is completed, you can see your built image, such as `codeengine-build`, in the {{site.data.keyword.registrylong_notm}} instance. You can also see a source image with `-source` appended to the name of your build, such as `codeengine-build-source`. You can delete this source image without impact. 
{: note}

For more information about builds, check the [troubleshooting tips](/docs/codeengine?topic=codeengine-troubleshoot-build).
