---

copyright:
  years: 2024
lastupdated: "2024-03-05"

keywords: api reference, api, Kubernetes configuration and code engine, CRD for code engine, CRD, custom resource definition, guid, kubernetes, authenticate, code engine api

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with the {{site.data.keyword.codeengineshort}} REST API 
{: #ceapi-getstart}

You can use the {{site.data.keyword.codeenginefull}} API to create and manage your {{site.data.keyword.codeengineshort}} entities. 
{: shortdesc}

## Setting up your API environment 
{: #ceapi-getstart-setup}

To work with the API to create and manage {{site.data.keyword.codeengineshort}} entities, set up your API environment.

Before you begin, [download and install the `jq` tool](https://jqlang.github.io/jq/){: external}, which is a lightweight and flexible command-line JSON processor. This tool makes it easier to work with JSON responses that you receive from {{site.data.keyword.codeengineshort}} API.

1. Set values for `region`, `api_key`, and `project_name` before you run the example Curl commands in the API. For example, 

    ```txt
    region=us-south
    api_key=YOUR_IBM_CLOUD_API_KEY
    project_name=MY_PROJECT_NAME
    ```
    {: pre}

    * To discover the {{site.data.keyword.cloud_notm}} region that you're logged in to, run the `ibmcloud region` command.
    * For more information about {{site.data.keyword.cloud_notm}} API keys, see [Managing user API keys](/docs/account?topic=account-userapikey).
    * For more information about {{site.data.keyword.codeengineshort}} projects, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).


2. Check that you have a valid {{site.data.keyword.iamlong}} (IAM) access token. For more information about IAM API, see [Create an IAM access token for a user or service ID by using an API key](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey){: external}.

    ```sh
    token=`curl -X POST "https://iam.cloud.ibm.com/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
      -d "apikey=${api_key}" \
      | jq .access_token -r`
    ```
    {: pre}

3. Use the authentication token and the variables that you defined in step 1 to retrieve the project ID of your project. In the following example, use `curl` with `jq` to parse the {{site.data.keyword.codeengineshort}} API response and save the project ID in a variable. For example, 

    ```sh
    project_id=`curl -X GET "https://api.${region}.codeengine.cloud.ibm.com/v2/projects" \
       -H "Authorization: ${token}" \
       | jq --arg project_name ${project_name} '.projects[] | select(.name == $project_name) | .id' -r`
    ```
    {: pre}

## Working with a {{site.data.keyword.codeengineshort}} application in the API 
{: #ceapi-getstart-workapps}

Now that your {{site.data.keyword.codeengineshort}} API environment is set up, you are ready to work with {{site.data.keyword.codeengineshort}} entities, such as applications or jobs. In the following scenario, let's create an application, access it, and then delete the application. 

1. Create an app. Use the previously set variables and the project ID to construct a URL and send a request to create the `my-app` application. For example, 
  
    ```sh
    curl -X POST "https://api.${region}.codeengine.cloud.ibm.com/v2/projects/${project_id}/apps" \
      -H "Authorization: ${token}" \
      -H "Content-Type: application/json" \
      -d '{
        "name": "my-app",
        "image_reference": "icr.io/codeengine/helloworld"
      }'
    ```
    {: pre}

2. To display details about the `my-app` application, send a `GET` request. Be sure to reference the name of your app. Note that the last line of `jq` is optional, though it makes the output more readable.   

    ```sh
    curl -X GET "https://api.${region}.codeengine.cloud.ibm.com/v2/projects/${project_id}/apps/my-app" \
      -H "Authorization: ${token}" \
      -H "Content-Type: application/json" \
      | jq .
    ```
    {: pre}

3. To delete the application, send the request again but this time, use the `DELETE` method instead of the `GET` method. 

    ```sh
    curl -X DELETE "https://api.${region}.codeengine.cloud.ibm.com/v2/projects/${project_id}/apps/my-app" \
      -H "Authorization: ${token}" \
      -H "Content-Type: application/json"
    ```
    {: pre}

4. (Optional) If you send another `GET` request to retrieve information about `my-app`, then you receive a `404 error` because the resource no longer exists. 

Example output

```json
{
  "errors": [
    {
      "code": "resource_not_found",
      "message": "Resource not found."
    }
  ],
  "trace": "codeengine-api-34dc0040429941de8c9e02f0f1200af1",
  "status_code": 404
}
```
{: screen}


## Next steps
{: #ceapi-getstart-next}

Now that you have setup your environment and taken the first steps with a {{site.data.keyword.codeengineshort}} application with the API, are you ready to further explore the {{site.data.keyword.codeengineshort}} API?

For more information and examples for {{site.data.keyword.codeengineshort}} SDKs in several languages, see the [{{site.data.keyword.codeengineshort}} API documentation](https://cloud.ibm.com/apidocs/codeengine/v2){: external}.

To start working with {{site.data.keyword.codeengineshort}} components with the API, see

* [Create a project](https://cloud.ibm.com/apidocs/codeengine/v2#create-project){: external} 
* [Create an application](https://cloud.ibm.com/apidocs/codeengine/v2#create-app){: external} 
* [Create a job](https://cloud.ibm.com/apidocs/codeengine/v2#create-job){: external} or [Create a job run](https://cloud.ibm.com/apidocs/codeengine/v2#create-job-run){: external}



{{site.data.keyword.codeenginefull}} is designed so that you do not need to interact with the underlying technology it is built upon. However, if you have existing tools that are based on Kubernetes or Knative, you can still use it with {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} supports the Knative and Kubernetes APIs and their CLI commands. For more information, see [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes) and [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes).


