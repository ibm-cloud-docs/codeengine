---

copyright:
  years: 2025
lastupdated: "2025-06-03"

keywords: lithops and code engine, lithops framework and code engine, Python and code engine, iam api key when using lithops for code engine, jobs in lithops framework with code engine, batch jobs in lithops framework with code engine, lithops, jobs

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Running jobs with Lithops framework
{: #lithops}

Lithops is an open source framework that designed to massively scale your Python applications. Lithops provides a simple push to the {{site.data.keyword.codeenginefull}} experience so that you can focus on your Python code, while Lithops focuses on the deployment of your code at massive scale while monitoring executions, obtaining results, and much more. Lithops enables native Python integration with Code Engine by using the Lithops API. For more information about Lithops, see [Lithops quick start guide](https://github.com/lithops-cloud/lithops#quick-start){: external}.
{: shortdesc}

## Running your first flow by using the Lithops framework
{: #first-lithops}

Before you can run jobs that reference the Lithops framework, you must first install Lithops and set up a storage backend.

Before you begin

- Install [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work](/docs/codeengine?topic=codeengine-manage-project) with a {{site.data.keyword.codeengineshort}} project.
- [Find and set your `kubeconfig` environment variable](/docs/codeengine?topic=codeengine-kubernetes).

### Installing Lithops
{: #install-lithops}

1. Install [Lithops](https://github.com/lithops-cloud/lithops#quick-start){: external}.
2. Create the [Lithops configuration file](https://github.com/lithops-cloud/lithops/tree/master/config#lithops-configuration){: external}.
3. Install [Docker (community edition) version](https://docs.docker.com/get-started/get-docker/){: external}. 
4. Log in to Docker.

    ```txt
    docker login
    ```
    {: pre}

### Setting up a storage backend for Lithops
{: #storage-lithops}

Select a [supported storage backend](https://github.com/lithops-cloud/lithops/tree/master/config#compute-and-storage-backends); for example, {{site.data.keyword.cos_full_notm}}. 

To set up {{site.data.keyword.cos_full_notm}}, 

1. Create an [{{site.data.keyword.cos_full_notm}} account](https://www.ibm.com/products/cloud-object-storage).
2. Create a bucket in the region that you want to use.
3. In the side navigation, click **Endpoints** to find your API endpoint. You must copy both the public and private endpoints of the region where you created your bucket.
4. Create the credentials to access to your {{site.data.keyword.cos_full_notm}} account. **Choose one option**

#### Option 1 (API key) for Lithops
{: #option1-storage}

1. From the {{site.data.keyword.cos_full_notm}} navigation, click **Service Credentials**.
2. Click **New credential +** and provide a name and select a role.
3. Click **Add** to generate service credential.
4. Click **View credentials** and copy the `apikey` value.
5. Edit your `lithops` config file and add the following keys.

    ```yaml
    lithops:
        storage_backend: ibm_cos

    ibm_cos:
        endpoint   : <REGION_ENDPOINT>  
        private_endpoint : <PRIVATE_REGION_ENDPOINT>
        api_key    : <API_KEY>
    ```
    {: pre}

#### Option 2 ({{site.data.keyword.cos_full_notm}} HMAC credentials) for Lithops
{: #option2-storage}

1. From the {{site.data.keyword.cos_full_notm}} navigation, click **Service Credentials**.
2. Click **New credential +** and provide a name and select a role.
3. Click **Advanced options** and enable the option `Include HMAC Credential`. 
4. Click **Add** to generate service credential.
5. Click **View credentials** and copy the `access_key_id` and `secret_access_key` values.
6. Edit your `lithops` config file and add the following keys:

    ```yaml
    lithops:
        storage_backend: ibm_cos

    ibm_cos:
        endpoint   : <REGION_ENDPOINT>  
        private_endpoint : <PRIVATE_REGION_ENDPOINT>
        access_key    : <ACCESS_KEY_ID>
        secret_key    : <SECRET_KEY_ID>
    ```
    {: pre}

#### Option 3 (IBM IAM API key) for Lithops
{: #option3-storage}

1. If you don't have an IAM API key, navigate to the [IBM IAM dashboard](https://cloud.ibm.com/iam/apikeys).
2. Click **Create an IBM Cloud API Key**. Enter a name and optional description for your API key and click **Create**.
3. Copy the generated IAM API key (You can see the key only when you create it, so make sure to copy it).
4. Edit your `lithops` config file and add the following keys:

    ```yaml
    lithops:
        storage_backend: ibm_cos

    ibm:
        iam_api_key: <IAM_API_KEY>

    ibm_cos:
        endpoint   : <REGION_ENDPOINT>  
        private_endpoint : <PRIVATE_REGION_ENDPOINT>
    ```
    {: pre}

### Deploy your first {{site.data.keyword.codeengineshort}} job by using Lithops
{: #running-first}

Run the following **hello world** example, 

```txt
import lithops

iterdata = [1,2,3,4,5]

def my_map_function(data):
    return data + 1

if __name__ == '__main__':
    pw = lithops.function_executor(type = "serverless", backend='code_engine') 
    futures = pw.map(my_map_function, iterdata)
    print (pw.get_result())
    pw.clean()
```
{: pre}

### Next steps for Lithops
{: #nextsteps-lithops}

You can find more examples and use cases, as well as ask questions, on the [Lithops project page](https://github.com/lithops-cloud/lithops){: external}. 
