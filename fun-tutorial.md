---

copyright:
  years: 2023, 2023
lastupdated: "2023-07-21"

keywords: function tutorial for code engine, function, functions in code engine, creating functions, tutorial for code engine

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Running a function from local source
{: #fun-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, run a Function with the {{site.data.keyword.codeengineshort}} CLI from code on your local system
{: shortdesc}

A Function is a stateless code snippet that performs tasks in response to an HTTP request. With IBM Code Engine Functions, you can run your business logic in a scalable and serverless way. IBM Code Engine Functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your Function code can be written in a managed runtime that includes specific [Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime) versions.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Set up your environment
{: #fun-tutorial-envirn}
{: step}
  
1. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```txt
    ibmcloud login -r us-south
    ```
    {: pre}
    
2. Target a resource group by running the following command. To see a list of your resource groups, run **`ibmcloud resource groups`**.

    ```txt
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    Example output

    ```txt 
    Targeted resource group default
    ```
    {: screen}

3. Create a project in {{site.data.keyword.codeengineshort}} called `sample`.

    ```txt
    ibmcloud ce project create --name sample
    ```
    {: pre}
    
    Example output
    
    ```txt
    Creating project 'sample'...
    ID for project 'sample' is 'abcdabcd-abcd-abcd-abcd-abcd12e3456f7'.
    Waiting for project 'sample' to be active...
    Now selecting project 'sample'.
    OK
    ```
    {: screen}
   
    Notice that your project is also selected for context, so all subsequent application-related commands are within the scope of this new `sample` project.

4. Become familiar with Functions commands by viewing the command options.

    ```txt
    ibmcloud ce fn --help
    ```
    {: pre}
  
## Create the source code
{: #fun-tutorial-sourcecode}
{: step}

Create a Node.js source file called `funhello.js` with the following sample code.
	
```javascript
  function main(params) {
      var msg = 'You did not tell me who you are.';
      if (params.name) {
          msg = `Hello, ${params.name}!`
       } else {
          msg = `Hello, Functions on CodeEngine!`
      }
      return {
          headers: { 'Content-Type': 'text/html; charset=utf-8' },
          body: `<html><body><h3>${msg}</h3></body></html>`
       }
  }
  
  module.exports.main = main;
```
{: codeblock}


## Create your function
{: #fun-tutorial-create}
{: step}
  

Create the Function from the `funhello.js` file.
	
```txt
ibmcloud ce fn create --name funhello --runtime nodejs-18 --build-source funhello.js
```
{: pre}

Command output
```txt
Preparing function 'funhello' for build push...
Creating function 'funhello'...
Packaging files to upload from source path 'hello.js'...
Submitting build run 'funhello-run-230623-090738611'...
Creating image 'private.stg.icr.io/ce--8a6a0-13c66hbi3rhz/function-funhello:230623-1407-s8kzr'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n funhello-run-230623-090738611' to check the build run status.
Waiting for function 'funhello' to become ready...
Function 'funhello' is ready.
OK                                                
Run 'ibmcloud ce function get -n funhello' to see more details.

https://funhello.13c66hbi3rhz.us-south.codeengine.appdomain.cloud
```
{: screen}


After the Function invocation URL becomes available, use the following command to find information about the Function.
  
```txt
ibmcloud ce fn get -n funhello
```
{: pre}

Let's take a deeper look at the previous **`function create`** command. Notice that the output of the **`function create`** command provides information about the progression of the build run before the function is created and deployed.

1. {{site.data.keyword.codeengineshort}} receives a request to create an function from source code. 
2. {{site.data.keyword.codeengineshort}} checks for an IAM service ID and API key that is associated with the selected project. This service ID must be authorized to read and write to {{site.data.keyword.registrylong_notm}}. If no service ID exists, {{site.data.keyword.codeengineshort}} creates one for you. Note that this service ID is used for subsequent {{site.data.keyword.codeengineshort}} build requests that are run from the same project.
3. This example builds code from a local source (`--build-source`). The source code (`hello.js`) is packed into a code-bundle file and uploaded to a managed namespace within the {{site.data.keyword.registrylong_notm}} instance in your account. Note that you can target only {{site.data.keyword.registrylong_notm}} for your local builds. For more information about IBM Container Registry, including information about quota limits and access, see [Getting started with IBM Cloud Container Registry](/docs/Registry?topic=Registry-getting-started).
4. {{site.data.keyword.codeengineshort}} builds your source code into a code bundle. The source code bundle is created in the same namespace as your source archive file.
5. After the build completes, your function is deployed. You can access your function from the provided URL.
	
## Invoke your function
{: #fun-tutorial-invoke}
{: step}

Invoke the Function URL by pasting it into a browser window. You can also use the `curl` command in your command line.
  
```txt
Hello, Functions on CodeEngine!
```
{: screen}

You successfully created and invoked a {{site.data.keyword.codeengineshort}} Function!

## Provide parameters for your function
{: #fun-tutorial-parameters}
{: step}	

Invoke the Function URL with a parameter by adding `?name=Sunshine` to the end of the URL and pasting it into a browser window.

```txt
https://funhello.13c66hbi3rhz.us-south.codeengine.appdomain.cloud?name=Sunshine
```
{: pre}

```txt
Hello, Sunshine!
```
{: screen}

## Clean up
{: #fun-tutorial-clean-up}


You can delete your function with the following command.

```txt
ibmcloud ce fn delete -n funhello
```
{: pre}

When you delete your function, the associated build files are also deleted.

Lastly, delete the code bundle that the build created from {{site.data.keyword.registrylong_notm}}. 

1. Navigate to [**Registry**](https://cloud.ibm.com/registry/start){: external} in the {{site.data.keyword.cloud_notm}} console.
2. Find the code bundle that are associated with your function by searching for your function name.
3. Select the code bundle and **Delete**.

## Next steps
{: #fun-tutorial-nextsteps}


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


