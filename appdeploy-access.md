---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Accessing your app
{: #access-service}

After your app deploys, you can access it through a URL.
{: shortdesc}

From the console, your application URL is available from the components page and on the application details page.

From the CLI, run the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to find the URL of your app. To have the command output only the URL of the app, specify the `--output url` option with the **`app get`** command. 

## Access details about your app 
{: #access-app-details}

Find details about your app from the console or with the CLI.
{: shortdesc}

{{site.data.keyword.codeengineshort}} has quotas for apps and revisions of the apps within a project and app limits, such as memory and CPU. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
{: important}

### Accessing app details from the console
{: #access-appdetails-ui}

Details about your app are available in the console from the app page by clicking the name of your app from the list of applications within your project.  

### Accessing app details with the CLI
{: #access-appdetails-cli}

To view details of your app with the CLI, use the **`app get`** command. For a complete listing of options, see the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command. 
{: shortdesc}

For example, the following **`app get`** command displays details about the `myapp` app.

```
ibmcloud ce app get --name myapp
```
{: pre}

**Example output**

```
[...]
OK

Name:               myapp
ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:       myproject
Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
Age:                2m4s
Created:            2021-09-09T14:01:02-04:00
URL:                https://myapp.abcdabcdabc.us-south.codeengine.appdomain.cloud
Cluster Local URL:  http://myapp.abcdabcdabc.svc.cluster.local
Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
Status Summary:     Application deployed successfully

Image:                docker.io/ibmcom/hello
Resource Allocation:
    CPU:                1
    Ephemeral Storage:  500Mi
    Memory:             4G

Revisions:
    myapp-00001:
        Age:                100s
    Latest:             true
    Traffic:            100%
    Image:              docker.io/ibmcom/hello (pinned to d6fd55)
    Running Instances:  1

Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  0
    Timeout:        300

Conditions:
    Type                 OK    Age  Reason
    ConfigurationsReady  true  86s
    Ready                true  60s
    RoutesReady          true  60s

Events:
    Type    Reason   Age   Source              Messages
    Normal  Created  102s  service-controller  Created Configuration "myapp"
    Normal  Created  102s  service-controller  Created Route "myapp"

Instances:
    Name                                    Revision     Running  Status       Restarts  Age
    myapp-00001-deployment-699c45ddd-c25rm  myapp-00001  1/2      Terminating  0         102s
```
{: screen}

## Application status
{: #app-status}

The following table shows the possible status that your application might have.

| Status | Description |
| ------ | ------------|
| Deploying | The application is deploying. Deployment time includes the time before the app is scheduled as well as time to download images over the network, which can take a while. |
| Ready | The application is deployed and ready to use. |
| Ready (with warnings) | The deployment of a new application revision failed, but the original deployment is available. |
| Failed | The application deployment terminated, and at least one instance terminated in failure. The instance either exited with nonzero status or was terminated by the system.
| Unknown | For some reason, the state of the application cannot not be obtained, typically due to an error in communicating with the host. |


