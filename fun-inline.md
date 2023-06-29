---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-29"

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

Create a function with inline code with the console.
{: shortdesc} 
  


1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating**.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to create a function. 
3. Select **Functions**.
4. Enter a name for the function; for example, `hellofun`. Use a name for your function that is unique within the project. 
6. From the **Main settings**, choose a runtime. You can also set resources and optional settings. 
7. Click **Create**.
8. In the **Configuration** section, paste in your function code.
9. Click **Save**.

You can invoke your function by clicking **Test function** and then **Send request**.

You can save the code that was used to create any inline function by running the **`function get`** command with the `--save` options. For example, `ibmcloud ce function get --name hellofun --save hellofun2.js`.
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


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}



