---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-23"

keywords: code engine, function, create function, code engine function, create code engine function

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with functions
{: #fun-work}

A function is a stateless code snippet that performs tasks as it is invoked by HTTP requests. With IBM Code Engine functions, you can run your business logic in a scalable and serverless way. IBM Code Engine functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your function code can be written in a managed runtime that includes specific [Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime) versions.
{: shortdesc}

A code bundle is a collection of files that represents your function code. This code bundle is injected into the runtime container. Your code bundle is created by {{site.data.keyword.codeengineshort}} and is stored in container registry or inline with the function. A code bundle is not a Open Container Initiative (OCI) standard container image.

Before you begin

- If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}.
- If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} function component.

Not sure what type of {{site.data.keyword.codeengineshort}} workload to create? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}

## Function limitations
{: #fun-limitations}

- No support for subscribing to event producers.
- No support for Terraform.

## How do I make my code run as a {{site.data.keyword.codeengineshort}} function component?
{: #fun-codebundle}

Whether your code exists as source in a local file or in a Git repository, or your code is an existing code bundle that is located in a public or private registry, {{site.data.keyword.codeengineshort}} provides a streamlined way for you to run your code as a function.

- If you are starting with source code that is located in a Git repository, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the code bundle from your source and creating the function with a single operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code to {{site.data.keyword.registrylong}}. To learn more, see [Creating a function from repository source code](/docs/codeengine?topic=codeengine-fun-create-repo).

- If you are starting with source code on a local workstation, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the image from your source and creating the function with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code to {{site.data.keyword.registrylong}}. To learn more, see [Creating your function from local source code with the CLI](/docs/codeengine?topic=codeengine-fun-create-local).

- If you are starting with source code, you can also run your source code inline. In this scenario, you paste in your source code when you create your function. For more information, see [Creating your function with inline code](/docs/codeengine?topic=codeengine-fun-create-inlinecode).


After you create and run your function, you can also update your function by using *any* of the preceding ways, independent of how you created or previously updated your function.

## What happens when I invoke my function?
{: #functions-invoke}

When a function is invoked (started), the corresponding Function instance is initialized with the configured Runtime container and Resource parameters. The process of the first initialization is referred to as *cold start*.

To reduce the cold start latency, {{site.data.keyword.codeengineshort}} optimizes the invocation by pre-warming certain runtimes with specific CPU and memory configurations. Pre-warmed combinations for functions include Node.js 18 and Python 3.11 versions as well as the default CPU and memory combination for Functions, which is 0.25 vCPU x 1 GB of memory. In addition, the system is designed to improve the reuse of Function instances that are already initialized. Therefore, a Function instance is kept alive after the invocation is finished to allow subsequent invocations by reusing the same instance and reusing the state of the instance when the last invocation completed. The reuse of a Function instance is not guaranteed.


## Can I keep my function instance alive longer?
{: #functions-scale}

With {{site.data.keyword.codeengineshort}}, your function scales up and down automatically, based on workload. When you create your function with the default CPU and memory combination, your function is injected into a "pre-warmed" container, which is optimized for use. When you create a function with a CPU and memory combination other than the default combination, then your function is injected into a new container. By default, this container is kept alive for only a short amount of time after the function completes. For more information, see [Supported CPU and memory combinations for functions](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo).

You can change the amount of time that your container is kept alive with the `--scale-down-delay` option in the CLI or the **Scale-down delay** option in the console. Note that while keeping your container alive reduces the cold start times for any subsequent run of your function, you are also billed for the amount of time that the custom function container exists.


## Requests and responses
{: #functions-request}

Functions are invoked with the HTTP protocol. When you invoke your function, you can specify the custom request parameters, custom request body and headers, as well as the HTTP method. The request parameters are made available to the function code as input parameters. The function code can set the response body, response headers, and response code, which are returned to the caller from the functions endpoint.

### Example 1: Generating an HTML response from a function
{: #functions-response1}

The following example illustrates how to generate an HTML response from a function.

```javascript
  function main(params) {
      var msg = 'You did not tell me who you are.';
      if (params.name) {
          msg = `Hello, ${params.name}!`
       } else {
          msg = `Hello, FaaS on CodeEngine!`
      }
      return {
          headers: { 'Content-Type': 'text/html; charset=utf-8' },
          body: `<html><body><h3>${msg}</h3></body></html>`
       }
  }

  module.exports.main = main;
```
{: screen}

### Example 2: Setting a response code and response header
{: #functions-response2}

Your function can set a specific response code and header flags. The following example illustrates how you can set a response code and response header to add a redirect to a different URL.


```javascript
function main(params) {
    return {
        headers: { location: 'https://cloud.ibm.com/docs/codeengine' },
        statusCode: 302
    }
}
```
{: screen}

### Example 3: Generating a plain text response from a function
{: #functions-response3}

The following example illustrates how to generate a plain text response from a function.

```javascript
function main(params) {
    var msg = 'You did not tell me who you are.';
    if (params.name !== "") {
        msg = `Hello, ${params.name}!`
    }
    return {
        headers: { 'Content-Type': 'text/plain;charset=utf-8' },
        body: `${msg}`
    }
}
```
{: screen}




## Error handling and debugging
{: #functions-error}

Function invocations can return system or application errors. For example, system errors indicate that the function code did not execute successfully, while application errors indicate a problem in the function code itself.

When a system error occurs, an HTTP response code similar to the following codes is returned.

| Code | Description |
| ---- | ------ |
| 409 | The resources that are required by the function was not satisfied. |
| 413 | The request payload exceeds the defined maximum. |
| 414 | The invocation URI is too long. |
| 416 | The function generated a response that exceeds the defined maximum. |
| 422 | The function code could not be loaded from a specified source. |
| 429 | You exceeded your resource quota, could not schedule the function. |
| 431 | The request headers exceed the defined maximum. |
| 500 | Internal server error. |
| 502 | Bad gateway. |
| 503 | Function currently unavailable, please try again later. |
| 507 | Insufficient storage to load the function. |
{: caption="Table 1. HTTP response codes" caption-side="bottom"}


If {{site.data.keyword.codeengineshort}} can execute the functions code, it responds to the invocation with one of the following status codes.

| Code | Description |
| ---- | ------ |
| 200 | Function invocation accepted, the function will be executed delayed. |
| 202 | Function invocation accepted, the function will be executed asynchronously. |
| 299 | The function exceeded the specified or maximum runtime limit and was aborted. |
{: caption="Table 2. Status codes" caption-side="bottom"}

As a developer of a function, you can generate any arbitrary HTTP status code, even the ones listed previously. Therefore, a response header indicates that the status code was generated by the function code.

{{site.data.keyword.codeengineshort}} functions adds the following response headers to the function invocation response.

| Code | Description |
| ---- | ------ |
| `x-faas-actionstatus` | The HTTP status code set by the function program logic. |
| `x-faas-activation-id` | The unique ID to identify the function invocation. |
| `x-faas-result` | A `success` message or short error message that is returned by the Runtime container. |
| `x-faas-errormessage` | A long error message with additional details. |
| `x-faas-prewarmed` | A message that indicates whether the invocation was cold or if the function ran in an existing (pre-warmed container. Possible values are `false` or `true`. |
{: caption="Table 2. Status codes" caption-side="bottom"}


## Function data input/output characteristics
{: #functions-data}

To run your function in {{site.data.keyword.codeengineshort}}, your code must implement a runtime contract with the following characteristics.

- Must be callable from a public web app endpoint, so that it can be embedded with web pages and then invoked from any Code Engine Eventing source, a Web Browser, or any other HTTPS capable client.
- Must implement a `main` procedure as entry point. The `main` procedure can receive input parameters in form of a JSON formatted data structure and can return output parameters, also in form of a JSON formatted data structure.
- Can receive an optional sub path, so that the function can implement different flavors, based on the specified path. The function's `main` procedure receives the path as a `__ce_path` input parameter.
- Can receive optional query parameters, which can be used to configure the function at runtime. The function's `main` procedure receives the parameters as key-value pairs within the JSON formatted input data structure.
- Can receive request headers, so that client code can specify  accepted encodings.
- Can receive an optional content-type request header.
- Can receive an optional request payload (body), which the function processes at runtime. Depending on the selected request content-type, the data payload is passed to the function's main entry point, either in base 64 encoded form or "unfolded" as part of the JSON input data structure. Special characters in keys values pairs of `application/x-www-form-urlencoded` input are `percent-encoded` values.
- Can define an arbitrary HTTP status code (optional) that is then returned to the invoking client.
- Can set arbitrary response headers, such as a redirect location, a response encoding, or cookie values.
- Can return an arbitrary response body with a selected binary or non-binary encoding; for example, `application/octet-stream`, `application/json`, `text/*`, `image/*`, or `audio/*`. If no `content-type` response header is set, it defaults to `text/plain`.
- Supports the following request content-types: `application/x-www-form-urlencoded` (default), `text/plain`, `application/json`, `application/octet-stream`, `image/*`, `audio/*`
- Does not support the `multipart/form-data` request header.


## Options for visibility for a {{site.data.keyword.codeengineshort}} function
{: #optionsvisibilityfun}

With {{site.data.keyword.codeengineshort}}, you can determine the right level of visibility for your function by defining the endpoints, or system domain mappings that are available for receiving requests.
{: shortdesc}

Every function has an *internal* system domain mapping that is visible to all components within the same {{site.data.keyword.codeengineshort}} project, but not outside of the project. In addition to the internal system domain mapping, you choose to make the function visible to either the *public* internet or the {{site.data.keyword.cloud_notm}} *private* network.

You can deploy your function with the following visibility levels:

| Setting | Description |
| --------- | ------------------- |
| [internal (project)](#fun-endpoint-projectonly) | A function with this setting can receive requests from components in the same {{site.data.keyword.codeengineshort}} project. Setting an internal (project) endpoint means that your function is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the same {{site.data.keyword.codeengineshort}} project. This endpoint is always enabled. **IMPORTANT:** A function cannot invoke another job or app using the internal routes.|
| [public](#fun-endpoint-public) | A function with this setting is exposed to the internet and your {{site.data.keyword.codeengineshort}} project. Setting a public endpoint means that your function can receive requests from the public internet or from components within your {{site.data.keyword.codeengineshort}} project. This setting is the default. |
| [private](#fun-endpoint-private) | A function with this setting is exposed to the {{site.data.keyword.cloud_notm}} private network and your {{site.data.keyword.codeengineshort}} project. Setting a private endpoint means that your function is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services by using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project.|
{: caption="Table 1. Visibility for functions" caption-side="bottom"}

You can set the endpoint settings for visibility of a function from the console or with the CLI when you create and deploy, or update your function.

### Deploying your function with an internal endpoint
{: #fun-endpoint-projectonly}

You can set the endpoint visibility for your function to deploy with an internal (project) endpoint. When you set an internal (project) endpoint, your function is not accessible from the public internet and network access is possible only from other {{site.data.keyword.codeengineshort}} components that are running within the same {{site.data.keyword.codeengineshort}} project. This endpoint is always enabled. Functions are still accessible through shared components and therefore need to be secured.

For example, if your solution consists of several functions within a project, you might set up your solution so that only one of those functions is visible from the internet so that it handles incoming traffic. This public-facing function can delegate work to other functions in your solution so that they do not need to be visible from the internet.

With the CLI, set the endpoint visibility for your function so that it is deployed with a project endpoint by using the `--visibility=project` option on the [**`function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) or [**`function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. You can obtain the available URLs for your function that reflect your endpoint definition by using the [**`function get`**](/docs/codeengine?topic=codeengine-cli#cli-function-get) command.

From the console, set the visibility of endpoints for your function by using the **Endpoints** setting when you create your function. After your function is deployed, you can view and modify these system domain mapping settings on the **Domain mappings** tab on your Functions page.

A function with this setting can receive requests from components in the same {{site.data.keyword.codeengineshort}} project. However, a function cannot invoke another job or app using the internal routes.
{: important}

### Deploying your function with a public endpoint
{: #fun-endpoint-public}

When you deploy a function, by default, the function can receive requests from the public internet or from components within the same {{site.data.keyword.codeengineshort}} project. In this case, the function is deployed with a public endpoint.

### Deploying your function with a private endpoint
{: #fun-endpoint-private}

You can set the endpoint visibility for your function to deploy with a private endpoint. When you set a private endpoint for your function, it is not accessible from the public internet and network access is possible only from other {{site.data.keyword.cloud_notm}} services from virtual private endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).

For example, if your solution consists of a component that is running on an {{site.data.keyword.containerfull_notm}} Kubernetes cluster within your own virtual private endpoint and you want to access the {{site.data.keyword.codeengineshort}} function from the {{site.data.keyword.cloud_notm}} private network, you can set the visibility of the function to private. When the visibility of the function is set to private, the function is not accessible through the public internet. The function is still accessible from other functions within the project.

You can [create your function with a private endpoint](/docs/codeengine?topic=codeengine-vpe#using-vpes-fun) so that the function is exposed only through the {{site.data.keyword.cloud_notm}} private network and not exposed to the external internet. The function is still reachable through shared components from within the internal network and the function endpoint needs to be secured.

With the CLI, set the endpoint visibility for your function so that it is deployed with a private endpoint by using the `--visibility=private` option on the [**`function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) or [**`function update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) command. You can obtain the available URLs for your function that reflect your endpoint definition by using the [**`function get`**](/docs/codeengine?topic=codeengine-cli#cli-function-get) command.

From the console, set the visibility of endpoints for your function by using the **Endpoints** setting when you create your function. After your function is deployed, you can view and modify these system domain mapping settings on the **Domain mappings** tab on your Functions page.

For more information about connecting over private networks, see [Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe).



## Options for creating functions
{: #functions-options}

Learn about the options that you can specify when you create your function. Note that options can vary between the console and the CLI.
{: shortdesc}


### Memory and CPU
{: #functions-combo}

When you deploy your function, you can specify the amount of memory and CPU that your function can consume. These amounts can vary, depending on if your function is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

By default, your function is assigned 2 G of memory and 0.50 vCPU. For more information about other supported memory and CPU combinations, see [Supported memory and CPU combinations for functions](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo).


### Creating and running your function with environment variables
{: #functions-envvar}

You can define and set environment variables as key-value pairs that can be used by your function at run time.
{: shortdesc}

You can define environment variables when you create your function, or when you update an existing function with the CLI.

For more information about defining environment variables, see [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

{{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the function. For more information about automatically injected environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

### Creating and running your function when using secrets and configmaps
{: #functions-secconfigmap}

In {{site.data.keyword.codeengineshort}}, secrets and configmaps can be consumed by your function by using environment variables.
{: shortdesc}

Both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

Your function can use environment variables to fully reference a configmap (or secret) or reference individual keys in a configmap (or secret).

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap#configmap-ref).

## Considerations for functions quotas
{: #functions-quotas}

When you work with applications, functions, and batch jobs, these resources run within the context of a {{site.data.keyword.codeengineshort}} project. Resource quotas are defined on a per project basis, and limits apply for applications, functions, and batch jobs. 

For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).


## Next steps
{: #function-nextsteps}

Now that you are familiar with key concepts of working with {{site.data.keyword.codeengineshort}} functions, are you ready to create and work with functions? See the following topics.

* [Creating function workloads with inline code](/docs/codeengine?topic=codeengine-fun-create-inlinecode).
* [Creating function workloads with repository source code](/docs/codeengine?topic=codeengine-fun-create-repo).
* [Creating function workloads from local source code](/docs/codeengine?topic=codeengine-fun-create-local).

For more information about working with functions, see the following topics.

* [Function workloads](/docs/codeengine?topic=codeengine-cefunctions).
* [Integrating {{site.data.keyword.cloud_notm}} services with service bindings](/docs/codeengine?topic=codeengine-service-binding).
* Working with [environment variables](/docs/codeengine?topic=codeengine-envvar), [configmaps](/docs/codeengine?topic=codeengine-configmap), and [secrets](/docs/codeengine?topic=codeengine-secret).
* [Troubleshooting functions](/docs/codeengine?topic=codeengine-troubleshoot-function).
