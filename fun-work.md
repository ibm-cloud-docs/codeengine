---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-29"

keywords: code engine, function, create function, code engine function, create code engine function

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with Functions
{: #fun-work}

A Function is a stateless code snippet that performs tasks in response to an HTTP request. With IBM Code Engine Functions, you can run your business logic in a scalable and serverless way. IBM Code Engine Functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your Function code can be written in in Node.js or Python, which are optimized to run in IBM Code Engine Functions. In addition, your Function code can be written for any OpenWhisk compatible runtime environment or a custom runtime image. 
{: shortdesc}

Before you begin

- If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
- If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} Function component.

## Function limitations
{: #fun-limitations}

- Supported in Washington, D.C. (`us-east`), Frankfurt (`eu-de`), and Sydney (`au-syd`) regions only.
- No support for subscribing to event producers.
- No support for custom domains.
- No support for limiting the visibility of your function.

## How do I make my code run as a {{site.data.keyword.codeengineshort}} Function component?
{: #fun-containerimage}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides a streamlined way for you to run your code as a Function.

- If you are starting with source code that is located in a Git repository, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the code bundle from your source and creating the Function with a single operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code to {{site.data.keyword.registrylong}}. To learn more, see [Creating a Function from repository source code](/docs/codeengine?topic=codeengine-fun-create-repo). 

- If you are starting with source code on a local workstation, you can choose to point to the location of your source, and {{site.data.keyword.codeengineshort}} takes care of building the image from your source and creating the Function with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your code to {{site.data.keyword.registrylong}}. To learn more, see [Creating your Function from local source code with the CLI](/docs/codeengine?topic=codeengine-fun-create-local). 
  
- If you are starting with source code, you can also run your source code inline. In this scenario, you paste in your source code when you create your Function. For more information, see [Creating your Function with inline code](/docs/codeengine?topic=codeengine-fun-create-inlinecode).


After you create and run your Function, you can also update your Function by using *any* of the preceding ways, independent of how you created or previously updated your Function.

## Requests and responses
{: #functions-request}

Functions are invoked with the HTTP protocol. When you invoke your Function, you can specify the custom request parameters, custom request body and headers, as well as the HTTP method. The request parameters are made available to the Function code as input parameters. The Function code can set the response body, response headers, and response code, which are returned to the caller from the Functions endpoint. 

### Example 1: Generating an HTML response from a Function
{: #functions-request1}

The following example illustrates how to generate an HTML response from a Function.

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
{: #functions-request2}

Your Function can set a specific response code and header flags. The following example illustrates how you can set a response code and response header to add a redirect to a different URL.


```javascript
function main(params) {
    return {
        headers: { location: 'https://cloud.ibm.com/docs/codeengine' },
        statusCode: 302
    }
}
```
{: screen}

### Example 3: Generating a plain text response from a Function
{: #functions-request3}

The following example illustrates how to generate a plain text response from a Function.

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

Function invocations can return system or application errors. For example, system errors indicate that the function code did not execute successfully, while application errors indicate a problem in the Function code itself.

When a system error occurs, an HTTP response code similar to the following codes is returned.

| Code | Description |
| ---- | ------ | 
| 409 | The resources that are required by the Function could not be satisfied. | 
| 413 | The request payload exceeds the defined maximum. | 
| 414 | The invocation URI is too long. | 
| 416 | The Function generated a response that exceeds the defined maximum. |
| 422 | The Function code could not be loaded from a specified source. |
| 429 | You exceeded your resource quota, could not schedule the Function. |
| 431 | The request headers exceed the defined maximum. |
| 500 | Internal server error. |
| 502 | Bad gateway. |
| 503 | Function currently unavailable, please try again later. |
| 507 | Insufficient storage to load the Function or Image. | 
{: caption="Table 1. HTTP response codes" caption-side="bottom"}


If {{site.data.keyword.codeengineshort}} can execute the Functions code, it responds to the invocation with one of the following status codes.

| Code | Description |
| ---- | ------ | 
| 200 | Function invocation accepted, the Function will be executed delayed. |
| 202 | Function invocation accepted, the Function will be executed asynchronously. |
| 299 | The Function exceeded the specified or maximum runtime limit and was aborted. |
{: caption="Table 2. Status codes" caption-side="bottom"}

As a developer of a Function, you can generate any arbitrary HTTP status code, even the ones listed previously. Therefore, a response header indicates that the status code was generated by the Function code.

{{site.data.keyword.codeengineshort}} Functions adds the following response headers to the Function invocation response.

| Code | Description |
| ---- | ------ | 
| `x-faas-actionstatus` | The HTTP status code set by the Function program logic. |
| `x-faas-activation-id` | The unique ID to identify the Function invocation. |
| `x-faas-result` | A `success` message or short error message that is returned by the Runtime container. |
| `x-faas-errormessage` | A long error message with additional details. |
| `x-faas-prewarmed` | A message that indicates whether the invocation was cold or if the Function ran in an existing (pre-warmed container. Possible values are `false` or `true`. |
{: caption="Table 2. Status codes" caption-side="bottom"}


## Function data input/output characteristics
{: #functions-data} 
  
To run your Function in {{site.data.keyword.codeengineshort}}, your code must implement a runtime contract with the following characteristics.
	
- Must be callable from a public web app endpoint, so that it can be embedded with web pages and then invoked from any Code Engine Eventing source, a Web Browser, or any other HTTPS capable client.
- Must implement a `main` procedure as entry point. The `main` procedure can receive input parameters in form of a JSON formatted data structure and can return output parameters, also in form of a JSON formatted data structure.
- Can receive an optional subpath, so that the Function can implement different flavors, based on the specified path. The Function's `main` procedure receives the path as a `__ce_path` input parameter.
- Can receive optional query parameters, which can be used to configure the Function at runtime. The Function's `main` procedure receives the parameters as key-value pairs within the JSON formatted input data structure.
- Can receive request headers, so that client code can specify  accepted encodings. 
- Can receive an optional content-type request header.
- Can receive an optional request payload (body), which the Function processes at runtime. Depending on the selected request content-type, the data payload is passed to the Function's main entry point, either in base 64 encoded form or "unfolded" as part of the JSON input data structure. Special characters in keys values pairs of `application/x-www-form-urlencoded` input are percent-encoded.
- Can define an arbitrary HTTP status code (optional) that is then returned to the invoking client.
- Can set arbitrary response headers, such as a redirect location, a response encoding, or cookie values.
- Can return an arbitrary response body with a selected binary or nonbinary encoding; for example, `application/octet-stream`, `application/json`, `text/*`, `image/*`, or `audio/*`. If no content-type response header is set, it defaults to `text/plain`.
- Supports the following request content-types: `application/x-www-form-urlencoded` (default), `text/plain`, `application/json`, `application/octet-stream`, `image/*`, `audio/*`
- Does not support the `multipart/form-data` request header.


## Options for creating Functions
{: #functions-options} 

Learn about the options that you can specify when you create your Function. Note that options can vary between the console and the CLI.
{: shortdesc}


### Memory and CPU
{: #functions-combo}

When you deploy your Function, you can specify the amount of memory and CPU that your Function can consume. These amounts can vary, depending on if your app is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

By default, your Function is assigned 4 G of memory and .5 vCPU. For more information about selecting managed memory and CPU combinations, see [Runtimes](/docs/codeengine?topic=codeengine-fun-runtime). For more information about other supported memory and CPU combinations, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).


### Creating and running your app with environment variables 
{: #functions-envvar}

You can define and set environment variables as key-value pairs that can be used by your Function at run time. 
{: shortdesc}

You can define environment variables when you create your Function, or when you update an existing Function with the CLI. 

For more information about defining environment variables, see [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

{{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the Function. For more information about automatically injected environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

### Creating and running your Function when using secrets and configmaps 
{: #functions-secconfigmap}

In {{site.data.keyword.codeengineshort}}, secrets and configmaps can be consumed by your Function by using environment variables. 
{: shortdesc}

Both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

Your Function can use environment variables to fully reference a configmap (or secret) or reference individual keys in a configmap (or secret).

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap#configmap-ref).

## Considerations for Functions quotas
{: #functions-quotas}

When you work with applications, functions, and batch jobs, these resources run within the context of a {{site.data.keyword.codeengineshort}} project. Resource quotas are defined on a per project basis, and limits apply for applications, functions, and batch jobs. 

For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).



