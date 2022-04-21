>---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-21"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands
{: #migrate-cf-ce-cmd}

Find and compare the {{site.data.keyword.codeengineshort}} CLI command that is equivalent to your Cloud Foundry commands.

## Connect to the deployment API region commands
{: #deployment-api}

Cloud Foundry
:    `ibmcloud target --cf-api api.us-south.cf.cloud.ibm.com`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud target -r [region]`

## Create a deployment location for your workload commands
{: #deployment-place}

Cloud Foundry
:    `ibmcloud cf create-org [orgName]`
:    `ibmcloud target -o [orgName]`
:    `ibmcloud target -s [spaceName]`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce project create --name [projectName]`

You can also create a project from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

## List your apps and jobs commands
{: #list-workload}

Cloud Foundry
:    `ibmcloud cf apps`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce app list`
:    `ibmcloud ce job list`

You can also view your applications and jobs from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

## Deploy a image as an app or job commands
{: #deploy-commands}

Cloud Foundry
:    `ibmcloud cf push`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce build create` Define a build
:    `ibmcloud ce buildrun submit`  Run a build
:    `ibmcloud ce app create` Deploy image as an app
:    `ibmcloud ce job create` Create a batch job

You can perform these tasks from a single web page in the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

## Bind a Service to a workload
{: #binding-commands}

Cloud Foundry
:    `ibmcloud cf bind-service [AppName] [ServiceInstance]https://cli.cloudfoundry.org/en-US/v6/bind-service.html`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce app bind --name [AppName] --service-instance [ServinceInstance]`
:    `ibmcloud ce job bind --name [JobName] --service-instance [ServinceInstance]`


## Update applications or jobs commands
{: #update-commands}

Cloud Foundry
:    `ibmcloud cf scale ...`
:    `ibmcloud cf set-env ...`
:    `ibmcloud cf push ...`
:    `ibmcloud cf delete ...`

For example, to scale your application to 2 instances, 1 G of memory, and restart it, run `cf scale APP_NAME -i 2 -m 1G -f`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce app update ...`
:    `ibmcloud ce job update ...`

You can also update your applications and jobs from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

For information about what you can update with {{site.data.keyword.codeengineshort}}, see the following topics.

- [Working with applications](/docs/codeengine?topic=codeengine-application-workloads)
- [Updating an app](/docs/codeengine?topic=codeengine-update-app)
- [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan)
- [Updating a job](/docs/codeengine?topic=codeengine-update-job)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command


## Control applications and jobs commands
{: #control-commands}

Cloud Foundry
:    `ibmcloud cf start AppName` to start your application
:    `ibmcloud cf stop AppName` to stop your application

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce app create ...`
:    `ibmcloud ce app delete ...`
:    `ibmcloud ce job create ...`
:    `ibmcloud ce job delete ...`

You can also control your applications and jobs from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

## Get information about apps commands
{: #get-info-commands}

Cloud Foundry
:    `ibmcloud cf app AppName`

{{site.data.keyword.codeengineshort}}
:    `ibmcloud ce app get -n <APPNAME>`
:    `ibmcloud ce job get -n <JOBNAME>`

You can also view information about your applications and jobs from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

## Specifying a buildpack version
{: #specify-buildpack}

Cloud Foundry
:    `ibmcloud cf push -b https://github.com/cloudfoundry/nodejs-buildpack.git#v1.6.56`

{{site.data.keyword.codeengineshort}}
:    Not supported


## Next steps
{: #migrate-cf-ce-next-cmd}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with Code Engine](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. [Try out Code Engine with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. **{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands**
7. Still have questions? Try the [Migrating Cloud Foundry applications to Code Engine FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).


