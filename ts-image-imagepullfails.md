---

copyright:
  years: 2023, 2023
lastupdated: "2023-09-19"

keywords: benefits, terminology, developers, capabilities, {{site.data.keyword.codeengineshort}} 

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Why can't {{site.data.keyword.codeengineshort}} pull an image?
{: #image-cannot-pull} 
{: troubleshoot}


When you deploy a {{site.data.keyword.codeengineshort}} app or run a job, you receive an error message that contains `Unable to pull the image`.
{: tsSymptoms}


To troubleshoot this problem, confirm that the image exists and that you have access to the image. Check that the following conditions are met.
{: tsCauses}


* To confirm that the image for your app or job exists, review the error message for information about the failure.

* To deploy applications or run jobs in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all the runtime artifacts your application needs to run, such as runtime libraries. You can use many different methods to [create the container image](/docs/codeengine?topic=codeengine-plan-build), including building your app from source code by using the build container images feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry). 

* If you use the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), or [**`ibmcloud ce jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command in the {{site.data.keyword.codeengineshort}} CLI, specify the name of the image that is used for your application or job by using the format `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io.` If `TAG` is not specified, the default is `latest`. Review these commands for more information about the format to use to specify the image registry.


Try the following solutions to resolve your problem.
{: tsResolve}


1.  You are not authorized. If you do not have the permissions to access the referenced image, the application create does not complete, and an error occurs. You receive an error message that contains `Unable to pull` the image.

    * To confirm that you can access the referenced image, verify the location of your image and confirm that you have permissions to access the image.

    * Check that you added registry access to {{site.data.keyword.codeengineshort}} and that you are using the correct registry secret, if the image is located in a container image registry, such as Docker Hub or {{site.data.keyword.registrylong}}. For more information about working with images in a container image registry, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry). 
  
2. The container registry quota is exceeded.

    *  Check for an `ImagePullBackOff` error by running the [**`ibmcloud ce jobrun events --jobrun JOBRUN_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command; for example,

    ```sh
      ibmcloud ce jobrun events --jobrun myjobrun
    ```
    {: pre} 

    * If the error in the system events is similar to the following message, this error indicates that the registry quota is exceeded. Consider upgrading your plan. For information about {{site.data.keyword.registrylong}} service plans and quota limits, see [About {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-registry_overview).

    ```txt
    403 Forbidden - Server message: denied: You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan.
    ```
    {: screen}

3. The container registry needs authentication.

    * If the error in the system events is similar to the following message, this error indicates that access to the registry does not exist or might require authorization. Check that your credentials have appropriate access to the registry.

    ```txt
    Failed to pull image "<image_name>": rpc error: code = Unknown desc = failed to pull and unpack image "<image_name:image_tag>": failed to resolve reference <image_name:image_tag>": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed.
    ```
    {: screen}

4. {{site.data.keyword.codeengineshort}} cannot find your image in your container registry. 

    In this scenario, your image exists and the registry access works, but {{site.data.keyword.codeengineshort}} finds a different image than the image it was expecting for a specific application revision. The container registry image digest does not match the expected digest of the image for an application revision.

    When you deploy your application or new app revision, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment.  

    If you create a newer version of the image with the same tag as the original image that was referenced by your application, the original image is overwritten in the container registry. However, {{site.data.keyword.codeengineshort}} cannot find this newer image because the newer image has a different digest than the digest for the application revision. The image that is associated with your specific application revision has a unique container registry digest, and {{site.data.keyword.codeengineshort}} uses this digest for the life of your application revision. 
    
    If you create a newer version of an image with the same tag as the original image, then the original image is overwritten in the container registry and becomes untagged. The newer image is tagged, and this newer image has a different digest. Your {{site.data.keyword.codeengineshort}} application does not use this newer image because the newer image has a different digest than the digest of the image that is referenced by the application revision. {{site.data.keyword.codeengineshort}} can still create new instances of the application revision if the image that was referenced originally still exists. If the originally referenced image by your application does not exist, {{site.data.keyword.codeengineshort}} does not find the expected image digest, and the application fails because it cannot pull the image. Take care when you clean up and delete images, and when you configure retention policies for your container registry. Overwriting a tagged image is not problematic. However, problems can occur if you overwrite an image with an enabled retention policy that deletes the untagged image, or if you manually trigger a cleanup of untagged images.


    If the error in the system events is similar to the following message, this error indicates that {{site.data.keyword.codeengineshort}} cannot pull the image from the registry namespace. Check that the tag for your image points to the correct image digest. 

    ```txt
    Unable to pull the image. Image "<image_name>" does not exist in the registry namespace. Check your registry repository and tag. If the image exists in the repository, check whether the specified tag points to the correct image digest.
      ```
    {: screen}

    To use a newer image that was pushed with the same tag with your application, you must [update your application](/docs/codeengine?topic=codeengine-update-app) to create a new application revision that references the newer tagged image.


## Next steps
{: #image-cannot-pull-next} 

To learn more about troubleshooting images, see [Debugging images](/docs/codeengine?topic=codeengine-troubleshoot-images).

For more information about troubleshooting apps, job, and builds with considerations for images, see the following topics.

* [Troubleshooting apps - Why is my app create failing?](/docs/codeengine?topic=codeengine-ts-app-create-fails)
* [Troubleshooting apps - Why did my app stop running?](/docs/codeengine?topic=codeengine-ts-app-end)
* [Troubleshooting apps - Why doesn't my app ever become ready?](/docs/codeengine?topic=codeengine-ts-app-neverready)
* [Troubleshooting jobs - Why is my job run not completing?](/docs/codeengine?topic=codeengine-ts-jobrun-doesnotcomplete)
* [Troubleshooting jobs - Why can't I submit a job run with the CLI?](/docs/codeengine?topic=codeengine-ts-jobrun-submit-fails-cli)
* [Troubleshooting builds - Build fails in the build and push step](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail)
* [Troubleshooting builds - Build fails when the ephemeral storage limit is exceeded](/docs/codeengine?topic=codeengine-ts-build-ephemeral-limit)
* [Troubleshooting builds - Build fails in the source step](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail)



