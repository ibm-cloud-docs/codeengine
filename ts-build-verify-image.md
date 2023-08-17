---

copyright:
  years: 2020, 2023
lastupdated: "2023-08-17"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds, verify image reference, image reference, container image

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I verify my image reference? 
{: #ts-build-verify-image}
{: troubleshoot}


When you work with {{site.data.keyword.codeengineshort}} apps and jobs, you must specify a container image reference and a registry secret to access the image. For these workloads to work correctly, the image reference and its access properties must remain valid for the life of the app or job. 
{: tsSymptoms}

If you receive a message to verify the image reference, check to make sure that the image reference, and its access properties are valid. 
{: tsCauses}

Example error message 

```txt
Revision failed
Unable to pull the image "icr.io/codeengine/my_image" Verify the image reference. 
```
{: screen}


Take the following steps to help you resolve the problem with your image.
{: tsResolve}

1. Your image must exist. 
    * Check that the image was pushed to the registry and that it has not been deleted from the registry. 
    * In the configuration for your {{site.data.keyword.codeengineshort}} entity (apps job, function), confirm that the name of the referenced image is correct, and that the path to the image is correct. 

2. Confirm that access to the container image is defined and that the credentials in the referenced registry secret are valid. 
    * If the referenced image uses an SHA checksum or tag name, make sure that your image can be pulled from the registry, and that all these values are included in the image reference. 
    * If you add a rotating API key to a {{site.data.keyword.codeengineshort}} registry secret after the {{site.data.keyword.codeengineshort}} app, job, or function was created, then the rotating API key does not automatically update the key that is stored in the registry secret. To ensure that the rotating API key is updated, [update the registry secret](/docs/codeengine?topic=codeengine-secret#secret-update) with the most recent API key. 
    * See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

For more information about image references, see the following topics. 
* [Planning your build](/docs/codeengine?topic=codeengine-plan-build). 
* [Building a container image](/docs/codeengine?topic=codeengine-build-image).
* [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads). 
* [Working with jobs](/docs/codeengine?topic=codeengine-job-plan).
* [Working with functions](/docs/codeengine?topic=codeengine-fun-work)




