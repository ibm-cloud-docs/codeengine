---

copyright:
  years: 2025
lastupdated: "2025-06-03"

keywords: low latency, zero error code engine apps, conformance testing, service-level objectives (SLOs), SLO, Iter8, code engine application, rolling back a revision, validating application code

subcollection: codeengine

content-type: tutorial
completion-time: 5m 

---

{{site.data.keyword.attribute-definition-list}}

# Validating your application code and latency with Iter8
{: #slovalidationtut}
{: toc-content-type="tutorial"}
{: toc-completion-time="5m"}

[Iter8](https://iter8.tools){: external} is the release engineering tool for Kubernetes that enables service-level objectives (SLO) validation, A/B testing, and progressive updates for Kubernetes applications. Now, you can use Iter8 to verify that your {{site.data.keyword.codeenginefull}} application is running with low latency and is error-free. Learn more about Iter8 in 5 minutes.
{: shortdesc}

Before you begin

- Set up [Docker](https://docs.docker.com/get-started/get-docker/){: external} on your local system.
- Create a {{site.data.keyword.codeengineshort}} application. Not sure how to create one? Then try the [Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) tutorial.

## Finding the URL of your {{site.data.keyword.codeengineshort}} application
{: #geturl-slovalidationtut}
{: step}

To find the URL of your application by using the CLI, run the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command and specify the `-output url`option. For example, find the URL for an application called `myapp`.

```txt
ibmcloud ce application get -n myapp -output url
```
{: pre}

Example output

```txt
https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}

To find the URL of an application by using the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview), go to the Application overview page. If the application is in `Ready` state, you can open it in a web page by clicking **Open application URL**. Save the URL.

## Running the Iter8 Docker container
{: #running-slovalidationtut}
{: step}

Iter8 is provided as a Docker container that includes all the dependencies that are needed to run Iter8. The following command starts the Docker container.

```txt
docker run --name ind --privileged -d iter8/ind:0.7.4
```
{: pre}

## Initializing the Iter8 Docker container
{: #initialize-slovalidationtut}
{: step}

When you initialize this Docker container, the command starts a local Kubernetes cluster within the Docker container and then installs Iter8 inside of the container.

```txt
docker exec ind ./iter8.sh
```
{: pre}

Look for output that says `All systems go...`.

## Validating service-level objectives (SLOs)
{: #experiment-slovalidationtut}
{: step}

Verify that your {{site.data.keyword.codeengineshort}} application satisfies latency and error-based service level objectives (SLOs) that you determined for your application. The following command generates requests for your {{site.data.keyword.codeengineshort}} application, constructs its latency and error profile, and verifies that your application satisfies the specified SLOs.

Replace `<URL-OF-YOUR-APPLICATION>` with the URL obtained in [Step 1](#geturl-slovalidationtut). You can also set custom limits for the three metrics that are used to evaluate your application. In the following example, you are verifying that the mean latency of your application is under 200.0 ms, the error rate is under 1% (you can make this 0.0), and the 95th percentile tail latency is under 500.0 ms.

```txt
docker exec ind helm install \
--set URL=<URL-OF-YOUR-APPLICATION> \
--set LimitMeanLatency=200.0 \
--set LimitErrorRate=0.01 \
--set Limit95thPercentileLatency=500.0 \
codeengine /iter8/helm/conformance
```
{: pre}

Example output

```txt
NAME: codeengine
LAST DEPLOYED: Wed Jun 30 01:10:14 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```
{: screen}

## Getting the results of the SLO validation
{: #results-slovalidationtut}
{: step}

The following command outputs the result of the SLO validation for your {{site.data.keyword.codeengineshort}} application.

```txt
docker exec ind \
bash -c "kubectl get experiment my-experiment -o yaml | iter8ctl describe -f -"
```
{: pre}

Example output

If you do not see output similar to the following example, you may need to wait a little longer and try the previous command again. The objectives section reports if your application is satisfying the specified SLOs. The metrics section reports the metrics observed for your application by Iter8.

```txt
****** Overview ******
Experiment name: my-experiment
Experiment namespace: default
Target: my-app
Testing pattern: Conformance
Deployment pattern: Progressive

****** Progress Summary ******
Experiment stage: Completed
Number of completed iterations: 1

****** Winner Assessment ******
> If the version being validated; i.e., the baseline version, satisfies the experiment objectives, it is the winner.
> Otherwise, there is no winner.
Winning version: my-app

****** Objective Assessment ******
> Identifies whether or not the experiment objectives are satisfied by the most recently observed metrics values for each version.
+--------------------------------------+--------+
|              OBJECTIVE               | MY-APP |
+--------------------------------------+--------+
| iter8-system/mean-latency <=         | true   |
|                              200.000 |        |
+--------------------------------------+--------+
| iter8-system/error-rate <=           | true   |
|                                0.010 |        |
+--------------------------------------+--------+
| iter8-system/latency-95th-percentile | true   |
| <= 500.000                           |        |
+--------------------------------------+--------+

****** Metrics Assessment ******
> Most recently read values of experiment metrics for each version.
+--------------------------------------+--------+
|                METRIC                | MY-APP |
+--------------------------------------+--------+
| iter8-system/request-count           | 40.000 |
+--------------------------------------+--------+
| iter8-system/error-count             |  0.000 |
+--------------------------------------+--------+
| iter8-system/mean-latency            | 66.060 |
+--------------------------------------+--------+
| iter8-system/error-rate              |  0.000 |
+--------------------------------------+--------+
| iter8-system/latency-95th-percentile | 73.055 |
+--------------------------------------+--------+
```
{: screen}

## Rolling back a revision
{: #rollout-slovalidationtut}
{: step}

If your latest revision fails to satisfy the experiment objectives that you specified, you may want to delete the latest revision and allow {{site.data.keyword.codeengineshort}} to automatically roll back to the previous stable revision. 

To delete the latest revision with the CLI, run the [**`ibmcloud ce revision delete`**](/docs/codeengine?topic=codeengine-cli#cli-revision-delete) command. 

To delete the latest revision from the console, go to the [{{site.data.keyword.codeengineshort}} Console](https://cloud.ibm.com/codeengine/overview). Select **Projects**-> your project -> **Applications** -> your application -> **Revisions and traffic**. Delete the revision that failed. {{site.data.keyword.codeengineshort}} automatically rolls back to the previous stable revision.

## Removing the Iter8 container
{: #cleanup-slovalidationtut}
{: step}

You can clean up your local system by removing the `Iter8-in-Docker` container and image if you no longer need it.

```txt
docker rm -f -v ind
```
{: pre}

## Next steps for Iter8
{: #nextsteps-slovalidationtut}

This tutorial is based on the Iter8 open source project. For more information, see [Iter8 open source project page](https://iter8.tools){: external}.
