---

copyright:
  years: 2023, 2025
lastupdated: "2025-07-01"

keywords: functions in code engine, function workloads, function inline

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating function workloads with inline code
{: #fun-create-inlinecode}

You can create your function with inline code. Your code is stored with your function. You can create this type of function from the console or with the CLI.
{: shortdesc}

A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image.


## Creating a function with inline with the console
{: #fun-create-inline-console}

Create a function with inline code from the console.
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Let's go**.
3. Select **Function**.
4. Enter a name for the function; for example, `myfunction`. Use a name for your function that is unique within the project.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must select a project to create a function.
6. Select a **Runtime image** for your function code. For more information, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime).
7. Select to **Specify your code as an inline code bundle**. When you select this option, your function is created with a sample code bundle for the selected runtime. You can edit the sample code after the function is created. The code bundle is stored inline with the function.
8. Specify your resource information, including [CPU and memory combinations](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo) and [Scale down delay](/docs/codeengine?topic=codeengine-fun-work#functions-scale).
9. Optionally, specify a [custom domain](/docs/codeengine?topic=codeengine-fun-domainmapping) or [environment variables](/docs/codeengine?topic=codeengine-envvar). You can add these options later.
10. Click **Create**.
11. After the function status changes to **Ready**, you can test the function. Click **Test function** and then click **Send request**. To open the function in a web page, click **Function URL**.
12. You can also change your function code in the Editor window. When you redeploy your function, the code is stored inline.

You can invoke your function by clicking **Test function** and then **Send request**.

You can retrieve the code that was used to create any inline function by running the **`function get`** command with the `--save` options. For example, `ibmcloud ce function get --name myfunction
 --save hellofun2.js`.
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
/**
 * The `main` function is the entry-point into the function.
 * It has one optional argument, which carries all the
 * parameters the function was invoked with.
*/
async function main(params) {
  // log environment variables available to the function
  console.log(process.env);
  // log Code Engine system headers available to the function
  console.log(params.__ce_headers);
  // log all parameters for debugging purposes
  console.log("params: "+params);
  // since functions are invoked through http(s), we return an HTTP response
  return {
      statusCode: 200,
      headers: { 'Content-Type': 'application/json' },
      body: params };
}

// this step is necessary, if you gave your main function a different name
// we include it here for documentation purposes only
module.exports.main = main;
```
{: codeblock}


Create your function and include the code in the command. For example, use the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command to create the `myhellofun` function.

```txt
ibmcloud ce fn create --name myhellofun --inline-code main.js --runtime nodejs
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
