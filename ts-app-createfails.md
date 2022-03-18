---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-18"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my app create failing?    
{: #ts-app-create-fails}
{: troubleshoot}

You cannot create an app. When you run the **`ibmcloud ce app create`** command in the CLI or deploy an app in the console, the application create does not complete successfully and displays a `failed` or `revision failed` error message.
{: tsSymptoms}

If you cannot create an app, determine whether one of the following cases is true.  
{: tsCauses}

1. The name of your app is not unique within the project. You receive an error message that contains `Application 'myapp' already exists within project 'myproj', please select a unique name.` 
2. The name of your app is not valid. You receive an error message that contains `An application name must consist of lowercase alphanumeric characters, '-' and must start with an alphabetic character and end with an alphanumeric character.` 
3. If the image that you referenced does not exist, the app create does not complete and an error occurs. You receive an error message that contains `Unable to pull the image`.
4. If you do not have the permissions to access the referenced image, the app create does not complete and an error occurs. You receive an error message that contains `Unable to pull the image`. 
5. The memory or CPU setting is not valid. You receive an error message that contains `memory parameter must be between .25 G and 32 G` or `cpu parameter must be between .0125 and 8.0`.For more information about {{site.data.keyword.codeengineshort}} limits for apps, see [Application limits and defaults for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits#limits_application).
6. The resource quota for apps or app revisions is reached and the app (or app revision) is not created. {{site.data.keyword.codeengineshort}} has quotas for apps and revisions of the apps within a project. For more information about {{site.data.keyword.codeengineshort}} limits, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

Try one of these solutions.
{: tsResolve}

1. To determine whether the name of your app is unique within the project, use the **`ibmcloud ce app list`** command to list all defined apps and check whether an app with the same name exists. If an app with the same name exists, use the `ibmcloud ce app  delete --name APP_NAME` to delete the old app. The name of the app must be unique within your project. 
2. To confirm that the name of your app is valid, check that the name of your app consists of lowercase alphanumeric characters, '-', and that the name starts and ends with an alphabetic character. 
3. To confirm that the image for your app exists, review the error message for information about the failure.  

    a. To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all the runtime artifacts your application needs to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-build-image) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

    b. If you use the **`app create`** command in the {{site.data.keyword.codeengineshort}} CLI, specify the name of the image that is used for your application by using the format `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. For more information about the format to use to specify the repository for your image, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. 

4. To confirm that you can access the referenced image, verify the location of your image and confirm that you have permissions to access the image.  

    If the image is located in a container image registry, such as Docker Hub or {{site.data.keyword.registryfull_notm}}, check that you added registry access to {{site.data.keyword.codeengineshort}} and that you are using the correct image registry access secret. For more information about working with images in a container image registry, see [adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).  

5. If you specify the `--memory` or `--cpu` option with the **`app create`** command, confirm that you are using valid values. In the following command, the values that are specified for `--memory` and `--cpu` are not valid; for example,  

    ```txt
    ibmcloud ce app create --name myapp  --image icr.io/codeengine/codeengine --memory 50Gi --cpu 20
    ```
    {: pre}

    **Example output**

    ```txt
    Creating application 'myapp'...
    FAILED
    memory parameter must be between 128Mi and 32Gi
    cpu parameter must be between .01 and 8.0
    ```
    {: screen}

    To fix the errors, set the `--memory` option between 128 Mi and 32 Gi, and set the `--cpu` option between 0.01 and 8.0 vCPU. 

6. If you receive an error message that indicates the resource quota is exceeded, delete apps or app revisions before you can deploy additional apps or app revisions. 

* To manage your apps, use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to display a list of all your apps in the current project. Use the [**`ibmcloud ce app delete`**](/docs/codeengine?topic=codeengine-cli#cli-application-delete) command to remove apps as needed.

* To manage your app revisions, use the [**`ibmcloud ce revision list`**](/docs/codeengine?topic=codeengine-cli#cli-revision-list) command to display all your app revisions. 

If these solutions do not solve your issue, for further debugging, try retrieving the logs or the system event information for your app. For more information, see [How do I get logs for my apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettinglogs) and [How do I get system event information for my apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent).

For more about working with apps, see [Deploying apps](/docs/codeengine?topic=codeengine-application-workloads).


