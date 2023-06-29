---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-29"

keywords: functions in code engine, function workloads, function local source, create function local source, create function

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating Function from local source code
{: #fun-create-local}


You can create your {{site.data.keyword.codeengineshort}} function directly from source code on your local workstation with the {{site.data.keyword.codeenginefull}} CLI. Use the **`fun create`** command to both build a code bundle from your local source, and deploy your function to reference this built code bundle.
{: shortdesc}


When you submit a build that pulls code from a local directory, your source code is packed into an archive file. {{site.data.keyword.codeengineshort}} automatically uploads the code bundle to an {{site.data.keyword.registrylong}} namespace in your account, and then creates and deploys your function to reference this built code bundle. Note that you can only target {{site.data.keyword.registrylong_notm}} for your local builds. For this scenario, you need to provide only a name for the function and the path to the local source. For a complete listing of options, see the [**`ibmcloud ce fun create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.  

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

You can choose to ignore certain file patterns from within your source code by using the `.ceignore` file, which behaves similarly to a `.gitignore` file. For example, entries for a `.ceignore` file for a Node.js function might include `node_modules` and `.npm`. For more sample file patterns to ignore, see the [GitHub .gitignore repository](https://github.com/github/gitignore){: external}.


{{site.data.keyword.registrylong}} is required for this scenario.
{: important}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Before you work with local source, make sure that your source is in an accessible location on your local workstation.  

## Creating a function from local source code with the CLI
{: #fun-create-local-cli}

This example uses the following Node.js code, saved as a `main.js` file. You can substitute your own code.


```javascript
async function main(params) {
    console.log(process.env);
    console.log(params.__ce_headers);
    console.log("params: "+params);
    return { 
        statusCode: 200, 
        headers: { 'Content-Type': 'application/json' }, 
        body: params };
}

module.exports.main = main;
```
{: codeblock}


1. Change to the directory that contains the `main.js` file or record the path to it. 

2. Create a function called `myfun-local` that uses a the `main.js` file as source. This command automatically builds and pushes the code bundle to a {{site.data.keyword.registryshort}} namespace in your account. If you do not have an existing {{site.data.keyword.registryshort}} namespace, {{site.data.keyword.codeengineshort}} automatically creates one for you.

    ```txt
    ibmcloud ce fn create --name myfun-local --runtime nodejs-18 --build-source main.js
    ```
    {: pre}

    Example output

    ```txt
    Preparing function 'myfun-local' for build push...
    Creating function 'myfun-local'...
    Packaging files to upload from source path 'main.js'...
    Submitting build run 'myfun-local-run-230123-111011111'...
    Creating image 'icr.io/ce--abcde-glxo4kabcde/function-myfun-local:230123-1650-yrj86'...
    Waiting for build run to complete...
    Build run status: 'Running'
    Build run completed successfully.
    Run 'ibmcloud ce buildrun get -n myfun-local-run-230626-115011911' to check the build run status.
    Waiting for function 'myfun-local' to become ready...
    Function 'myfun-local' is ready.
    OK                                                
    Run 'ibmcloud ce function get -n myfun-local' to see more details.

    https://myfun-local.glxo4kabcde.us-south.codeengine.test.appdomain.cloud
    ```
    {: screen}

    Notice the output of the **`function create`** command provides information on the progression of the build run before the function is created. 
    {: tip}

    In this example, the built code-bundle is uploaded to the `ce--abcde-glxo4kabcde` namespace in {{site.data.keyword.registryshort}}. 

    The following table summarizes the options that are used with the **`fn create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.

    | Option | Description |
    | -------------- | -------------- |
    | `--name` | The name of the function. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). | 
    | `--build-source` | The path to the local source. |
    | `--runtime` | The runtime to use for this function. |
    {: caption="Table 1. Command description" caption-side="bottom"}

4. Use the **`function get`** command to display information about your app, including information about the build.

    ```txt
    ibmcloud ce function get --name myfun-local
    ```
    {: pre}

    Example output

    ```txt
    Getting function 'myfun-local'...
    OK
    
    Name:          myfun-local  
    Project Name:  sample  
    Project ID:    abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
    Age:           5m41s  
    Created:       2023-06-26T16:50:14Z  
    URL:           https://myfun-local.glxo4kabcde.us-south.codeengine.test.appdomain.cloud  
    Status:        Ready  

    Resources:    
      CPU:                 0.25  
      Memory:              500M  
      Max Execution Time:  60 seconds  

    Build Information:    
      Build Run Name:     myfun-local-run-230123-111011111 
      Build Type:         local  
      Build Strategy:     codebundle-nodejs-18  
      Timeout:            600  
      Source:             main.js  
                      
      Build Run Summary:  Succeeded  
      Build Run Status:   Succeeded  
      Build Run Reason:   All Steps have completed executing  
      Run 'ibmcloud ce buildrun get -n myfun-local-run-230123-111011111' for details.  

    Function Code:    
      Runtime:        nodejs-18 (managed)  
      Bundle Secret:  ce-auto-icr-us-south  
      Code Bundle:    cr://icr.io/ce--abcde-glxo4kabcde/function-myfun-local:230123-1650-yrj86  
      Main:           main() 
    ```
    {: screen}

## Including dependencies for your Function
{: #fun-package}

You can create Functions in many different programming languages. When your Function code grows complex, you can add code modules as dependencies for your Function. Each language has its own modules to use with your Function code. For example, Node.js dependencies are usually existing `npm` modules, whereas Python uses Python packages. These dependencies must be declared and created in a file with your source code

### Including modules for a Node.js Function
{: #function-nodejs-ce}

Create a function that includes a dependency for a specific Python module by creating a `package.json` file. In this case, both the source code and package file are located in the same folder.

1. Create your source code by writing your code into a `main.js` file. For example, copy the following code example into a file called `main.js`.

    ```javascript
    function main(args) {
	  	  const oneLinerJoke = require('one-liner-joke');
	  	  let getRandomJoke = oneLinerJoke.getRandomJoke();

  		  return {
              	headers: { 'Content-Type': 'text/plain;charset=utf-8' },
          	    body: getRandomJoke
      	}
    }

    module.exports.main = main;
    ```
    {: codeblock}
  
2. Create a `package.json` file that contains the required dependencies for your Function. For the previous code example, use the following contents for your `package.json` file.

    ```sh
    {
	    "main": "main.js",
    	"dependencies" : {
   		"one-liner-joke" : "1.2.2"
     	}
    }
    ```
    {: codeblock}


3. Create your files as a Function in {{site.data.keyword.codeengineshort}}. In this case, you are in the directory where the local files exist so you can use `.` as the build source.
  
    ```sh
    ibmcloud ce fn create -n nodejokes -runtime nodejs-18 --build-source .
    ```
    {: pre}
  
4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a random joke!

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

### Including modules for a Python Function
{: #function-python}

Create a function that includes a dependency for a specific Python module by creating a `requirements.txt` file. In this case, both the source code and requirements file are located in the same folder.

1. Create your Function by saving your code into a `__main__.py` file 

    ```py
    import pyjokes
    def main(params):
	    return {
	    	      "headers": { 'Content-Type': 'text/plain;charset=utf-8' },
	    	      "body": pyjokes.get_joke()
    	}
    ```
    {: pre}

2. Create a `requirements.txt` containing your required dependencies for your Function

    ```sh
    pyjokes==0.6.0
    ```
    {: pre}
  

3. Create your files as a Function in {{site.data.keyword.codeengineshort}}. In this case, you are in the directory where the local files exist so you can use `.` as the build source.
  
    ```sh
    ibmcloud ce fn create -n pyjokes -runtime python-3.11 --build-source .
    ```
    {: pre}
    
 4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a random joke!
 

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

## Next steps
{: #nextsteps-funruncr}

Now that your function is created and deployed from local source code, you can update the function to meet your needs by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

When your function is deployed from local source or from [repository source code](/docs/codeengine?topic=codeengine-app-source-code) from the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted.  Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.  
{: note}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}



