---

copyright:
  years: 2023, 2023
lastupdated: "2023-03-30"

keywords: benefits, terminology, developers, capabilities, code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Debugging images
{: #troubleshoot-images} 
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot images. 
{: shortdesc}


## Working with images
{: #ts-image-workwith}

A build, or image build, is a mechanism that you can use to create a container image from your source code. 

A container registry, or registry, is a service that stores container images. For example, {{site.data.keyword.registryfull_notm}} and Docker Hub are container registries. A container registry can be public or private. A container registry that is public does not require credentials to access. In contrast, accessing a private registry does require credentials.

{{site.data.keyword.codeengineshort}} requires access to container registries to complete the following actions:
- To retrieve (or "pull") a container image to run an app or job
- To store a newly created container image as an output of an image build
- To store and retrieve local files when a build is run from local source

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you a streamlined way to run your code as an app or job.

When you want {{site.data.keyword.codeengineshort}} to handle the build process for you, {{site.data.keyword.codeengineshort}} can pull your source code and create the container image for you from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile or Cloud Native Buildpacks. 

Consider the following points before you build your container image:

* Before you start building images, review [planning information](/docs/codeengine?topic=codeengine-plan-build). You'll also need to verify that you can access the registry. See [Setting up authorities for container registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

* If you build multiple versions of the same container image, the latest version of the container image is downloaded and used when you run your job or deploy your application, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the app or job. 

* Build runs that are submitted with the CLI that do not reference a defined build configuration are not viewable from the console.

* {{site.data.keyword.codeengineshort}} has quotas for build runs within a project. For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). 

Build runs that complete are ultimately automatically deleted. When you run a build run with a single CLI command such that it is not based on a build configuration, this build run is deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.
{: note}

For more details, see the following information.  

* [Planning to build container images](/docs/codeengine?topic=codeengine-plan-build), and [building a container image](/docs/codeengine?topic=codeengine-build-image).
* [Working with apps](/docs/codeengine?topic=codeengine-application-workloads)
* [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan)


## Getting logs for my images
{: #ts-images-logs}

Logs can be helpful to troubleshoot problems when you deploy applications, run jobs, or run builds to create images. 
{: shortdesc}

See the following topics for ways to get logs. 

* [Getting logs for builds](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettinglogs).
* [Getting logs for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettinglogs).
* [Getting logs for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-gettinglogs).


## Getting system event information for my images
{: #ts-images-systemevents}

System event information can be helpful to troubleshoot problems when you deploy applications, run jobs, or run builds to create images. 

See the following topics for ways to get system events. 

* [Getting system event information for builds](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettingevent).
* [Getting system event information for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent).
* [Getting system event information for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent).







