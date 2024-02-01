---

copyright:
  years: 2020, 2024
lastupdated: "2024-02-01"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging builds 
{: #troubleshoot-build}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} builds and runs of your build.
{: shortdesc}

Whether you are running your build in the console or in the CLI, use the CLI for troubleshooting problems with your build.
1. Run the `ibmcloud ce buildrun get --name BUILDRUN_NAME` command to display the details of your build run.
2. Review the `Reason` in the command output.
{: note}  

When your build isn't behaving as expected, looking at logs and system events can provide information that might help you debug the problem. 

## Build limits to consider 
{: #ts-build-limits}

The maximum number of build configurations that you can have per project is 100. You are limited to a total of 100 build runs per project before you need to remove or clean up old ones.

For more information about limits for builds including memory and CPU, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

With the CLI, you can use the [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to display information about limits and current usage. For example,

```txt
ibmcloud ce project create --name myproject  
```
{: pre}

Example output

```txt 
Getting project 'myproject'...
OK

Name:                                      myproject  
ID:                         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:                                    active  
Enabled:                                   true  
Application Private Visibility Supported:  true  
Selected:                                  true  
Region:                                    us-south 
Resource Group:             default
Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
Age:                        52d 
Created:                                   Tue, 28 Sep 2021 05:12:16 -0500  
Updated:                                   Tue, 28 Sep 2021 05:12:19 -0500  

Quotas:    
Category                                  Used  Limit  
App revisions                             2    120  
Apps                                      1     40  
Build runs                                1     100  
Builds                                    2     100  
Configmaps                                2     100  
CPU                                       0     128  
Ephemeral storage                         0     512G  
Functions                                 0     20  
Instances (active)                        0     250  
Instances (total)                         0     2500  
Job runs                                 13     100  
Jobs                                      2     100  
Memory                                    0     512G  
Secrets                                   6     100  
Subscriptions (cron)                      0     100  
Subscriptions (IBM Cloud Object Storage)  0     100  
Subscriptions (Kafka)                     0     100
```
{: screen}



## Getting logs for my builds
{: #ts-build-gettinglogs}

Logs can be helpful to troubleshoot problems when you run builds. You can view logs for builds with the CLI or the console. 
{: shortdesc}

### Getting logs for my builds from the console
{: #ts-build-gettinglogs-ui}

You can display logs for specific build run instances from the console. 
{: shortdesc}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Image builds**.
4. From the **Image build** tab, click the name of your image build to open the build page for a defined build, or [create a build](/docs/codeengine?topic=codeengine-build-create-config1#build-create-console).
5. From the build page for your defined build, click the name of the instance of your build run in the **Build runs** section. You might need to click **Submit build** to create a build run.  
6. From the build run instance page, you can view the build log information. Expand the specific build steps for detailed logging information.

For more information, see [viewing build logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-build-ui).

### Getting logs for my builds with the CLI
{: #ts-build-gettinglogs-cli}

Use the [**`ibmcloud ce buildrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs) command to display logs about the build run. Use this command to display logs of all the instances of a build run based on the name of the build run.

To view the logs for all instances of the `mybuildrun` build run, specify the name of the build run with the `--name` option; for example,  

```txt
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

Example output

```txt
Getting build run 'mybuildrun'...
Getting instances of build run 'mybuildrun'...
Getting logs for build run 'mybuildrun'...
OK

mybuildrun-bvzbg-pod-tppvg/step-source-default:
2021/09/21 09:39:08 Info: ssh (/usr/bin/ssh): OpenSSH_8.0p1, OpenSSL 1.1.1g FIPS  21 Apr 2020
2021/09/21 09:39:08 Info: git (/usr/bin/git): git version 2.27.0
2021/09/21 09:39:08 Info: git-lfs (/usr/bin/git-lfs): git-lfs/2.11.0 (GitHub; linux amd64; go 1.14.4)
2021/09/21 09:39:08 /usr/bin/git clone --quiet --no-tags --branch main --depth 1 --single-branch -- https://github.com/IBM/CodeEngine /workspace/source
2021/09/21 09:39:09 /usr/bin/git -C /workspace/source submodule update --init --recursive --depth 1
2021/09/21 09:39:10 /usr/bin/git -C /workspace/source rev-parse --abbrev-ref HEAD
2021/09/21 09:39:10 Successfully loaded https://github.com/IBM/CodeEngine (main) into /workspace/source
2021/09/21 09:39:10 /usr/bin/git -C /workspace/source rev-parse --verify HEAD

mybuildrun-bvzbg-pod-tppvg/step-build-and-push:
INFO[0000] Retrieving image manifest golang:alpine
INFO[0000] Retrieving image golang:alpine from registry index.docker.io
INFO[0001] Retrieving image manifest alpine
INFO[0001] Retrieving image alpine from registry index.docker.io
INFO[0003] Built cross stage deps: map[0:[/codeengine]]
INFO[0003] Retrieving image manifest golang:alpine
INFO[0003] Returning cached image manifest
INFO[0003] Executing 0 build triggers
INFO[0003] Unpacking rootfs as cmd COPY ./helloworld /helloworld requires it.
INFO[0009] COPY ./helloworld /helloworld
INFO[0009] Taking snapshot of files...
INFO[0009] COPY codeengine.go /
INFO[0009] Taking snapshot of files...
INFO[0009] RUN go build -o /codeengine /codeengine.go
INFO[0009] Taking snapshot of full filesystem...
INFO[0017] cmd: /bin/sh
INFO[0017] args: [-c go build -o /codeengine /codeengine.go]
INFO[0017] Running: [/bin/sh -c go build -o /codeengine /codeengine.go]
INFO[0018] Taking snapshot of full filesystem...
INFO[0018] Saving file codeengine for later use
INFO[0018] Deleting filesystem...
INFO[0019] Retrieving image manifest alpine
INFO[0019] Returning cached image manifest
INFO[0019] Executing 0 build triggers
INFO[0019] Unpacking rootfs as cmd COPY --from=0 /codeengine /codeengine requires it.
INFO[0019] COPY --from=0 /codeengine /codeengine
INFO[0019] Taking snapshot of files...
INFO[0019] CMD /codeengine
INFO[0019] Pushing image to us.icr.io/acme-namespace/codeengine-sample
INFO[0023] Pushed image to 1 destinations
```
{: screen}

## Getting system event information for my builds
{: #ts-build-gettingevent}

System event information can be helpful to troubleshoot problems when you run builds. You can view system event information for builds with the CLI. 
{: shortdesc}

1. Use the [**`ibmcloud ce buildrun list`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-list) command to list all your build runs in a project; for example,

    ```txt
    ibmcloud ce buildrun list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce buildrun get`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get) command to get the details of your a build run, for example,

    ```txt
    ibmcloud ce buildrun get --name mybuildrun  
    ```
    {: pre}

    Example output 

    ```txt
    Getting build run 'mybuildrun'...
    Run 'ibmcloud ce buildrun events -n mybuildrun' to get the system events of the build run.
    Run 'ibmcloud ce buildrun logs -f -n mybuildrun' to follow the logs of the build run.
    OK

    Name:          mybuilddrun
    [...]

    Created:       2021-06-01T11:43:24-04:00

    Summary:  Succeeded
    Status:   Succeeded
    Reason:   All Steps have completed executing

    Image:  us.icr.io/mynamespace/codeengine-codeengine-200
    ```
    {: screen}

    If you want more fine-grained details about your build run, use the `--o yaml` option with the **`buildrun get`** command; for example, `ibmcloud ce buildrun get --name myapp --o yaml`. This option is useful to show more detailed information in the CLI for the build run.
    {: tip}

3. Display the system events of your build run. Use the [**`ibmcloud ce buildrun events`**](/docs/codeengine?topic=codeengine-cli#cli-buildrun-events) command; for example,

    ```txt
    ibmcloud ce buildrun events --name mybuildrun 
    ```
    {: pre} 

    Example output 

    ```txt
    Getting build run 'mybuildrun'...
    Getting instances of build run 'mybuildrun'...
    Getting events for build run 'mybuildrun'...
    OK

    mybuildrun-bvzbg-pod-tppvg:
        Type    Reason     Age    Source                Messages
        Normal  Scheduled  4m43s  default-scheduler     Successfully assigned 62ckpsxlh7x/mybuildrun-bvzbg-pod-tppvg to 10.242.0.17
        Normal  Pulled     4m42s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/tekton-pipeline/entrypoint-bff0a22da108bc2f16c818c97641a296:v0.23.0-rc6@sha256:43dd56a6c7c10f80300a861615f6f8d91c026deba744f81553a4e536b301b322" already present on machine
        Normal  Created    4m42s  kubelet, 10.242.0.17  Created container place-tools
        Normal  Started    4m41s  kubelet, 10.242.0.17  Started container place-tools
        Normal  Pulled     4m40s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/git:v0.8.100" already present on machine
        Normal  Created    4m40s  kubelet, 10.242.0.17  Created container step-source-default
        Normal  Started    4m40s  kubelet, 10.242.0.17  Started container step-source-default
        Normal  Pulled     4m40s  kubelet, 10.242.0.17  Container image "icr.io/obs/codeengine/buildkit/builder:v0.9.0-rc.19" already present on machine
        Normal  Created    4m40s  kubelet, 10.242.0.17  Created container step-build-and-push
        Normal  Started    4m40s  kubelet, 10.242.0.17  Started container step-build-and-push
    ```
    {: screen}

    Events are only stored for one hour in the system.
    {: tip}


