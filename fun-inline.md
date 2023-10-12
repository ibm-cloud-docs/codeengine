---

copyright:
  years: 2023, 2023
lastupdated: "2023-10-12"

keywords: functions in code engine, function workloads, function inline

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating Function workloads with inline code
{: #fun-create-inlinecode}

You can create your function with inline code. Your code is stored with your function. You can create this type of function from the console or with the CLI. 
{: shortdesc}




## Creating a function with inline with the console
{: #fun-create-inline-console}

Create a function with inline code from the console.
{: shortdesc} 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Let's go**.
3. Select **Functions**.
4. Enter a name for the function; for example, `myfunction`. Use a name for your function that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must select a project to create a function. 
6. Select a **Runtime image** for your function code. For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).
7. Select to **Specify your code as an inline code bundle**. When you select this option, your function is created with a sample code bundle for the selected runtime. You can edit the sample code after the function is created. The code bundle is stored inline with the function.
8. Specify your resource information, including [CPU and memory combinations](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo) and {Scale down delay](/docs/codeengine?topic=codeengine-fun-work#functions-scale). 
9. Optionally, specify a [custom domain](/docs/codeengine?topic=codeengine-fun-domainmapping) or [environment variables](/docs/codeengine?topic=codeengine-envvar). You can add these options later.
10. Click **Create**.
11. After the Function status changes to **Ready**, you can test the function. Click **Test function** and then click **Send request**. To open the function in a web page, click **Function URL**. 
12. You can also change your function code in the Editor window. When you redeploy your function, the code is stored inline.

You can invoke your function by clicking **Test function** and then **Send request**.

You can retrieve the code that was used to create any inline function by running the **`function get`** command with the `--save` options. For example, `ibmcloud ce function get --name hellofun --save hellofun2.js`.
{: tip}

## Creating a function with inline code with the CLI
{: #fun-create-inline-cli}

Create a function with inline code with the CLI by using the **`ibmcloud ce function create`** command. For a complete listing of options, see the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

This example uses a code file named `main.js`. You can use the following example code to create your `main.js` file or you can substitute your own code.
  
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


Create your function and include the code in the command. For example, use the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command to create the `myhellofun` function. 

```txt
ibmcloud ce fn create --name myhellofun --inline-code main.js --runtime nodejs-18
```
{: pre}


Example output

```txt
Creating function 'myhellofun'...
OK
Run 'ibmcloud ce function get -n myhellofun' to see more details.

https://myhellofun.glxo4kabcde.us-south.codeengine.appdomain.cloud
```
{: screen}

You can save the code that was used to create any inline function by running the **`function get`** command with the `--save` options. For example, `ibmcloud ce function get --name myhellofun --save hellofun2.js`.
{: tip}

## Next steps
{: #nextsteps-funinline}

Now that your function is created and deployed from local source code, you can update the function to meet your needs by using the [**`ibmcloud ce function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. If you want to update your source to use with your function, you must provide the `--build-source` option on the **`function update`** command.

When your function is deployed from local source or from [repository source code](/docs/codeengine?topic=codeengine-app-source-code) from the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted.  Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.  
{: note}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}




