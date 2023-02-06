---

copyright:
  years: 2023, 2023
lastupdated: "2023-02-06"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud functions on {{site.data.keyword.codeengineshort}}
{: #functions}

A function is a stateless code snippet that performs one specific task in response to a HTTP request or event from other IBM Cloud or third-party services. With  Cloud functions, you can run your business logic in a scalable and serverless way. IBM Functions on {{site.data.keyword.codeengineshort}} provides an optimized runtime environment to support low latency and rapid scale-out scenarios. While your function code can use any OpenWhisk compatible runtime environment, functions written in Node.js, Golang, or Python are optimized to run in {{site.data.keyword.codeengineshort}}. 
{: shortdesc}

## Cloud function for Node.js
{: #functions-example}

A function written for the Node.js runtime may look like this:

```javascript
async function main(params) {
    console.log(process.env);
    console.log(params.__ow_headers);
    console.log("params: "+params);
    return { 
        statusCode: 200, 
        headers: { 'Content-Type': 'application/json' }, 
        body: params };
}module.exports.main = main;
```
{: codeblock}

Cloud functions are invoked calling http on the same Code Engine Endpoint URL, just like any other CodeEngine application.

```sh
curl -v https://action-nodejs.v4aij9h6oqz.dev-serving.codeengine.dev.appdomain.cloud/echome?param=abc
```
{: pre}
