---

copyright:
  years: 2023, 2023
lastupdated: "2023-10-17"

keywords: troubleshooting for code engine, troubleshooting network errors in code engine, tips for network errors with code engine, debugging network errors with code engine, connection errors, networking errors and code engine

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I getting ECONNRESET errors when connecting to an endpoint? 
{: #ts-other-econnreset}
{: troubleshoot}


When my {{site.data.keyword.codeengineshort}} app, job, or function makes an HTTP request to an endpoint, my connection fails and an `ECONNRESET` error is received.
{: tsSymptoms}

An `ECONNRESET` error can occur if keepalive settings in your HTTP client are not compatible with the settings on the destination server endpoint. How you configure your HTTP client depends on your programming language.
{: tsCauses}


You can resolve this issue by configuring keepalive settings in the client.
{: tsResolve}

For example, if you are using Node.js, you can use the [`agentkeepalive`](https://www.npmjs.com/package/agentkeepalive){: external} module. Configure your HTTP client to use this module and then configure the keepalive settings. 

For example, the following code snippet illustrates one way that you can configure keepalive settings in your HTTP client.



```javascript
[...]
import { HttpsAgent } from 'agentkeepalive';

const keepaliveAgent = new HttpsAgent({
    maxSockets: 100,
    maxFreeSockets: 10,
    timeout: 60000,
    freeSocketTimeout: 30000,
});
[...]
```
{: pre}

For more information, see [example for keepalive settings](https://github.com/node-modules/agentkeepalive#support-https){: external}.






