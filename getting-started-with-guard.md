---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-21"

keywords: security, zero trust, runtime security, workload security, situational awareness, serverless security, Guard, code engine application security, code engine security

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Securing your application with Guard
{: #getting-started-with-guard}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Guard is a runtime-security solution that {{site.data.keyword.codeenginefull}} you can use to govern the incoming requests and outgoing responses of your application. Guard uses a per-application auto learned set of micro-rules to govern the application incoming requests and outgoing responses. As a result, you can use Guard to identify application anomalies and support Situational Awareness. Guard can also block requests or responses that are not in line with expected patterns. 
{: shortdesc}

In this tutorial, deploy a Hello World application and protect it with Guard.

Before you begin:

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- Be familiar with [deploying applications using CLI](/docs/codeengine?topic=codeengine-deploy-app-tutorial).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}


## Deploy a guard-learner application as a per-project service
{: #guard-learner}
{: step}

Guard-Learner is a service that learns the necessary micro-rules for each Guard-protected application in a project. To deploy a Guard-Learner application, create it in your project. Note that you create the Guard-Learner application only one time per {{site.data.keyword.codeengineshort}} project. 

- Protect your application and avoid exposing it to potential offenders by setting the visibility for the app to the project level with the `--v project` option. For more information, see [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).
- Scale the Guard-Learner service to continuously run a single instance with the  `--min 1 --max 1` option.

```txt
ibmcloud ce application create -n guard-learner -v project --min 1 --max 1 -p 8888 -i ghcr.io/ibm/workload-security-guard/guard-learner
```
{: pre}

Example output

```txt
Creating application 'guard-learner'...
[...]
Run 'ibmcloud ce application get -n guard-learner' to check the application status.
OK

http://guard-learner.p8abcd4abcd.svc.cluster.local
```
{: screen}
    

## Creating and deploying a protected Hello World application
{: #guard-deploy-app}
{: step}

Create the Hello World application and assign it `project` visibility.  In the following example, you can change the application name and set a different image and port.

- Protect your application and avoid exposing it to potential offenders by setting the visibility for the app to the project level with the `--v project` option. For more information, see [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).
- Consider setting the minimum scale to a single instance with the  `--min 1` option.

```txt
export SERVICE_NAME="myapp"
ibmcloud ce application create -n ${SERVICE_NAME} -v project -min 1 -p 8080 -i icr.io/codeengine/hello
```
{: pre}

Example output

```txt
Creating application 'myapp'...
[...]
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK
    
http://myapp.p8abcd4abcd.svc.cluster.local
```
{: screen}


## Finding the namespace and service URLs 
{: #guard-get-parameters}
{: step}

Extract information about your deployed application and about the project's Guard-Leaner.

```txt
export NAMESPACE=`ibmcloud ce project current -o json|jq -r .kube_config_context`
export GUARD_URL=`ibmcloud ce application get -n guard-learner -o url`
export SERVICE_URL=`ibmcloud ce application get -n ${SERVICE_NAME} -o url`

echo "The protected service name '${SERVICE_NAME}' namespace '${NAMESPACE}' url '${SERVICE_URL}'"
echo "The guard learner url is '${GUARD_URL}'"
```
{: pre}

Example output

```txt
The protected service name 'myapp' namespace 'p8abcd4abcd' url 'http://myapp.p8abcd4abcd.svc.cluster.local'
The guard learner url is 'http://guard-learner.p8abcd4abcd.svc.cluster.local'
```
{: screen}

## Exposing the Hello World application to the internet through Guard
{: #guard-expose-app}
{: step}

Add a Hello World guard to securely expose the Hello World application to the internet.

```txt
ibmcloud ce application create -n ${SERVICE_NAME}-guard --min 1 -p 22000 \
        -e GUARD_URL=${GUARD_URL} \
        -e SERVICE_URL=${SERVICE_URL} \
        -e SERVICE_NAME=${SERVICE_NAME} \
        -e NAMESPACE=${NAMESPACE} \
        -i ghcr.io/ibm/workload-security-guard/guard-rproxy
```
{: pre}

Example output

```txt
Creating application 'myapp-guard'...
[...]
Run 'ibmcloud ce application get -n myapp-guard' to check the application status.
OK
    
https://myapp-guard.p8abcd4abcd.us-south.codeengine.appdomain.cloud
```
{: screen}

You can access the protected Hello World application through the URL that is exposed by Hello World guard.


Notes:
- Deploy a Guard for any application you want to protect.
- Provide Guard with the project namespace and the corresponding application name and url it protects. 
- Provide Guard with the url of the Guard-Learner. 
- Set `USE_CONFIGMAP=true` to maintain the micro-rules in a configmap named `guardian-${SERVICE_NAME}` .
- Consider setting the minimum scale of the Guard app to a single instance with the  `--min 1` option.


## Managing the security of the Hello World application and gaining situational awareness
{: #guard-situational-awareness}
{: step}

Guard offers situational awareness into the application security posture. You can find security alerts in the log file of Guard, as they occur.

```txt
ibmcloud ce application logs -n ${SERVICE_NAME}-guard 
```
{: pre}

Example output

```txt
[...]
{"level":"warn","message":"SECURITY ALERT! HttpRequest: Headers: KeyVal: Known Key X-B3-Traceid: Digits: Counter out of Range: 25"}  
[...]
```
{: screen}

Security alerts appear as warnings in the guard log file and start with the string `SECURITY ALERT!`. The default setup of Guard is to allow any request or response and learn any new pattern after reporting it. When the application is actively serving requests, it typically takes about 30 min for Guard to learn the patterns of the application requests and responses and build corresponding micro-rules. After the initial learning period, Guard sends alerts only when a change in behavior is detected. 

Note that in the default setup, Guard continues to learn any new behavior and therefore avoids reporting alerts repeatedly when the new behavior reoccurs.
Correct security procedures should include reviewing any new behavior detected by Guard. 

Guard can also be configured to operate in other modes of operation, such as:

- Move from auto learning to manual micro-rules management after the initial learning period
- Block requests/responses when they do not conform to the micro-rules 

For more information or for troubleshooting help, see the [#code-engine channel](https://ibm-cloud-success.slack.com){: external}.

## Clean up the tutorial applications
{: #guard-cleanup}
{: step}

After you are finished with this tutorial, you can remove the Hello World application, the Hello World Guard, and the Guard-Learner as shown in the following example.

```txt
ibmcloud ce application delete -n ${SERVICE_NAME}
ibmcloud ce application delete -n ${SERVICE_NAME}-guard
ibmcloud ce application delete -n guard-learner
```
{: pre}

