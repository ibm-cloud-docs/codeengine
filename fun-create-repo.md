---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-28"

keywords: functions in code engine, function workloads, function source code, function git repository

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating Function workloads with repository source code
{: #fun-create-repo}


You can create your function directly from source code that is located in a Git repository with the {{site.data.keyword.codeenginefull}} CLI.
{: shortdesc}

Use the **`function create`** command to both build a code bundle from your Git repository source, and create your function to reference this built code bundle.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

In this scenario, {{site.data.keyword.codeengineshort}} builds a code bundle from your Git repository source, automatically uploads the code bundle to your container registry, and then creates your function to reference this built code bundle. You need to provide only a name for the function, the URL to the Git repository, and the runtime for the Function. In this case, {{site.data.keyword.codeengineshort}} manages the namespace for you. However, if you want to use a different container registry, then you must specify the code bundle and a registry secret for that container registry. For a complete listing of options, see the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.  

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

The following example **`function create`** command creates the `myfun` function, which references code that is located in `https://github.com/IBM/CodeEngine`. This command automatically builds the code bundle and uploads it to an {{site.data.keyword.registrylong}} namespace in your account. The function references this built code bundle. By specifying the `--build-context-dir` option, the build uses the source in the `helloworld` directory.  

```txt
ibmcloud ce function create --name myfun --build-source https://github.com/IBM/CodeEngine --build-context-dir /helloworld
```
{: pre}

Example output

```txt
Preparing function 'myfun' for build push...
Creating function 'myfun'...
Submitting build run 'myfun-run-110627-111124665'...
Creating image 'icr.io/ce--abcde-4svg40kna19/function-myfun:110627-2222-hjxl6'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myfun-run-110627-111124665' to check the build run status.
Waiting for function 'myfun' to become ready...
Function 'myfun' is ready.
OK                                                
Run 'ibmcloud ce function get -n myfun' to see more details.

https://myfun.13c66hbi3rhz.us-south.codeengine.appdomain.cloud
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
| `--build-context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. |
| `--runtime` | The runtime for the function. |
{: caption="Table 1. Command description" caption-side="bottom"}

The following output shows the result of the **`function get`** command for this example, including information about the build.

Example output

```txt
Getting function 'kerstenrepofunction'...
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
  Build Run Name:     myfun-run-110627-111124665  
  Build Type:         git  
  Build Strategy:     codebundle-nodejs-18  
  Timeout:            600  
  Source:             https://github.com/myrepo/test  
                      
  Build Run Summary:  Succeeded  
  Build Run Status:   Succeeded  
  Build Run Reason:   All Steps have completed executing  
  Run 'ibmcloud ce buildrun get -n myfun-run-110627-111124665' for details.  

Function Code:    
  Runtime:        nodejs-18 (managed)  
  Bundle Secret:  ce-auto-icr-us-south  
  Code Bundle:    cr://icr.io/ce--8a6a0-13c66hbi3rhz/function-kerstenrepofunction:230627-2107-wjxl6  
  Main:           main() 
```
{: screen}

Now that your function is created from repository source code, you can update the function to meet your needs by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

When your function is created from repository source code or from [local source](/docs/codeengine?topic=codeengine-fun-create-local) with the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted. Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.
{: note}


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


3. Create your files as a Function in {{site.data.keyword.codeengineshort}}. Both of previous files must be accessible in the repository. If they are in a private repository, create [private code repository access](/docs/codeengine?topic=codeengine-code-repositories) and then provide that value with the `--build-git-repo-secret` option. If your files are located in a directory other than main, provide the path to the directory with the `--build-context-dir` option.
  
    ```sh
    ibmcloud ce fn create -n nodejoke -runtime nodejs-18 --build-source GITHUB_DIR
    ```
    {: pre}
  
4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a random joke!

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

## Including modules for a Python Function
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
  

3. Create your files as a Function in {{site.data.keyword.codeengineshort}}. Both of previous files must be accessible in the repository. If they are in a private repository, create [private code repository access](/docs/codeengine?topic=codeengine-code-repositories) and then provide that value with the `--build-git-repo-secret` option. If your files are located in a directory other than main, provide the path to the directory with the `--build-context-dir` option.
  
    ```sh
    ibmcloud ce fn create -n pyjokes -runtime python-3.11 --build-source GITHUB_DIR
    ```
    {: pre}
    
 4. Invoke your Function by pasting the provided URL into a web browser. Your browser displays a random joke!
 

For more information about the `fn create` command and its options, see [Create a Function](/docs/codeengine?topic=codeengine-cli#cli-function-create).

## Next steps
{: #nextsteps-funsource}


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}




