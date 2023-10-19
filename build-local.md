---

copyright:
  years: 2020, 2023
lastupdated: "2023-10-17"

keywords: builds for code engine, builds, building, source code, build run, application image builds for code engine, job image builds for code engine, container image builds with code engine, registry secret, registry access secret

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Create a build configuration that pulls source from a local directory
{: #build-config-local}

If your source is on your local workstation, create a build configuration with settings that include information about where to pull source from the local directory. For the build output, you can specify registry details, or let {{site.data.keyword.codeengineshort}} manage {{site.data.keyword.registrylong_notm}} details. 
{: shortdesc}

You can create a build configuration that pulls source from a local directory by using only the {{site.data.keyword.codeengineshort}} CLI. 

When you submit a build that pulls code from a local directory, your source code is packed into an archive file and uploaded to your {{site.data.keyword.registrylong_notm}} instance. Note that you can only target {{site.data.keyword.registrylong_notm}} for your local builds. The source image is created in the same namespace as your build image. 

You can ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a Node.js application might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.

Creating a build configuration does not create an image, but creates the configuration to build an image. You must then run a build that references the build configuration to create an image. The build configuration is not validated or used to create an image until the build is run. The build configuration enables multiple subsequent builds of an image, such as when changes are applied to the source repository.
{: tip}

To create a build configuration that pulls code from a local directory with the CLI, use the **`build create`** command and specify the `build-type` as `local`. For a complete listing of options, see the [**`ibmcloud ce build create`**](/docs/codeengine?topic=codeengine-cli#cli-build-create) command.

With the **`build create`** command, you can have {{site.data.keyword.codeengineshort}} build the image from your source and store the image in {{site.data.keyword.registrylong_notm}}. For this *automatic access* case, you do not need to specify a registry secret or the location of the image registry. Or, you can specify the location for your build image output and provide a registry secret so that {{site.data.keyword.codeengineshort}} can access and push the build result to your registry.


## Creating a build configuration with the CLI (with local source and automatic access to registry)
{: #build-config-local-cli-a}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your local source, and automatically uploads the image to {{site.data.keyword.registrylong_notm}}. See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry) for more information about setting required permissions for {{site.data.keyword.codeengineshort}} to automatically access these images in {{site.data.keyword.registryshort}}.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Create a build configuration to build an image from source on your local workstation and let {{site.data.keyword.codeengineshort}} automatically store and access the image. When you specify `local` as the value for `-build-type`, you can only target {{site.data.keyword.registrylong_notm}} for the output of your local build. In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. By not specifying the location of the image registry or a registry secret, {{site.data.keyword.codeengineshort}} pushes the build output to {{site.data.keyword.registrylong_notm}} with automatic access. 

```txt
ibmcloud ce build create --name build-local-dockerfile --build-type local 
```
{: pre}

After you create the build configuration, you must [run the build](/docs/codeengine?topic=codeengine-build-run) to create the image file. After your image file is created, you can [deploy an app](/docs/codeengine?topic=codeengine-deploy-app-crimage) or [run a job](/docs/codeengine?topic=codeengine-create-job-crimage) with your newly built image file.


## Creating a build configuration with the CLI (with local source and user-provided access to registry)
{: #build-config-local-cli-b}

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your local source, and then uploads the image to your container registry with the registry access that you provide. 

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Create a registry secret so you can save your image](/docs/codeengine?topic=codeengine-add-registry).

Create a build configuration to build an image from source on your local workstation and specify the location of the image registry for the build output with a registry secret. With the **`build create`** command, when you specify `local` as the value for `--build-type`, you can only target {{site.data.keyword.registrylong_notm}} for the output of your local build. Specify the `--image` option to provide the location of the image registry, and specify the `--registry-secret` option to access the registry. In this example, the command uses the default `dockerfile` strategy, and the default `medium` build size. 


```txt
ibmcloud ce build create --name build-local-dockerfile --build-type local --image us.icr.io/mynamespace/codeengine-build --registry-secret myregistry 
```
{: pre}

After you create the build configuration, you must [run the build](/docs/codeengine?topic=codeengine-build-run) to create the image file. After your image file is created, you can [deploy an app](/docs/codeengine?topic=codeengine-deploy-app-crimage) or [run a job](/docs/codeengine?topic=codeengine-create-job-crimage) with your newly built image file.


