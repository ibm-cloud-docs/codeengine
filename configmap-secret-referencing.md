---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-18"

keywords: configmaps with code engine, secrets with code engine, key references with code engine, key-value pair with code engine, referencing secrets with code engine, referencing configmaps with code engine, configmaps, secrets, environment variables, key reference, references

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Referencing secrets and configmaps with environment variables (CLI)
{: #secretcm-reference}

In {{site.data.keyword.codeengineshort}}, after you create secrets and configmaps, the information that is stored as key-value pairs can be consumed by your job or application as an environment variable by referencing the full secret or configmap or by referencing individual keys. 
{: shortdesc}

The following table lists command information for setting environment variables on jobs and apps to reference secrets and configmaps.

| Action| Option format| Commands for jobs | Commands for apps |
|-----------------|-----------------|--------------|-----|
| Referencing a full secret | `--env-from-secret NAME` where `NAME` is the name of the secret. | [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) | [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)  |
| Referencing a full configmap | `--env-from-configmap NAME` where `NAME` is the name of the configmap. | [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) | [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)  |
| Referencing specific keys in a secret | `--env-from-secret NAME:KEY_A,KEY_B` where `KEY_A`,`KEY_B` are the keys of a key-value pair. If you want to use a different name for a referenced key, use the format `NAME:MY_KEY_A=KEY_A,MY_KEY_B=KEY_B`. | [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) | [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)  |
| Referencing specific keys in a configmap | `--env-from-configmap NAME:KEY_A,KEY_B` where `KEY_A`,`KEY_B` are the keys of a key-value pair. If you want to use a different name for a referenced key, use the format `NAME:MY_KEY_A=KEY_A,MY_KEY_B=KEY_B`.| [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) | [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)  |
| Removing a fully referenced secret | `--env-from-secret-rm NAME` where `NAME` is the name of the secret. | [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) | [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) |
| Removing a fully referenced configmap | `--env-from-configmap-rm NAME` where `NAME` is the name of the configmap. | [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) | [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) |
| Removing referenced keys in a secret | `--env-rm KEY_A --env-rm KEY_B` where `KEY_A`,`KEY_B` are the keys of a key-value pair. | [**`jobf update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) | [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) |
| Removing referenced keys in a configmap | `--env-rm KEY_A --env-rm KEY_B` where `KEY_A`,`KEY_B` are the keys of a key-value pair. | [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) | [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) |
{: caption="Setting environment variables from secrets and configmaps"}

Working with secrets as environment variables is similar to working with configmaps as environment variables. When you work with secrets, the data is encoded. 

Consider the following information when you update an app or job that has an environment variable that references configmaps or secrets. 
* When you update an app or job that has an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set).
* When you update an app or job that has an environment variable that references a key in one configmap (or secret) to reference the same key in a different configmap (or secret), then the last referenced key is used.  
* When you update an app or job that has an environment variable that fully references a configmap (or secret) to add a reference to a specific key, then the specific key reference overrides the full configmap (or secret) reference. 
{: note} 

For basic information about referencing configmaps or secrets with the CLI, see [Referencing configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap-secret#configmap-ref-cli) and [Referencing secrets with the CLI](/docs/codeengine?topic=codeengine-configmap-secret#secret-ref-cli).

The following scenarios can be completed for secrets or configmaps.

## Referencing a full secret with the CLI
{: #secretcm-reference-fullref-cli}

In this scenario, create a secret, which contains key-value pairs for a username and password, and then reference the full secret when you run a job. You can update the secret to add a key and then demonstrate the use of the new key in a job. While this scenario uses a secret, you can use the same steps to fully reference a configmap by substituting `configmap` for `secret` in the commands.  

1. Create the `mydatabasesec` secret and specify the key-value pairs for a username and password by using the `--from-literal` option. 

    ```txt
    ibmcloud ce secret create -n mydatabasesec --from-literal username=reader --from-literal password=abcd
    ```
    {: pre}

2. View details about the `mydatabasesec` secret by using the **`secret get`** command. The values for the `password` and `username` keys of the secret are encoded.  

    ```txt
    ibmcloud ce secret get -n mydatabasesec 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting generic secret 'mydatabasesec'...
    OK

    Name:          mydatabasesec
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           17s
    Created:       2020-10-14 14:07:59 -0400 EDT

    Data:
    ---
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

3. Set an environment variable on a job to reference the full `mydatabasesec` secret. Use the `--env-from-secret NAME` option where `NAME` specifies to reference the full secret. Because the `busybox` image does not print any output by default, the `-c env` option specifies to print all the environment variables in the container. 

    ```txt
    ibmcloud ce job create -n demo -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

4. (Optional) View the details of the `demo` job. The output displays the full reference to the `mydatabasesec` secret. 

    ```txt
    ibmcloud ce job get -n demo
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'demo'...
    OK

    Name:          demo
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           6s
    Created:       2021-02-12T07:05:23-06:00

    Last Job Run:
        Name:     demo-jobrun-abcde
        Age:      192d
        Created:  2021-04-30T08:17:38-04:00

    Commands:                 
        env  
    Environment Variables:    
        Type                   Name           Value  
        Secret full reference  mydatabasesec    
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

5. Run a job that uses the configuration of the `demo` job. 

    ```txt
    ibmcloud ce jobrun submit --name demo1 --job demo
    ```
    {: pre}

6. Display the logs of the job run. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. In this example, display the logs of the `demo1` job run. Notice in the log output that the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```txt
    ibmcloud ce jobrun logs --jobrun demo1
    ```
    {: pre}

    **Example output**

    ```txt
    Getting jobrun 'demo1'...
    Getting instances of jobrun 'demo1'...
    Getting logs for all instances of job run 'demo1'...
    [...]

    username=reader
    password=abcd
    [...]
    ```
    {: screen}

7. Update the `mydatabasesec` secret to add a key by using `--from-file` option. This option uses the format `--from-file FILE` or `--from-file KEY=FILE`. In the following command, `certificate` is the key and `cert.pem` is the name of the file.

    ```txt
    ibmcloud ce secret update -n mydatabasesec --from-file certificate=cert.pem
    ```
    {: pre}

8. View details about the updated `mydatabasesec` secret by using the **`secret get`** command. The secret now contains three keys, `certificate`, `password`, and `username`. Secret values are encoded.

    ```txt
    ibmcloud ce secret get -n mydatabasesec 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting generic secret 'mydatabasesec'...
    OK

    Name:          mydatabasesec
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           4m13s
    Created:       2020-10-14 13:35:43 -0400 EDT

    Data:
    ---
    certificate: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tLS0tDQphc2RmO2Frc2pkZmxrYWpzZGZsa2phc2xka2ZqYWxza2RqZmxha3NqZGZsaw0KLS0tLS1FTkQgQ0VSVEZJQ0lBVEUtLS0tLS0tLS0t
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

9. Run a job that uses the `demo` job. Previously, you referenced the full secret `mydatabasesec` from the `demo` job. For a job to use the updated secret with the added `certificate` key-value pair, submit a new job run. To update an app to use the updated secret, restart the app. 

    ```txt
    ibmcloud ce jobrun submit --name demo2 --job demo
    ```
    {: pre}

10. Display the logs of the job run by using the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. To display the logs of a specific instance of the job run, use the `--instance` option with the **`jobrun logs`** command. If needed, use the **`jobrun get --name demo2`** command to display details of this job run, including the instances of the job run. In this example, display the logs of the running instance of `demo2-0-0` where `demo2` is the name of the job run, `0` is the `arrayindex`, and `0` is the `retryindex`. Notice in the output that the `certificate`, `username`, and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded.

    ```txt
    ibmcloud ce jobrun logs --instance demo2-0-0
    ```
    {: pre}

    **Example output**

    ```txt
    Getting logs for job run instance 'demo2-0-0'...
    [...]

    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=abcd
    username=reader
    ```
    {: screen}

## Referencing individual keys of a configmap with the CLI
{: #secretcm-reference-keyref-cli}

In this scenario, let's create a configmap that contains multiple key-value pairs and then reference specific keys in a job. While this scenario uses a configmap, you can use the same general steps to reference individual keys with a secret by substituting `secret` for `configmap` in the commands.  

1. Create the `mydatabase` configmap and specify the key-value pairs for a name and a URL by using the `--from-literal KEY=VALUE` option.

    ```txt
    ibmcloud ce configmap create -n mydatabasecm --from-literal name=myname --from-literal url=myurl
    ```
    {: pre}

2. View details about the `mydatabasecm` configmap by using the **`configmap get`** command. 

    ```txt
    ibmcloud ce configmap get -n mydatabasecm 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting configmap 'mydatabasecm'...
    OK

    Name:          mydatabasecm
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           16s
    Created:       2020-10-14 13:31:19 -0400 EDT

    Data:
    ---
    name: myname
    url: myurl
    ```
    {: screen}

3. Set an environment variable on a job to reference the `url` key in the `mydatabasecm` configmap. Use the `--env-from-configmap NAME:KEY_A,KEY_B` option where `NAME:KEY_A` specifies to reference the `KEY_A` of the configmap. 

    ```txt
    ibmcloud ce job create --name keydemo --image busybox --command env --env-from-configmap mydatabasecm:url 
    ```
    {: pre}

4. Run a job that uses the `keydemo` job. 

    ```txt
    ibmcloud ce jobrun submit -name keydemo1 --job keydemo
    ```
    {: pre}

5. Display the logs of the job run by using the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. To display the logs of a specific instance of the job run, use the `--instance` option with the **`jobrun logs`** command. If needed, use the **`jobrun get --name keydemo1`** command to display details of this job run, including the instances of the job run. Notice in the output that `url` is the only referenced key and that the `name` key is not referenced by the job. 

    ```txt
    ibmcloud ce jobrun logs --instance keydemo1-0-0
    ```
    {: pre}

    **Example output**

    ```txt
    Getting logs for job run instance 'keydemo1-0-0'...
    [...]

    url=myurl
    [...]
    ```
    {: screen}

## Overriding references with the CLI
{: #secretcm-reference-overfull-cli}

You can override referenced secrets and configmaps. The following scenarios can be completed for secrets or configmaps.

### Scenario A.  Override a fully referenced secret with another fully referenced secret
{: #secretcm-reference-overfull-withfull-cli}

In this scenario, let's create a new `mydatabasesec-writer` secret with the `username` and `password` keys and then override `username` and `password` keys in the previously created `mydatabasesec` secret. The `mydatabasesec` secret contains the `username=reader` and `password=abcd` keys.
{: shortdesc}

Full references override other full references in the order in which they are set (the last referenced set overrides the first set).

1. Set an environment variable on the `writerjob` job to reference the full `mydatabasesec` secret, which was created previously. The `mydatabasesec` secret contains the `username=reader` and `password=abcd` keys.  

    ```txt
    ibmcloud ce job create -n writerjob -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerjob` job. The output displays the full reference to the `mydatabasesec` secret. 

    ```txt
    ibmcloud ce job get -n writerjob
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'writerjob'...
    OK

    Name:          writerjob
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           17s
    Created:       2021-02-12T07:12:08-06:00
    [...]

    Commands:                 
        env  
    Environment Variables:    
        Type                   Name           Value  
        Secret full reference  mydatabasesec    
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

3. Run a job that uses the `writerjob` job. 

    ```txt
    ibmcloud ce jobrun submit --name writerjob1 --job writerjob
    ```
    {: pre}

4. Display the logs of the job run. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. In this example, display the logs of the `writerjob1` job run. Notice in the output that the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```txt
    ibmcloud ce jobrun logs --jobrun writerjob1
    ```
    {: pre}

    **Example output**

    ```txt
    Getting jobrun 'writerjob1'...
    Getting instances of jobrun 'writerjob1'...
    Getting logs for all instances of job run 'writerjob1'...
    OK
    [...]

    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=abcd
    username=reader
    [...]
    ```
    {: screen}

5. Create the `mydatabasesec-writer` secret and specify the key-value pairs for a username and password by using the `--from-literal` option. 

    ```txt
    ibmcloud ce secret create --name mydatabasesec-writer --from-literal username=writer --from-literal password=wxyz
    ```
    {: pre}

6. View details about the `mydatabasesec-writer` secret by using the **`secret get`** command. The values for the `password` and `username` keys of the secret are encoded.  

    ```txt
    ibmcloud ce secret get -n mydatabasesec-writer 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting generic secret 'mydatabasesec-writer'...
    OK

    Name:          mydatabasesec-writer
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           14s
    Created:       2020-10-14 13:44:16 -0400 EDT

    Data:
    ---
    password: d3h5eg==
    username: d3JpdGVy
    ```
    {: screen}

7. Update the `writerjob` job to reference the full `mydatabasesec-writer` secret. 

    ```txt
    ibmcloud ce job update --name writerjob --env-from-secret mydatabasesec-writer
    ```
    {: pre}

8. (Optional) View details of the updated `writerjob` job. The job fully references the `mydatabasesec` and the `mydatabase-writer` secrets. 

    ```txt
    ibmcloud ce job get -n writerjob 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'writerjob'...
    OK

    Name:          writerjob
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           4m2s
    Created:       2021-02-12T07:12:08-06:00
    [...]

    Commands:                 
        env  
    Environment Variables:    
        Type                   Name                  Value  
        Secret full reference  mydatabasesec           
        Secret full reference  mydatabasesec-writer    
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

9. Run a job that uses the `writerjob` job. Because the `writerjob` job was updated to reference both the `mydatabasesec` secret and the `mydatabasesec-writer` secret and both of these secrets include keys for `username` and `password`, the last referenced full secret `mydatabasesec-writer` overrides the  `mydatabasesec` secret. 

    For a job run to use the updated configuration of a job with the updates to its fully referenced secrets, run a new job. To update an app to use the updated secret, restart the app. 

    ```txt
    ibmcloud ce jobrun submit --name writerjob2 --job writerjob
    ```
    {: pre}

10. Display the logs of the job run by using the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. To display the logs of all the instances of a job, use the `--jobrun` option with the **`jobrun logs`** command. To display the logs of a specific instance of the job run, use the `--instance` option with the **`jobrun logs`** command. If needed, use the **`jobrun get --name writerjob2`** command to display details of this job run, including the instances of the job run. Notice in the output that the `username` and `password` keys of the `mydatabasesec-writer` secret overrode the keys of the `mydatabasesec` secret. Secret values are added to the environment decoded. 

    ```txt
    ibmcloud ce jobrun logs --instance writerjob2-0-0
    ```
    {: pre}

    **Example output**
            
    ```txt
    Getting logs for job run instance 'writerjob2-0-0'...
    [...]

    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=wxyz
    username=writer
    [...]
    ```
    {: screen}

### Scenario B.  Override a fully referenced secret with a key reference
{: #secretcm-reference-overfull-withkey-cli}

References to a key in a secret or configmap always overrides a full reference to a secret or configmap when the key that is used resides in a fully referenced  secret or configmap, without regard for order.
{: shortdesc}

In this scenario, let's use the previously created `mydatabasesec` and `mydatabasesec-writer` secrets and reference keys within the secrets from a job. 

1. Set an environment variable on a `writerpic` job to reference specific keys in the `mydatabasesec` and `mydatabasesec-writer` secrets. The `mydatabasesec` secret contains the `username=reader`, `password=abcd`, and `certificate=cert.pem` keys. The `mydatabasesec-writer` secret contains the `username=writer` and `password=wxyz` keys.  

    ```txt
    ibmcloud ce job create -n writerpick -i busybox -c env --env-from-secret mydatabasesec-writer:username --env-from-secret mydatabasesec-writer:password --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerpick` job. The output displays the full reference to the `mydatabasesec` secret and the key reference to the `password` and `username` keys of the `mydatabasesec-writer` secret. 

    ```txt
    ibmcloud ce job get -n writerpick
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'writerpick'...
    OK

    Name:          writerpick
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           107s
    Created:       2021-02-12T07:16:46-06:00  
    [...]

    Commands:                 
        env  
    Environment Variables:    
        Type                   Name           Value  
        Secret full reference  mydatabasesec    
        Secret key reference   password       mydatabasesec-writer.password  
        Secret key reference   username       mydatabasesec-writer.username  
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3 
    ```
    {: screen}

3. Run a job that uses the `writerpick` job. 

    ```txt
    ibmcloud ce jobrun submit --name writerpick1 --job writerpick
    ```
    {: pre}

4. Display the logs of the `writerpick1` job run by using the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. To display the logs of a specific instance of the job run, use the `--instance` option with the **`jobrun logs`** command. If needed, use the **`jobrun get --name writerpick1`** command to display details of this job run, including the instances of the job run. Because the `writerpick` job was updated to reference specific keys in the `mydatabasesec-writer` secret and to reference the full `mydatabasesec` secret, the reference to the `username` and `password` keys in the `mydatabasesec-writer` secret overrides the reference to the full secret. Secret values are added to the environment decoded. 

    ```txt
    ibmcloud ce jobrun logs --instance writerpick1-0-0
    ```
    {: pre}

    **Example output**

    ```txt
    Getting logs for job run instance 'writerpick1-0-0'...
    [...]

    username=writer
    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=wxyz
    [...]
    ```
    {: screen}

### Scenario C.  Override key references with new keys
{: #secretcm-reference-overkey-withkey-cli}

You can update the reference to a specific key in a secret or configmap and override the value with a new value. 
{: shortdesc}

In this scenario, let's use the previously created `mydatabasecm` configmap, which contains the `url:myurl` key to update the value of the key.

1. Set an environment variable on a `keyref` job to reference a specific key in the `mydatabasecm` configmap. 

    ```txt
    ibmcloud ce job create -n keyref -i busybox -c env --env-from-configmap mydatabasecm:url
    ```
    {: pre}

2. (Optional) View the details of the `keyref` job. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```txt
    ibmcloud ce job get -n keyref
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'keyref'...
    OK

    Name:          keyref
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           65s
    Created:       2021-02-12T07:18:44-06:00  
    [...]

    Commands:                 
        env  
    Environment Variables:    
        Type                     Name  Value  
        ConfigMap key reference  url   mydatabasecm.url  
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

3. Run a job that uses the `keyref` job. 

    ```txt
    ibmcloud ce jobrun submit --name keyref1 --job keyref
    ```
    {: pre}

4. Display the logs of a running instance of the `keyref1` job run by using the [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. To display the logs of a specific instance of the job run, use the `--instance` option with the **`jobrun logs`** command. If needed, use the **`jobrun get --name keyref1`** command to display details of this job run, including the instances of the job run. The job run used the `url=myurl` key reference. 

    ```txt
    ibmcloud ce jobrun logs --instance keyref1-0-0
    ```
    {: pre}

    **Example output**

    ```txt
    Getting logs for job run instance 'keyref1-0-0'...
    [...]

    url=myurl
    [...]
    ```
    {: screen}

5. Update the `keyref` job to override the `url=myurl` with a new key. Use the `--env` option to update the `url` key. The `--env` option on the [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command sets environment variables for the job in `NAME=VALUE` format.

    ```txt
    ibmcloud ce job update --name keyref --env url=newurl  
    ```
    {: pre}

6. (Optional) View the details of the `keyref` job. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```txt
    ibmcloud ce job get -n keyref
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'keyref'...
    OK

    Name:          keyref
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           3m6s
    Created:       2021-02-12T07:18:44-06:00  

    Commands:                 
        env  
    Environment Variables:    
        Type     Name  Value  
        Literal  url   newurl  
    Image:                  busybox  
    Resource Allocation:      
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

## Removing fully referenced secrets or configmaps with the CLI
{: #secretcm-reference-fullremove-cli}

You can remove a fully referenced secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the fully referenced `mydatabasesec` secret from the `demo` job.  

1. Update the `demo` job to remove the reference to the `mydatabasesec` secret.  

    ```txt
    ibmcloud ce job update -n demo --env-from-secret-rm mydatabasesec 
    ```
    {: pre}

2. View the details of the `demo` job. The output illustrates that the reference to the `mydatabasesec` secret is removed. 

    ```txt
    ibmcloud ce job get -n demo 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'demo'...
    OK

    Name:          demo
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           19m
    Created:       2021-02-12T07:05:23-06:00  
    [...]

    Commands:               
        env  
    Image:                busybox    
    Resource Allocation:    
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}

## Removing key references with the CLI
{: #secretcm-reference-keyremove-cli}

You can remove a referenced key in a secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the `url` key from the `keyref` job. 

Even though the `--env-from-configmap` option was used on a job to reference the `url` key in the `mydatabasecm` configmap, you can use the `--env-rm` option to remove individual keys. You can use the `--env-rm` option with the [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) commands to remove key references regardless of whether the keys are individual key references in a secret or configmap, or whether the keys were directly set on a job or app with the `--env` option. 
{: tip}

1. Update the `keydef` job to remove the reference to the `url` key.  

    ```txt
    ibmcloud ce job update -name keyref --env-rm url 
    ```
    {: pre}

2. View the details of the `keyref` job. The output illustrates that the reference to the `url` key is removed.  

    ```txt
    ibmcloud ce job get -n keyref 
    ```
    {: pre}

    **Example output**

    ```txt
    Getting job 'keyref'...
    OK

    Name:          keyref
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           6m27s
    Created:       2021-02-12T07:18:44-06:00  
    [...]

    Commands:               
        env  
    Image:                busybox  
    Resource Allocation:    
        CPU:     1  
        Memory:  4G  

    Runtime:    
        Array Indices:       0  
        Max Execution Time:  7200  
        Retry Limit:         3
    ```
    {: screen}



