---

copyright:
  years: 2025
lastupdated: "2025-03-27"

keywords: service access, trusted profiles, authenication file, authenticate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Enabling your component code to authenticate trusted profiles
{: #trusted-profiles-authentication-file}

After you [enable trusted profile support for your {{site.data.keyword.codeengineshort}} application, function, or job](/docs/codeengine?topic=codeengine-trusted-profiles), an additional file is automatically available in the file system where your code runs: `/var/run/secrets/codeengine.cloud.ibm.com/compute-resource-token/token`.
{: shortdesc}

This file contains a compute resource token that identifies your {{site.data.keyword.codeengineshort}} component. Read this file's content and use it for the [IAM API call to create an access token based on that compute resource token](/apidocs/iam-identity-token-api#gettoken-crtoken). Provide the identity (name or identifier) of the trusted profile that you want to use. You can then use the resulting access token to complete actions that the trusted profile grants.

For Go, Java, Node, and Python, an SDK is available that handles the token retrieval and refreshes it for you. The authenticator that you need from those libraries is called `ContainerAuthenticator` and are available in Git:

* For the Go SDK, see [https://github.com/IBM/go-sdk-core](https://github.com/IBM/go-sdk-core) {: external}
* For the Java SDK, see [https://github.com/IBM/java-sdk-core](https://github.com/IBM/java-sdk-core) {: external}
* For the Node SDK, see [https://github.com/IBM/node-sdk-core](https://github.com/IBM/node-sdk-core) {: external}
* For the Python SDK, see : [https://github.com/IBM/python-sdk-core](https://github.com/IBM/python-sdk-core) {: external}
