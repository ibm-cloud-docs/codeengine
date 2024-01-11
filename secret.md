---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-11"

keywords: secrets with code engine, key references with code engine, key-value pair with code engine, setting up secrets with code engine, secrets, configmaps, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with secrets 
{: #secret} 

Learn how to work with secrets in {{site.data.keyword.codeengineshort}}. In {{site.data.keyword.codeengineshort}}, you can store your information as key-value pairs in secrets that can be consumed by your function, job, or application by using environment variables. 
{: shortdesc}

## What are secrets and why would I use them? 
{: #secret-whatwhy}

In {{site.data.keyword.codeengineshort}}, secrets (and configmaps) are a collection of key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app, function, or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs.

Because secrets and configmaps are similar entities (except secrets are stored more securely), the way you interact and work with secrets and configmaps is also similar. To learn more about configmaps, see [Working with configmaps](/docs/codeengine?topic=codeengine-configmap).
{: note} 

### What kind of secrets can I create in {{site.data.keyword.codeengineshort}}? 
{: #secret-categories}

{{site.data.keyword.codeengineshort}} supports various secrets and provides options for creating and working with secrets. 

The following table summarizes the supported secrets in {{site.data.keyword.codeengineshort}}. 

| Name | Description | 
| -------------- | -------------- |
| Basic authentication  | A secret that contains a `username` and `password` key. \n Use basic authentication secrets when you access a service that requires basic HTTP authentication. |
| Generic  | A secret that stores simple key-value pairs and {{site.data.keyword.codeengineshort}} makes no assumptions about the defined key-value pairs nor about the intended use of the secret. \n Use generic secrets when you want to define your own key-value pairs to access a service.  |
| Registry  | A secret that stores credentials to access a container registry. \n Use registry secrets when you work with {{site.data.keyword.codeengineshort}} apps or jobs to access a container image. Or, you use {{site.data.keyword.codeengineshort}} to build a container image and the registry secret is used by {{site.data.keyword.codeengineshort}} to access the registry to store the built container image. \n This secret is also referred to as a `Registry access secret` in the CLI. |
| Service access | A secret that stores credentials to access an {{site.data.keyword.cloud_notm}} service instance. \n Use service access secrets when you work with [service bindings](/docs/codeengine?topic=codeengine-service-binding) in {{site.data.keyword.codeengineshort}}.  {{site.data.keyword.codeengineshort}} can automatically generate this secret or you can create your own custom service access secret. |
| SSH | A secret that stores credentials to authenticate to a service with an SSH key, such as authenticating to a Git repository, such as GitHub or GitLab. \n Use SSH secrets when you want {{site.data.keyword.codeengineshort}} to build a container image for you. {{site.data.keyword.codeengineshort}} uses this secret to access your source code in a code repository. For example, use this secret with build runs to access your source code in a repository, such as GitHub or GitLab. \n This secret is also used as a `Git repository access secret` in the CLI and `Code repo access` in the console. |
| Transport Layer Security (TLS) | A secret that contains a signed TLS certificate, including all its intermediate certificates, and its corresponding private key from a certificate authority (CA). \n Use TLS secrets when you work with [custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings) in {{site.data.keyword.codeengineshort}}. |
{: caption="Table 1. Secrets in {{site.data.keyword.codeengineshort}}" caption-side="bottom"}


## Creating secrets
{: #secret-create}

Use secrets to provide sensitive information to your apps, jobs, or functions. Secrets are defined in key-value pairs and the data that is stored in secrets is encoded.
{: shortdesc}

### Creating a secret from the console
{: #secret-create-ui}

Learn how to create secrets from the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}


#### Creating a generic secret from the console
{: #secret-create-ui-generic}

Learn how to create generic secrets from the {{site.data.keyword.codeengineshort}} console that can be consumed by functions, jobs, or apps as environment variables.
{: shortdesc}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Components page, click **Secrets and configmaps**.
3. From the Secrets and configmaps page, click **Create** to create your secret.
4. From the Create config page, complete the following steps:
    1. Select **Generic secret**, and click **Next**.
    2. Provide a name; for example, `mysecret`.
    3. Click **Add key-value pair**. Specify one or more key-value pairs for this secret. For example, specify one key as `secret1` with the value of `mysecret1` and specify another key as `secret2` with the value of `target-secret`. The name that you choose for your key does not need to be the same as the name of your environment variable. Notice that the value for the key is hidden, but it can be viewed if needed. 
5. Click **Create** to create the secret. 
6. Now that your secret is created from the console, go to the Secrets and configmaps page to view a listing of defined secrets and configmaps. For secrets, you can display a list of user-generated secrets or a list of all secrets, which includes secrets that are generated by {{site.data.keyword.codeengineshort}}. 

#### Creating a TLS secret from the console
{: #secret-create-ui-tls}

Learn how to create a TLS secret from the console that can be consumed by apps when you work with custom domain mappings in {{site.data.keyword.codeengineshort}}. A Transport Layer Security (TLS) secret contains a signed TLS certificate, including all its intermediate certificates, and its corresponding private key from a certificate authority (CA).

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Components page, click **Secrets and configmaps**.
3. From the Secrets and configmaps page, click **Create** to create your secret.
4. From the Create config page, complete the following steps:
    1. Select the **TLS secret** option.  
    2. Provide a name; for example, `myTLSsecret`.
    3. Add the certificate chain and its private key. Note that you can concatenate the certificates by starting each in a new line. You can provide this information in a file. 
5. Click **Create** to create the TLS secret. 
6. Now that your TLS secret is created from the console, go to the Secrets and configmaps page to view a listing of defined secrets and configmaps. For secrets, you can display a list of user-generated secrets or a list of all secrets, which includes secrets that are generated by {{site.data.keyword.codeengineshort}}. You can use your TLS secret when working with [custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings) in {{site.data.keyword.codeengineshort}}.




### Creating secrets with the CLI
{: #secret-create-cli}

Learn how to create secrets with the {{site.data.keyword.codeengineshort}} CLI that can be consumed by apps, jobs, or functions as environment variables.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Beginning with CLI version 1.42.0, defining and working with secrets in the CLI is unified under the **`secret`** command group. See [**`ibmcloud ce secret`**](/docs/codeengine?topic=codeengine-cli#cli-secret-create) commands. Use the `--format` option to specify the category of secret, such as `basic_auth`, `generic`, `ssh`, `tls`, or `registry`. The default value for the `--format` option is `generic`. 
{: important}


By using the **`secret create`** command, you can create and manage various secret formats. For descriptions of the various secret formats, see [What kind of secrets can I create in {{site.data.keyword.codeengineshort}}?](#secret-categories) 

Learn how to create the following types of secrets with the CLI,
* [Basic authentication](#secret-create-cli-basicauth)
* [Generic](#secret-create-cli-generic)
* [Registry](#secret-create-cli-registry)
* [SSH](#secret-create-cli-ssh)
* [TLS](#secret-create-cli-tls)

#### Creating a basic authentication secret with the CLI
{: #secret-create-cli-basicauth}

A basic authentication secret contains a username and password key and is used to access a service that requires basic HTTP authentication. The following example creates a basic authentication secret with credentials for `myusername` and the associated password is provided in a file on the local workstation 

```txt
ibmcloud ce secret create --name mysecret-basicauth --format basic_auth --username myusername --password-from-file ./password.txt
```
{: pre}

To display the details of this secret, 

```txt
ibmcloud ce secret get --name mysecret-basicauth 
```
{: pre}

Example output

```txt
Getting secret 'mysecret-basicauth'...
OK

Name:          mysecret-basicauth
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Format:        basic_auth 
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2021-03-10T18:44:18-05:00

Data:    
---
password: REDACTED
username: bXl1c2VybmFtZQ==
```
{: screen}

Notice that the value of the key `username` for this basic authentication secret is encoded, and the value of `password` is redacted. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command.  

#### Creating a generic secret with the CLI
{: #secret-create-cli-generic}

A generic secret stores simple key-value pairs and {{site.data.keyword.codeengineshort}} makes no assumptions about the defined key-value pairs nor about the intended use of the secret. 

You can create a generic secret with the **`secret create`** command in one of the following ways. By default, a generic secret is created when the `--format` option is not specified.

* Create a secret directly from the command line by using the `--from-literal` option in `KEY=VALUE` format. For example, 

    ```txt
    ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My literal secret"
    ```
    {: pre}

* Create a secret by using the `--from-file` option to point to a file. By using this option, all the contents of the file become the value for the key-value pair. For this example, use a file that is named `secrets.txt`, which contains `my little secret1`. 


    * The following example uses the `--from-file KEY=FILE` format with the **`secret create`** command:  

        ```txt
        ibmcloud ce secret create --name mysecretmsg1 --from-file TARGET=secrets.txt
        ```
        {: pre}

    * The following example command uses the `--from-file FILE` format with the **`secret create`** command. In this example, `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to the job.

        ```txt
        ibmcloud ce secret create --name mysecretmsg2  --from-file TARGET
        ```
        {: pre}

* Create a secret by using the `--from-env-file` option to point to a file that contains one or more lines that match the format `KEY=VALUE`. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. For this example, use a file that is named `secrets_multi.txt`, which contains the key-value pairs: `sec1=mysec1`, `sec2=mysec2`, and `sec3=mysec3`. 

    ```txt
    ibmcloud ce secret create --name mysecretmulti --from-env-file secrets_multi.txt
    ```
    {: pre}


If you want to create (or update) a generic secret from a file, use the `--from-file` option with one of the following formats: `--from-file FILE` or `--from-file KEY=FILE` In {{site.data.keyword.codeengineshort}}, when you use the `--from-file` option to specify secret values, *all* the contents within the file is the value for the key-value pair. When you use the option format of `--from-file KEY=FILE`, the `KEY` is name of the environment variable that is known to your job, function, or app. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job, function, or app. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. Any lines in the specified file that are empty or begin with `#` are ignored. 
{: tip}

To display the details of the generic secret, `myliteralsecret`, 

```txt
ibmcloud ce secret get --name myliteralsecret
```
{: pre}

Example output

```txt
Getting secret 'myliteralsecret'...
OK

Name:          myliteralsecret
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Format:        generic 
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2023-03-07 21:06:34 +0000 UTC  

Data:    
---
TARGET: TXkgbGl0ZXJhbCBzZWNyZXQ=
```
{: screen}

Notice that the value of the key `TARGET` for this generic secret is encoded. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command.  

#### Creating a registry secret with the CLI
{: #secret-create-cli-registry}

A registry secret stores credentials to access a container registry. 

The following example creates a registry secret that is named `mysecret-registry` to access an {{site.data.keyword.registryfull_notm}} instance that is on the `us.icr.io` registry server and specifies credentials for `username` and `password`.

```txt
ibmcloud ce secret create --name mysecret-registry --format registry --server us.icr.io --username iamapikey --password API_KEY
```
{: pre}

To display the details of this secret, 

```txt
ibmcloud ce secret get --name mysecret-registry
```
{: pre}

Example output

```txt
Getting secret 'mysecret-registry'...
OK

Name:          mysecret-registry
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Format:        registry 
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2023-03-07 20:00:45 +0000 UTC  

Data:    
---
email: ""
password: REDACTED
server: dXMuaWNyLmlv
username: aWFtYXBpa2V5
```
{: screen}

Notice that the value of the `username` and `server` keys for this registry secret is encoded, and the value of `password` is redacted. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command.  

#### Creating an SSH secret with the CLI
{: #secret-create-cli-ssh}

An SSH secret stores credentials to authenticate to a service with an SSH key; for example, authenticating to a Git repository, such as GitHub or GitLab.  

The following example creates an SSH secret that is named `mysecret-ssh` to access a host that is included in the `known_hosts` file by authenticating with an unencrypted SSH private key file that is located at `/<filepath>/.ssh/<key_name>`, where `<filepath>` is the path on your local workstation. This command requires a name and a key path, and also allows other optional arguments such as the path to the known hosts file. 

```txt
ibmcloud ce secret create --name mysecret-ssh --format ssh --key-path ~/.ssh/<key_name> --known-hosts-path  ~/.ssh/known_hosts
```
{: pre}


To display the details of this secret, 

```txt
ibmcloud ce secret get --name mysecret-ssh
```
{: pre}

Example output

```txt
Getting secret 'mysecret-ssh'...
OK

Name:          mysecret-ssh'
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Format:        ssh 
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2023-03-07 19:19:59 +0000 UTC  

Data:    
---
known_hosts: fDF8bGh0ekpiSFVXdXRxZWg1NUlrWTk4RjdOdjJZPXxsUmhZd0txVmIwd3dSV2xzcjEySFdoWURUTG89IHNzaC1yc2EgQUFBQUIzTnphQzF5YzJFQUFBQUJJd0FBQVFFQXEyQTdoUkdtZG5tOXRVRGJPOUlEU3dCSzZUYlFhK1BYWVBDUHk2cmJUclR0dzdQSGtjY0tycHAweVZocDVIZEVJY0tyNnBMbFZEQmZPTFg5UVVzeUNPVjB3emZqSUpObEdFWXNkbExKaXpIaGJuMm1VanZTQUhRcVpFVFlQODFlRnpMUU5uUEh0NEVWVlVoN1ZmREVTVTg0S2V6bUQ1UWxXcFhMbXZVMzEveU1mK1NlOHhoSFR2S1NDWklGSW1Xd29HNm1iVW9XZjluenBJb2FTakIrd2VxcVVVbXBhYWFzWFZhbDcySitVWDJCKzJSUFczUmNUMGVPelFncWxKTDNSS3JUSnZkc2pFM0pFQXZHcTNsR0hTWlh5MjhHM3NrdWEyU21WaS93NHlDRTZnYk9EcW5UV2xnNyt3QzYwNHlkR1hBOFZKaVM1YXA0M0pYaVVGRkFhUT09CnwxfEpUSjI4MCt0RkFSMGcxZ3VrZW56U3ZBYm5sQT18RDlSUWppenZlR3UxS0FnNjhNeisrUHM3RmZrPSBlY2RzYS1zaGEyLW5pc3RwMjU2IEFBQUFFMlZqWkhOaExYTm9ZVEl0Ym1semRIQXlOVFlBQUFBSWJtbHpkSEF5TlRZQUFBQkJCRW1LU0VOalFFZXpPbXhrWk15N29wS2d3RkI5bmt0NVlScllNak51RzVOODd1UmdnNkNMcmJvNXdBZFQveTZ2MG1LVjBVMncwV1oyWUIvKytUcG9ja2c9CnwxfDhIOXpNb0VORklZVDNPeVZYWlQrY25wb0srND18dVdhVThFV1FPc0ttSDMzREVVd0xnNUtiUk44PSBzc2gtZWQyNTUxOSBBQUFBQzNOemFDMWxaREkxTlRFNUFBQUFJT01xcW5rVnpybTBTZEc2VU9vcUtMc2FiZ0g1Qzlva1dpMGRoMmw5R0tKbAo=
ssh-privatekey: REDACTED
```
{: screen}

Notice that the value of the `known_hosts` key for this SSH secret is encoded, and the value of `ssh-privatekey` is redacted. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command.

#### Creating a TLS secret with the CLI
{: #secret-create-cli-tls}

A Transport Layer Security (TLS) secret contains a signed TLS certificate, including all its intermediate certificates, and its corresponding private key from a certificate authority (CA). Use TLS secrets when you work with custom domain mappings.

The following example creates a TLS secret that is named `mysecret-tls`. The certificate chain that corresponds to the custom domain is contained in the file `certificate.txt` and the matching private key file is contained in the file `privatekey.txt`. In this example, both of these files are located in the root directory of the local workstation.

```txt
ibmcloud ce secret create --name mysecret-tls  --format tls  --cert-chain-file certificate.txt --private-key-file privatekey.txt 
```
{: pre}


To display the details of this secret, 

```txt
ibmcloud ce secret get --name mysecret-tls
```
{: pre}

Example output



```txt
Getting secret 'mysecret-tls'...
OK

Name:          mysecret-tls'
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Format:        tls 
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2023-03-07 16:14:46 +0000 UTC  

Data:    
---
tls.crt: REDACTED
tls.key: REDACTED
```
{: screen}



#### Listing secrets with the CLI
{: #secret-list-cli}

After secrets are created, use the [**`secret list`**](/docs/codeengine?topic=codeengine-cli#cli-secret-list) command to list all secrets in your project. For example, 


```txt
ibmcloud ce secret list
```
{: pre}

Example output

```txt
Listing secrets...
OK

Name                          Format          Data  Age  
ce-auto-icr-private-us-south  registry        4     333d  
ce-auto-private-icr-us-south  registry        4     335d  
myregistry-seccmd             registry        4     3h31m  
mysecret-basicauth            basic_auth      2     7m37s  
mysecret-generic              generic         1     7m7s  
mysecret-genericfromfile      generic         2     2m29s  
mysecret-registry             registry        4     111s  
mysecret-ssh                  ssh_auth        2     42m  
mysecret-tls                  tls             2     3h47m 
```
{: screen}

## Updating secrets 
{: #secret-update}

You can change key-value pairs for existing secrets.
{: shortdesc}

### Updating secrets from the console 
{: #secret-update-ui}

You can update key-value pairs for your defined secrets from the console. 
{: shortdesc}

1. You can update key-value pairs for your defined secrets from the console in one of the following ways. 

    * Go to the Secrets and configmaps page for your project and locate the secret that you want to update. Click the name of the secret that you want to update to open it.
    * If your secret is referenced by an app, job, or function, then use the links in the environment variables table on the **Environmental variables** tab of your app, job, or function. These links take you directly to your secret. Alternatively, you can also go to the Secrets and configmaps page for your project and locate the secret that you want to update. Click the name of the secret that you want to update to open it.

2. Click **Edit** and make the updates for your secret. 

3. Click **Save** to save the changes to your secret.

If your updated secret is referenced by a job, function, or app, then your job, function, or app must be restarted for the new data to take effect. 

* Apps - From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated secret.
* Jobs - From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated secret.
* Functions - From the page for your function, click **Test Function**. If you have a browser open to the function URL, refresh the browser.

### Updating secrets with the CLI 
{: #secret-update-cli}

You can update an existing secret and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a defined secret, use the [**`secret update`**](/docs/codeengine?topic=codeengine-cli#cli-secret-update) command. Let's update the `mysecret-registry` secret to use a different server. 

    ```txt
    ibmcloud ce secret update --name mysecret-registry --format registry --server <new_server> --username <new_username> --password <password>
    ```
    {: pre}

2. Now that your secret is updated, use the **`secret get`** command to display details about a specific secret. If needed, use the `--decode` option to display the secret data as decoded. For example,

    ```txt
    ibmcloud ce secret get --name mysecret-registry --decode
    ```
    {: pre}

    Example output

    ```txt
    Getting generic secret 'mysecret-registry'...
    OK

    Name:          mysecret-registry
    ID:            abcdefgh-abcd-abcd-abcd-c88e2775388e
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           21m
    Created:       2023-03-07 20:00:45 +0000 UTC  

    Data:    
    ---
    email: ""
    password: REDACTED
    server: newserver
    username: newuser
    ```
    {: screen}


## Referencing secrets 
{: #secret-ref}

Your job, function, or app can consume and use the information that is stored in a secret by using environment variables. 
{: shortdesc}

### Referencing secrets from the console 
{: #secret-ref-ui}

You can use the console to create environment variables for your apps, jobs, and functions that fully reference a secret or reference individual keys in a secret. 
{: shortdesc}

Before you can reference a secret, it must exist. See [create a secret](#secret-create). For this example, create a secret that is named `target-secret` with the key-value pair of `TARGET=Sunshine`.

1. To reference a defined secret from your apps, jobs, and functions, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing secret or reference an individual key in an existing secret. When you fully reference a secret (or configmap), you can optionally specify a `prefix`. For example, if you fully reference the `mysecret` secret from the `myapp` application and use the `mysecret_` prefix, each key in the secret is prefixed with `mysecret_`. 

2. After you create environment variables, you must restart your apps, jobs, and functions for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs, submit your job to update the job with the environment variables that you defined. 

3. After the apps, jobs, and functions status changes to **Ready**, you can test the application or function, or run the job. For an app, click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. In the `myapp` example, because a prefix was specified for the fully referenced `mysecret` secret, all the keys of this secret are referenced as environment variables and are prefixed with `mysecret_`. For example, these environment variables display as `mysecret_secret1=mysecret1` and `mysecret_secret2=mysecret2`. 

To update an environment variable that references a secret, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations for updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a secret, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

For example, let's use the previously defined `mysecret` secret that you defined from the console with a job and fully reference this secret with an environment variable. 

1. [Create and run a job](/docs/codeengine?topic=codeengine-job-plan). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    From the Jobs page,
    1. Create a job; for example, `myjob`.
    2. Specify `icr.io/codeengine/codeengine` as the image reference.
    3. Click **Create** to create the job. 

    If the workload that you want to use with the secret is already defined in {{site.data.keyword.codeengineshort}}, go to the Applications, Jobs, or Functions page and then click the name of your app, job, or function to open the component. 

2. When the job is created, from the Jobs page, click the name of your job to open it. 

3. Update the job to add a secret as an environment variable. Click **Environment variables** to open the tab and click **Add** to add your environment variable. 

4. From the Add environment variable page,
    1. To use the previously defined secret, select **Reference full secret**.
    2. From the menu, select the name of the secret that you want; for example, `target-secret`.
    3. Click **Add** to add the environment variable. 
    4. Click **Save** to save the changes to your job. 

5. To run the job with the environment variable that references a secret, click **Submit job**. For this example, the logs of the `myjob` job run display `Hello Sunshine from {{site.data.keyword.codeengineshort}}` and the prints the environment variables, including any values of secrets that are referenced with environment variables. 

### Referencing secrets with the CLI 
{: #secret-ref-cli}

To use secrets with apps, jobs, and functions, you can set environment variables that fully reference a secret or reference individual keys in a secret with the CLI.
{: shortdesc}

#### Referencing existing secrets with the CLI 
{: #secret-ref-existing-cli}

The following examples reference a generic secret, which is the default secret when the `--format` option is not specified. Use the `--format` option to specify the category of secret, such as `basic_auth`, `generic`, `ssh`, `tls`, or `registry`. 
{: note}

To use a secret with a workload with the CLI, specify the `--env-from-secret` option on the following commands.
- [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)
- [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create)
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update)
- [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit)
- [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit)
- [**`fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create)
- [**`fn update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update)

The following example describes how to reference an existing generic secret with a job by using the CLI. 

1. Use the **`secret create`** command to create the following two generic secrets for this scenario. By default, a generic secret is created when the `--format` option is not specified.

    ```txt
    ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My big literal secret"
    ```
    {: pre}

    ```txt
    ibmcloud ce secret create --name myliteralsecret2 --from-literal "TARGET=My little literal secret"
    ```
    {: pre}       

2. [Create a job](/docs/codeengine?topic=codeengine-job-plan) and reference the `myliteralsecret` secret. For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine --array-indices 2-3 --env-from-secret myliteralsecret
    ```
    {: pre}

3. Run the `myjob` job. 

    ```txt
    ibmcloud ce jobrun submit --name myjobrun --job myjob
    ```
    {: pre}

4. Use the **`jobrun get`** command to display details of the job run, including the instances of the job run. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    Getting events of jobrun 'myjobrun'...
    Run 'ibmcloud ce jobrun events -n myjobrun' to get the system events of the job run instances.
    Run 'ibmcloud ce jobrun logs -f -n myjobrun' to follow the logs of the job run instances.
    OK

    Name:               myjobrun
    [...]
    Job Ref:                myjob
    Environment Variables:
        Type                   Name          Value
        Secret full reference  myliteralsecret
    Image:                  icr.io/codeengine/codeengine
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  4G
        Memory:             4G

    Runtime:
        Mode:                  task
        Array Indices:         2-3
        Array Size:            2
        JOP_ARRAY_SIZE Value:  2
        Max Execution Time:    7200
        Retry Limit:           3

    Status:
        Completed:          9s
        Instance Statuses:
            Succeeded:  2
        Conditions:
            Type      Status  Last Probe  Last Transition
            Pending   True    13s         13s
            Running   True    9s          9s
            Complete  True    9s          9s

    Events:
        Type    Reason     Age                Source                Messages
        Normal  Updated    10s (x4 over 14s)  batch-job-controller  Updated JobRun "myjobrun"
        Normal  Completed  10s                batch-job-controller  JobRun completed successfully

    Instances:
        Name          Running  Status     Restarts  Age
        myjobrun-2-0  0/1      Succeeded  0         14s
        myjobrun-3-0  0/1      Succeeded  0         14s
    ```
    {: screen}

5. Display the logs of the `myjobrun` job run. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. This time, display the logs of the all the instances of the job run. The log displays `Hello my big literal secret!`, which was specified by using an environment variable with a secret. Note, for this job that is defined with the `icr.io/codeengine/codeengine` image, the output of the job run prints the environment variables, including any values of secrets that are referenced with environment variables. 

    ```txt
    ibmcloud ce jobrun logs --jobrun myjobrun
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of job run 'myjobrun'...
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    OK

    myjobrun-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2

    Hello My big literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrun-2-0
    JOB_INDEX=2
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    TARGET=My big literal secret

    myjobrun-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello My big literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrun-3-0
    JOB_INDEX=3
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    TARGET=My big literal secret
    ```
    {: screen}

6. Resubmit the job run and specify to use the `myliteralsecret2` secret for this job run.  

    ```txt
    ibmcloud ce jobrun resubmit  --jobrun myjobrun  --name myjobrunresubmit  --env-from-secret myliteralsecret2
    ```
    {: pre}

    When you update a job, app, or function with an environment variable that fully references a secret to fully reference a different secret, full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
    {: note}

7. Use the **`jobrun get`** command to display details of the job run, including the instances of the job run. Notice that the job run references both `myliteralsecret` and `myliteralsecret2` secrets.

    ```txt
    ibmcloud ce jobrun get --name myjobrunresubmit
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrunresubmit'...
    Getting instances of jobrun 'myjobrunresubmit'...
    Getting events of jobrun 'myjobrunresubmit'...
    [...]

    Name:          myjobrunresubmit
    ID:            79f01367-932b-4a76-be18-b1e68790a85b
    Project Name:  myproject
    Project ID:    841f0f38-420d-4388-b5d8-f230657d7dc6
    Age:           14s
    Created:       2021-06-15T21:15:37-04:00

    Job Ref:                myjob
        Environment Variables:
        Type                   Name              Value
        Secret full reference  myliteralsecret
        Secret full reference  myliteralsecret2
    Image:                  icr.io/codeengine/codeengine
        Resource Allocation:
        CPU:                1
        Ephemeral Storage:  4G
        Memory:             4G

    Runtime:
        Mode:                  task
        Array Indices:         2-3
        Array Size:            2
        JOP_ARRAY_SIZE Value:  2
        Max Execution Time:    7200
        Retry Limit:           3

    Status:
        Completed:          11s
        Instance Statuses:
            Succeeded:  2
        Conditions:
            Type      Status  Last Probe  Last Transition
            Pending   True    14s         14s
            Running   True    12s         12s
            Complete  True    11s         11s

    Events:
        Type    Reason     Age                Source                Messages
        Normal  Updated    13s (x4 over 16s)  batch-job-controller  Updated JobRun "myjobrunresubmit"
        Normal  Completed  13s                batch-job-controller  JobRun completed successfully

    Instances:
        Name                  Running  Status     Restarts  Age
        myjobrunresubmit-2-0  0/1      Succeeded  0         16s
        myjobrunresubmit-3-0  0/1      Succeeded  0         16s
    ```
    {: screen}

8. Display the job run logs of an instance of the `myjobrunresubmit` job run. This time, display the logs of the `myjobrunresubmit-3-0` instance. The log displays `Hello My little literal secret!`, which is the value that is specified in the `myliteralsecret2` secret. Use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. 

    ```txt
    ibmcloud ce jobrun logs --instance myjobrunresubmit-3-0
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for job run instance 'myjobrunresubmit-3-0'...
    OK

    myjobrunresubmit-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello My little literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrunresubmit-3-0
    JOB_INDEX=3
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    TARGET=My little literal secret
    ```
    {: screen}

9. To change the value of key-value pair in a secret, use the **`secret update`** command. Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My big literal secret` to `My new big literal secret`.

    ```txt
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new big literal secret"
    ```
    {: pre}

10. For the new data to take effect, run your job again. Resubmit the job run again and specify to use the `myliteralsecret` secret for this job run. 

    ```txt
    ibmcloud ce jobrun resubmit  --jobrun myjobrun  --name myjobrunresubmit2 --env-from-secret myliteralsecret 
    ```
    {: pre}

11. Display the logs of the `myjobrunresubmit2` job run. This time, the job log displays `Hello My new big literal secret!`, which is the value in the updated `myliteralsecret` secret. You can use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. Display the logs for any running instance of the job run.

    ```txt
    ibmcloud ce jobrun logs --instance myjobrunresubmit2-2-0
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for job run instance 'myjobrunresubmit2-2-0'...
    OK

    myjobrunresubmit2-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2

    Hello My new big literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrunresubmit2-2-0
    JOB_INDEX=2
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    TARGET=My new big literal secret
    ```
    {: screen}

To summarize, you completed basic scenarios to demonstrate how to use secrets with a job by referencing an existing full secret and updating keys within a secret.

#### Referencing secrets that are not yet defined with the CLI 
{: #secret-ref-notyetdefined-cli}

If a secret does not exist before it is referenced, an app will not deploy successfully, and a job or function will not run successfully until the referenced secret is created.  

If you are working with an app, job, or function and the referenced secret is not yet defined, use the `--force` option to avoid verification of the existence of the referenced secret. 
The `--force` option can be used with the following commands.
- [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)
- [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create)
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update)
- [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit)
- [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit)
- [**`fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create)
- [**`fn update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) 

When you use the `--force` option with these commands, the action to create, update, or run the app, job, or function completes. However, the app, job, or function will not run successfully until the referenced secret exists. If you add the `--no-wait` option in addition to the `--force` option to the command, the system completes the action, and does not wait for the app, job, or function to run successfully. 

The following example describes how to reference a secret that is not yet defined with a job by using the CLI. 

1. [Create a job](/docs/codeengine?topic=codeengine-job-plan). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine 
    ```
    {: pre}

2. Use the **`jobrun submit`** command to run the `myjob` job. Note that the `mynewliteralsecret` does not exist. By using the `--no-wait` option with the **`jobrun submit`** command, the job run is submitted and does not wait for the instances of this job run to complete. 

    ```txt
    ibmcloud ce jobrun submit --name myjobrun1 --job myjob --env-from-secret mynewliteralsecret --force --no-wait
    ```
    {: pre}

3. Use the **`jobrun get`** command to display details of the job run, including the environment variable information. Notice that the job run is in `pending` status. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun1
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun1'...
    Getting instances of jobrun 'myjobrun1'...
    Getting events of jobrun 'myjobrun1'...
    [...]

    Name:          myjobrun1
    [...]

    Job Ref:                myjob
    Environment Variables:
        Type                   Name                Value
        Secret full reference  mynewliteralsecret
    Image:                  icr.io/codeengine/codeengine
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Runtime:
        Mode:                  task
        Array Indices:         0
        Array Size:            1
        JOP_ARRAY_SIZE Value:  1
        Max Execution Time:    7200
        Retry Limit:           3

    Status:
        Instance Statuses:
            Pending:  1
        Conditions:
            Type     Status  Last Probe  Last Transition
            Pending  True    100s        100s

    Events:
        Type    Reason   Age                   Source                Messages
        Normal  Updated  108s (x5 over 2m29s)  batch-job-controller  Updated JobRun "myjobrun1"

    Instances:
        Name           Running  Status   Restarts  Age
        myjobrun1-0-0  0/1      Pending  0         2m29s
    ```
    {: screen}

4. Create the secret.  

    ```txt
    ibmcloud ce secret create --name mynewliteralsecret --from-literal "TARGET=Fun secret"
    ```
    {: pre}

5. Run the `myjobrun1` job run again. 

    ```txt
    ibmcloud ce jobrun resubmit --jobrun myjobrun1 --name myjobrunresubmit1
    ```
    {: pre}

    Run the **`ibmcloud ce jobrun get -n myjobrunresubmit1`** command to check the status of this job run.

6. Display the logs of the `myjobrunresubmit1` job run. The logs display `Hello Fun secret from {{site.data.keyword.codeengineshort}}`, which confirms the job run referenced the `myliteralsecret` secret. 

    ```txt
    ibmcloud ce jobrun logs --jobrun myjobrunresubmit1
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of job run 'myjobrunresubmit1'...
    Getting jobrun 'myjobrunresubmit1'...
    Getting instances of jobrun 'myjobrunresubmit1'...
    OK

    myjobrunresubmit1-0-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 0

    Hello Fun secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrunresubmit1-0-0
    JOB_INDEX=0
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
    TARGET=Fun secret
    ```
    {: screen}

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


## Deleting secrets 
{: #secret-delete}

When you no longer need a secret, you can delete it. 
{: shortdesc} 

### Deleting secrets from the console
{: #secret-delete-ui}

1. To delete a secret from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the secret that you want to delete to open its page. 
    3. From the page for the specific secret, click **Actions > Delete secret**.
2. To delete a key-value pair for a specific secret from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the secret that you want to change to open its page. 
    3. From the page for the specific secret, delete the key-value pair that you want to remove. 

You can also delete defined environment variables that reference secrets and configmaps. To delete a defined environment variable, from the **Environment variables** tab of your app, job, or function and delete the environment variable that you want to delete. After you delete a defined environment variable, be sure to click **Save** to save the changes to your app, job, or function. For more information, see [Delete an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Deleting secrets with the CLI
{: #secret-delete-cli}

To delete a secret with the CLI, use the [**`secret delete`**](/docs/codeengine?topic=codeengine-cli#cli-secret-delete) command; for example, 

```txt
ibmcloud ce secret delete --name myliteralsecret -f
```
{: pre}

Example output

```txt
Deleting secret myliteralsecret...
OK
```
{: screen}

You can also [delete environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-cli) that reference secrets and configmaps from the CLI.



