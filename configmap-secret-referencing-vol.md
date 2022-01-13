---

copyright:
  years: 2022
lastupdated: "2022-01-13"

keywords: configmaps with code engine, secrets with code engine, key references with code engine, key-value pair with code engine, referencing secrets with code engine, referencing configmaps with code engine, configmaps, secrets, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Referencing secrets and configmaps as mounted files (CLI)
{: #secretcm-reference-mountedfiles}

In {{site.data.keyword.codeengineshort}}, after you create secrets and configmaps, the information that is stored as key-value pairs can be consumed by your job or application as a mounted file. 
{: shortdesc}

Working with secrets and configmaps as mounted files is similar to working with secrets and configmaps as environment variables. 

When you work with secrets, data is saved as an encoded string. The data is not encoded when it is added to the environment as an environment variable or as a mounted file. 


## Referencing a secret as a mounted file with the CLI
{: #secret-reference-mount-file-cli}

In this scenario, create a secret and then reference the secret as a mounted file when you run an application, which uses the `icr.io/codeengine/ce-secret-vol` image. 

The sample image, `icr.io/codeengine/ce-secret-vol`, reads each file in the `/mysecrets` directory and prints the name of the file and its contents to standard output for each request so that the output is contained in the app logs. For more information about this sample application, see the [secrets as volumes (`secrets-vol`) sample in the {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/secrets-vol){: external}.

While this scenario uses a secret, you can use the same steps to reference a configmap as a mounted file by substituting `configmap` for `secret` in the commands. 
{: tip} 

1. Create a secret, named `mysecret`, and specify the key-value pairs for the secret by using the `--from-literal` option; for example,

    ```sh
    ibmcloud ce secret create -n mysecret --from-literal apikey=abcdefgh 
    ```
    {: pre}

2. Create the `myapp` application that uses the `icr.io/codeengine/ce-secret-vol` image. Use the `--mount-secret` option to mount or add the contents of the `mysecret` secret to the app in the `/mysecrets` directory. By specifying the `--min-scale=1` option, the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. For example, 

    ```sh
    ibmcloud ce app create --name myapp --image icr.io/codeengine/ce-secret-vol --mount-secret /mysecrets=mysecret --min-scale 1
    ```
    {: pre}

    **Example output**

    ```sh
    Creating application 'myapp'...
    [...]
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce application get -n myapp' to check the application status.
    OK

    https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

3. Copy the URL from the previous output and call the application with `curl`; for example,

    ```sh
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

4. View the logs from your application. In this example, the `myapp` app uses the sample image, `icr.io/codeengine/ce-secret-vol`. This app reads each file in the `/mysecrets` directory and prints the name of the file and its contents to standard output for each request so that the output is contained in the app logs. The name of the file is `apikey`.

    ```sh
    ibmcloud ce app logs --app myapp
    ```
    {: pre}

    **Example output**

    ```sh
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-b3gxd-1-deployment-6f45dcf7f4-nw59z/user-container:
    Listening on port 8080
    apikey: abcdefgh
    ```
    {: screen}

5. Update the `mysecret` secret to change the value for the `apikey` key-value pairs; for example, 

    ```sh
    ibmcloud ce secret update -n mysecret --from-literal apikey=qrst 
    ```
    {: pre}

6. Call the application again. 

    ```sh
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

7. View the logs from your application.

    ```sh
    ibmcloud ce app logs --app myapp
    ```
    {: pre}

    **Example output**

    ```sh
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-b3gxd-1-deployment-6f45dcf7f4-nw59z/user-container:
    Listening on port 8080
    apikey: abcdefgh
    apikey: qrst
    ```
    {: screen}

You added data that is stored in secrets (or configmaps) to your app as a mounted file, and then updated the data stored in the secret. The app did not require a restart to use the updated referenced secret.


