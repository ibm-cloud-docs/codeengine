---

copyright:
  years: 2023, 2023
lastupdated: "2023-11-14"

keywords: functions in code engine, function workloads, function source code, function git repository

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating function workloads with repository source code
{: #fun-create-repo}


You can create your function directly from source code that is located in a Git repository from the {{site.data.keyword.codeenginefull}} console or with the CLI.
{: shortdesc}

In this scenario, {{site.data.keyword.codeengineshort}} builds a code bundle from your Git repository source, automatically uploads the code bundle to your container registry, and then creates your function to reference this built code bundle. You need to provide only a name for the function, the URL to the Git repository, and the runtime for the function. In this case, {{site.data.keyword.codeengineshort}} manages the namespace for you. However, if you want to use a different container registry, then you must specify the code bundle and a registry secret for that container registry. 

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).


## Creating function workloads with repository source code from the console
{: #fun-create-repo-console}


Create a function with source code from the console.
{: shortdesc} 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Let's go**.
3. Select **Function**.
4. Enter a name for the function; for example, `myfunction`. Use a name for your function that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must select a project to create a function. 
6. Select a **Runtime image** for your function code. For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).
7. Select to **Build code bundle from source code**. When you select this option, your function is created from source code and stored in container registry.
8. Select a source repository, for example `https://github.com/IBM/CodeEngine`. If you choose to use the sample source, you do not need require credentials so you can select `None` for the **Code repo access**. You can optionally provide a branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. Click **Next**.  
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Select a container registry location, such as `IBM Registry, Dallas` to specify where to store the image of your build output. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Provide registry information about where to store the image of your build output. Select an existing **Registry access secret** or create a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you.
12. Select a namespace, name, and a tag for your image. If you are building your image to an {{site.data.keyword.registrylong_notm}} instance that is in your account, you can select an existing namespace or let {{site.data.keyword.codeengineshort}} create and manage the namespace for you. For additional help, click **Help me specify the code bundle**. For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).
13. Specify your resource information, including [CPU and memory combinations](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo) and [Scale down delay](/docs/codeengine?topic=codeengine-fun-work#functions-scale). 
14. Optionally, specify a [custom domain](/docs/codeengine?topic=codeengine-fun-domainmapping) or [environment variables](/docs/codeengine?topic=codeengine-envvar). You can add these options later.
15. Click **Create**.
16. After the Function status changes to **Ready**, you can test the function. Click **Test function** and then click **Send request**. To open the function in a web page, click **Function URL**. 
17. You can also change your function code in the Editor window. When you redeploy your function, the code is stored inline.

You can invoke your function by clicking **Test function** and then **Send request**.


## Creating function workloads with repository source code with the CLI
{: #fun-create-repo-cli}

Use the **`function create`** command to both build a code bundle from your Git repository source, and create your function to reference this built code bundle. For a complete listing of options, see the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command. 


Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).


The following example **`function create`** command creates the `myfun` function, which references code that is located in `https://github.com/IBM/CodeEngine`. This command automatically builds the code bundle and uploads it to an {{site.data.keyword.registrylong}} namespace in your account. The function references this built code bundle. By specifying the `--build-context-dir` option, the build uses the source in the `helloworld-samples/function-nodejs` directory.   

```txt
ibmcloud ce function create --name myfun --runtime nodejs-18 --build-source https://github.com/IBM/CodeEngine --build-context-dir /helloworld-samples/function-nodejs
```
{: pre}

Example output

```txt
Preparing function 'myfun' for build push...
Creating function 'myfun'...
Submitting build run 'myfun-run-230111-111212718'...
Creating image 'icr.io/ce--abcde-glxo4kabcde/function-myfun:230111-1532-vwo4o'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myfun-run-230111-111212718' to check the build run status.
Waiting for function 'myfun' to become ready...
Function 'myfun' is ready.
OK                                                
Run 'ibmcloud ce function get -n myfun' to see more details.

https://myfun.11a66hbi3rhz.us-south.codeengine.appdomain.cloud
```
{: screen}

Notice the output of the **`function create`** command provides information on the progression of the build run before the function is created. 
{: tip}

In this example, the built code bundle is uploaded to the `ce--abcde-4svg40kna19` namespace in {{site.data.keyword.registryshort}}. 

The following table summarizes the options that are used with the **`function create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the function. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). | 
| `--build-source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`. |
| `--build-context-dir` | The directory in the repository that contains the code. This value is optional. |
| `--runtime` | The runtime for the function. |
{: caption="Table 1. Command description" caption-side="bottom"}

The following output shows the result of the **`function get`** command for this example, including information about the build.

Example output

```txt
Getting function 'myfun'
'...
OK

Name:          myfun  
Project Name:  sample  
Project ID:    abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
Age:           27m  
Created:       2023-06-27T21:07:26Z  
URL:           https://myfun.13c66hbi3rhz.us-south.codeengine.test.appdomain.cloud  
Status:        Ready  

Resources:    
  CPU:                 0.25  
  Memory:              500M  
  Max Execution Time:  60 seconds  

Build Information:    
  Build Run Name:     myfun-run-230111-111212718  
  Build Type:         git  
  Build Strategy:     codebundle-nodejs-18  
  Timeout:            600  
  Source:             https://github.com/IBM/CodeEngine  
  Context Directory:  /helloworld-samples/function-nodejs    
                      
  Build Run Summary:  Succeeded  
  Build Run Status:   Succeeded  
  Build Run Reason:   All Steps have completed executing  
  Run 'ibmcloud ce buildrun get -n myfun-run-230111-111212718' for details.  

Function Code:    
  Runtime:        nodejs-18 (managed)  
  Bundle Secret:  ce-auto-icr-us-south  
  Code Bundle:    cr://icr.io/ce--abcde-glxo4kabcde/function-myfun:230111-1532-vwo4o 
  Main:           main() 
```
{: screen}

Now that your function is created from repository source code, you can update the function to meet your needs by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

When your function is created from repository source code or from [local source](/docs/codeengine?topic=codeengine-fun-create-local) with the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted. Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.
{: note}


## Including dependencies for your Function
{: #fun-package-repo}

You can create Functions in many different programming languages. When your Function code grows complex, you can add code modules as dependencies for your Function. Each language has its own modules to use with your Function code. For example, Node.js dependencies are usually existing `npm` modules, whereas Python uses Python packages. These dependencies must be declared and created in a file with your source code

### Including modules for a Node.js Function
{: #function-nodejs-dep-repo}

Create a function that includes a dependency for a specific Node.js module by creating a `package.json` file. In this case, both the source code and package file are located in the same folder.

1. Create your source code by writing your code into a `main.js` file. For example, copy the following code example into a file called `main.js`.

    ```javascript
    function main(args) {
      const LoremIpsum = require("lorem-ipsum").LoremIpsum;
      const lorem = new LoremIpsum();

      return {
        headers: { "Content-Type": "text/plain;charset=utf-8" },
        body: lorem.generateWords(10),
      };
    }

    module.exports.main = main;
    ```
    {: codeblock}
  
2. Create a `package.json` file that contains the required dependencies for your Function. For the previous code example, use the following contents for your `package.json` file.

    ```sh
    {
      "name": "function",
      "version": "1.0.0",
      "main": "main.js",
      "dependencies" : {
    		    "lorem-ipsum" : "2.0.8"
     	}
    }
    ```
    {: codeblock}


3. Create your files as a Function in {{site.data.keyword.codeengineshort}}. Both of previous files must be accessible in the repository. If they are in a private repository, create [private code repository access](/docs/codeengine?topic=codeengine-code-repositories) and then provide that value with the `--build-git-repo-secret` option. If your files are located in a directory other than main, provide the path to the directory with the `--build-context-dir` option. 
  
    ```sh
    ibmcloud ce fn create -n nodelorem -runtime nodejs-18 --build-source GITHUB_DIR
    ```
    {: pre}
  
4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a passage of `lorem ipsum`.

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

### Including modules for a Python function
{: #function-python-dep-repo}

Create a function that includes a dependency for a specific Python module by creating a `requirements.txt` file. In this case, both the source code and requirements file are located in the same folder.

1. Create your Function by saving your code into a `__main__.py` file 

    ```py
    from lorem_text import lorem


    def main(params):
         words = 10

         return {
              "headers": {
                  "Content-Type": "text/plain;charset=utf-8",
              },
              "body": lorem.words(words),
          }
    ```
    {: codeblock}

2. Create a `requirements.txt` containing your required dependencies for your Function

    ```sh
    lorem-text
    ```
    {: codeblock}
  

3. Create your files as a function in {{site.data.keyword.codeengineshort}}. Both of previous files must be accessible in the repository. If they are in a private repository, create [private code repository access](/docs/codeengine?topic=codeengine-code-repositories) and then provide that value with the `--build-git-repo-secret` option. If your files are located in a directory other than main, provide the path to the directory with the `--build-context-dir` option.
  
    ```sh
    ibmcloud ce fn create -n pylorem -runtime python-3.11 --build-source GITHUB_DIR
    ```
    {: pre}
    
4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a passage of `lorem ipsum`.
 

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

## Next steps
{: #nextsteps-funsource}

- After your function is created, you can access your function by clicking **Test function** in the console or finding the URL for your function with the [**`function get`**](/docs/codeengine?topic=codeengine-cli#cli-function-get) command.

- You can create a [custom domain mapping](/docs/codeengine?topic=codeengine-domain-mappings) and assign it to your function.  

- After your function is created and deployed, you can update the function to meet your needs from the console or by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

After your function is created, you can update your function and its referenced code by using *any* of the following ways, independent of how you created or previously updated your function:

- If you have an existing code bundle, then you need to provide only a reference to the image, which points to the location of your container registry when you deploy your app. For more information, see [Creating function workloads from existing code bundles](/docs/codeengine?topic=codeengine-fun-create-existing).

    If you created your function by using the **`function create`** command and you specified the `--build-source` option to build the code bundle from local or repository source, and you want to change your function to point to a different code bundle, you must first remove the association of the build from your function. For example, run `ibmcloud ce function update -n FUN_NAME --build-clear`. After you remove the association of the build from your function, you can update the function to reference a different image. 
    {: note}

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} to build the code bundle from your source and create your function with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code bundle to {{site.data.keyword.registrylong}}. To learn more, see [Creating your function from repository source code](/docs/codeengine?topic=codeengine-fun-create-repo).

- If you are starting with source code that resides on a local workstation, you can choose for {{site.data.keyword.codeengineshort}} to build the code bundle from your source and create your function with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your source code and code bundle to {{site.data.keyword.registrylong}}. 

    For example, you might choose for {{site.data.keyword.codeengineshort}} to build your local source while you evolve the development of your source for the function. Then, after the code bundle is matured, you can update your function to reference the specific code bundle that you want. You can repeat this process as needed.



Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}




