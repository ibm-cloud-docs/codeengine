---

copyright:
  years: 2020
lastupdated: "2020-09-15"

keywords: code engine, configmap, secret

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Referencing secrets and configmaps with the CLI 
{: #secretcm-reference}

In {{site.data.keyword.codeengineshort}}, after creating secrets and configmaps, the information that is stored as key-value pairs can be consumed by your job or application as an environment variable by referencing the full secret or configmap or by referencing individual keys. 
{: shortdesc}

You can work with configmaps and secrets with the CLI, but this capability is not currently available from the console.
{: important} 

The following table lists command information for setting environment variables on jobs and apps to reference secrets and configmaps.

| Action| Option format| Commands for jobs | Commands for apps |
|-----------------|-----------------|--------------|-----|
| Referencing a full secret | `--env-from-secret NAME` where `NAME` is the name of the secret. | [`job create`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-create), [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update), [`jobrun submit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-submit), [`jobrun resubmit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-resubmit) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing a full configmap | `--env-from-configmap NAME` where `NAME` is the name of the configmap. | [`job create`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-create), [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update), [`jobrun submit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-submit), [`jobrun resubmit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-resubmit) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing specific keys in a secret | `--env-from-secret NAME:KEY_A,KEY_B` where `KEY` is the key of a key-value pair. |  [`job create`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-create), [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update), [`jobrun submit](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-submit), [`jobrun resubmit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun-resubmit) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing specific keys in a configmap | `--env-from-configmap NAME:KEY_A,KEY_B` where `KEY` is the key of a key-value pair. | [`job create`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-create), [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update), [`jobrun submit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrin-submit), [`jobrun resubmit`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobrun resubmit) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Removing a fully referenced secret | `--env-from-secret-rm NAME` where `NAME` is the name of the secret. | [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing a fully referenced configmap | `--env-from-configmap-rm NAME` where `NAME` is the name of the configmap. | [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing referenced keys in a secret | `--env-rm KEY_A --env-rm KEY_B` where `KEY` is the key of a key-value pair. | [`jobf update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing referenced keys in a configmap | `--env-rm KEY_A --env-rm KEY_B` where `KEY` is the key of a key-value pair. | [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
{: caption="Setting environment variables from secrets and configmaps"}

To work with secrets as environment variables is similar to working with configmaps as environment variables. When working with secrets, the data is encoded. 

The following scenarios can be completed for secrets or configmaps.

## Referencing a full secret with the CLI
{: #secretcm-reference-fullref-cli}

In this scenario, let's create a secret, which contains key-value pairs for a username and password, and then reference the full secret when running a job. We can update the secret to add a new key and then demonstrate the use of the new key in a job. While this scenario uses a secret, you can use the same steps to fully reference a configmap by substituting `configmap` for `secret` in the commands.  

1. Create the `mydatabasesec` secret and specify the key-value pairs for a username and password by using the `--from-literal` option. 

    ```
    ibmcloud ce secret create -n mydatabasesec --from-literal username=reader --from-literal password=abcd
    ```
    {: pre}

2. View details about the `mydatabasesec` secret by using the `secret get` command. The values for the `password` and `username` keys of the secret are encoded.  

    ```
    ibmcloud ce secret get -n mydatabasesec 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting secret mydatabasesec...
    ...

    Data:
    ---
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

3. Set an environment variable on a job to reference the full `mydatabasesec` secret.  Use the `--env-from-secret NAME` option where `NAME` specifies to reference the full secret. Because the `busybox` image does not print any output by default, the `-c env` command option specifies to print all the environment variables in the container. 

    ```
    ibmcloud ce job create -n demo -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

4. (Optional) View the details of the `demo` job. The output displays the full reference to the `mydatabasesec` secret. 

    ```
    ibmcloud ce job get -n demo
    ```
    {: pre}

    **Example output**
    
    ```
    ...

    Containers:
        Arguments:
        Commands:
        env
        Environment Variables:
        Reference Type         Name  Value  Reference Name  Reference Key
        Secret full reference               mydatabasesec
        Image:                  busybox
        Name:                   demo
    ...
    ```
    {: screen}

5. Run a job that uses the configuration of the `demo` job. 

    ```
    ibmcloud ce jobrun submit --name demo1 --job demo
    ```
    {: pre}

6. Display the logs of a running instance of the `demo1` jobrun. You can use the `jobrun get --name demo1` command to display details of this jobrun including the instances of the jobrun. In this example, display the logs of the running instance of `demo1-0-0` where `demo1` is the jobrun name, `0` is the `arrayindex` and `0` is the `retryindex`. Notice in the log output that the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce jobrun logs --instance demo1-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'demo1-0-0'...
    ...

    username=reader
    password=abcd
    ...
    ```
    {: screen}

7. Update the `mydatabasesec` secret to add a key by using `--from-file` option. This option uses the format `--from-file FILE` or `--from-file KEY=FILE`. In the following command, `certificate` is the key and `cert.pem` is the name of the file.

    ```
    ibmcloud ce secret update -n mydatabasesec --from-file certificate=cert.pem
    ```
    {: pre}

8.  View details about the updated `mydatabasesec` secret by using the `secret get` command. The secret now contains 3 keys, `certificate`, `password`, and `username`. Secret values are encoded.

    ```
    ibmcloud ce secret get -n mydatabasesec 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting secret mydatabasesec...
    ...

    Data:
    ---
    certificate: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tLS0tDQphc2RmO2Frc2pkZmxrYWpzZGZsa2phc2xka2ZqYWxza2RqZmxha3NqZGZsaw0KLS0tLS1FTkQgQ0VSVEZJQ0lBVEUtLS0tLS0tLS0t
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

9. Run a job that uses the `demo` job. Previously, you referenced the full secret `mydatabasesec` from the `demo` job. For a job to use the updated secret with the added `certificate` key-value pair, submit a new jobrun. If you are using apps instead of a job, an app must be restarted to use the updated secret with the additional key.

    ```
    ibmcloud ce jobrun submit --name demo2 --job demo
    ```
    {: pre}

10. Display the logs of a running instance of the `demo2` jobrun. You can use the `jobrun get --name demo2` command to display details of this jobrun including the instances of the jobrun. In this example, display the logs of the running instance of `demo2-0-0` where `demo2` is the jobrun name, `0` is the `arrayindex` and `0` is the `retryindex`. Notice in the output the `certificate`, `username`, and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded.

    ```
    ibmcloud ce jobrun logs --instance demo2-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'demo2-0-0'...
    ...

    username=reader
    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=abcd
    ...
    ```
    {: screen}

## Referencing individual keys of a configmap with the CLI
{: #secretcm-reference-keyref-cli}

In this scenario, let's create a configmap that contains multiple key-value pairs and then reference specific keys in a job. While this scenario uses a configmap, you can use the same general steps to reference individual keys with a secret by substituting `secret` for `configmap` in the commands.  

1. Create the `mydatabase` configmap and specify the key-value pairs for a name and a URL by using the `--from-literal KEY=VALUE` option.

    ```
    ibmcloud ce configmap create -n mydatabasecm --from-literal name=myname --from-literal url=myurl
    ```
    {: pre}

2. View details about the `mydatabasecm` configmap by using the `configmap get` command. 

    ```
    ibmcloud ce configmap get -n mydatabasecm 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting configmap 'mydatabasecm'....
    ...

    Data:
    ---
    name: myname
    url: myurl
    ```
    {: screen}

3. Set an environment variable on a job to reference the `url` key in the `mydatabasecm` configmap. Use the `--env-from-configmap NAME:KEY_A,KEY_B` option where `NAME:KEY_A` specifies to reference the `KEY_A` of the configmap. 

    ```
    ibmcloud ce job create --name keydemo --image busybox --command env --env-from-configmap mydatabasecm:url 
    ```
    {: pre}

4. Run a job that uses the `keydemo` job. 

    ```
    ibmcloud ce jobrun submit -name keydemo1 --job keydemo
    ```
    {: pre}

5. Display the logs of a running instance of the `keydemo1` jobrun. You can use the `jobrun get --name keydemo1` command to display details of this jobrun including the instances of the jobrun. Notice in the output that `url` is the only referenced key and that the `name` key is not referenced by the job.  

    ```
    ibmcloud ce jobrun logs --instance keydemo1-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'keydemo1-0-0'...
    ...

    url=myurl
    ...
    ```
    {: screen}

## Overriding references with the CLI
{: #secretcm-reference-overfull-cli}

You can override referenced secrets and configmaps. The following scenarios can be completed for secrets or configmaps.

### Scenario A.  Override a fully referenced secret with another fully referenced secret
{: #secretcm-reference-overfull-withfull-cli}

Full references override other full references in the order in which they are set (the last referenced set overrides the first set).
{: shortdesc}

In this scenario, let's create a new `mydatabasesec-writer` secret with the `username` and `password` keys and then override `username` and `password` keys in the previously created `mydatabasesec` secret. The `mydatabasesec` secret contains the `username=reader` and `password=abcd` keys. 

1. Set an environment variable on the `writerjob` job to reference the full `mydatabasesec` secret, which was created previously. The `mydatabasesec` secret contains the `username=reader` and `password=abcd` keys.  

    ```
    ibmcloud ce job create -n writerjob -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerjob` job. The output displays the full reference to the `mydatabasesec` secret. 

    ```
    ibmcloud ce job get -n writerjob
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'writerjob'...
    ...

    Containers:
        Arguments:
        Commands:
        env
        Environment Variables:
        Reference Type         Name  Value  Reference Name  Reference Key
        Secret full reference               mydatabasesec
        Image:                  busybox
        Name:                   writerjob
    ...
    ```
    {: screen}

3. Run a job that uses the `writerjob` job. 

    ```
    ibmcloud ce jobrun submit --name writerjob1 --job writerjob
    ```
    {: pre}

4. Display the logs of a running instance of the `writerjob1` jobrun. You can use the `jobrun get --name writerjob1` command to display details of this jobrun including the instances of the jobrun. Notice in the output the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 
    ```
    ibmcloud ce jobrun logs --instance writerjob1-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'writerjob1-0-0'...
    ...

    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=abcd
    username=reader
    ...
    ```
    {: screen}

5. Create the `mydatabasesec-writer` secret and specify the key-value pairs for a username and password by using the `--from-literal` option. 

    ```
    ibmcloud ce secret create --name mydatabasesec-writer --from-literal username=writer --from-literal password=wxyz
    ```
    {: pre}

6. View details about the `mydatabasesec-writer` secret by using the `secret get` command. The values for the `password` and `username` keys of the secret are encoded.  

    ```
    ibmcloud ce secret get -n mydatabasesec-writer 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting secret mydatabasesec-writer...
    ...

    Data:
    ---
    password: d3h5eg==
    username: d3JpdGVy
    ```
    {: screen}

7. Update the `writerjob` job to reference the full `mydatabasesec-writer` secret. 

    ```
    ibmcloud ce job update --name writerjob --env-from-secret mydatabasesec-writer
    ```
    {: pre}

8. (Optional) View details of the updated `writerjob` job. The job fully references the `mydatabasesec` and the `mydatabase-writer` secrets. 

    ```
    ibmcloud ce job get -n writerjob 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'writerjob'...
    ...

    Containers:
        Arguments:
        Commands:
        env
        Environment Variables:
        Reference Type         Name  Value  Reference Name        Reference Key
        Secret full reference               mydatabasesec
        Secret full reference               mydatabasesec-writer
        Image:                  busybox
        Name:                   writerjob
    ...
    ```
    {: screen}

9. Run a job that uses the `writerjob` job. Because the `writerjob` job was updated to reference both the `mydatabasesec` secret and the `mydatabasesec-writer` secret and both of these secrets include keys for `username` and `password`, the last referenced full secret `mydatabasesec-writer` overrides the  `mydatabasesec` secret. 

    For a jobrun to use the updated configuration of a job with the updates to its fully referenced secrets, run a new job. If you are using apps instead of a job, an application must be restarted to use the secret with the overridden keys.

    ```
    ibmcloud ce jobrun submit --name writerjob2 --job writerjob
    ```
    {: pre}

10. Display the logs of a running instance of the `writerjob2` jobrun. You can use the `jobrun get --name writerjob2` command to display details of this jobrun including the instances of the jobrun. Notice in the output the `username` and `password` keys of the `mydatabasesec-writer` secret overrode the keys of the `mydatabasesec` secret. Secret values are added to the environment decoded. 

        ```
        ibmcloud ce jobrun logs --instance writerjob2-0-0
        ```
        {: pre}


    **Example output**
            
            ```
            Logging job run instance 'writerjob2-0-0'...
            ...

            certificate=-----BEGIN CERTIFICATE--------
            asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
            -----END CERTFICIATE----------
            password=wxyz
            username=writer
            ...
            ```
            {: screen}

### Scenario B.  Override a fully referenced secret with a key reference
{: #secretcm-reference-overfull-withkey-cli}

References to a key in a secret or configmap always overrides a full reference to a secret or configmap when the key that is used resides in a fully referenced  secret or configmap, without regard for order.
{: shortdesc}

In this scenario, let's use the previously created `mydatabasesec` and `mydatabasesec-writer` secrets and reference keys within the secrets from a job. 

1. Set an environment variable on a `writerpic` job to reference specific keys in the `mydatabasesec` and `mydatabasesec-writer` secrets. The `mydatabasesec` secret contains the `username=reader`, `password=abcd`, and `certificate=cert.pem` keys. The `mydatabasesec-writer` secret contains the `username=writer` and `password=wxyz` keys.  

    ```
    ibmcloud ce job create -n writerpick -i busybox -c env --env-from-secret mydatabasesec-writer:username --env-from-secret mydatabasesec-writer:password --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerpick` job. The output displays the full reference to the `mydatabasesec` secret and the key reference to the `password` and `username` keys of the `mydatabasesec-writer` secret. 

    ```
    ibmcloud ce job get -n writerpick
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'writerpick'...
    ...

    Containers:
        Arguments:
        Commands:
        env
        Environment Variables:
        Reference Type         Name      Value  Reference Name        Reference Key
        Secret full reference                   mydatabasesec
        Secret key reference   password         mydatabasesec-writer  password
        Secret key reference   username         mydatabasesec-writer  username
        Image:                  busybox
        Name:                   writerpick
    ...
    ```
    {: screen}

3. Run a job that uses the `writerpick` job. 

    ```
    ibmcloud ce jobrun submit --name writerpick1 --job writerpick
    ```
    {: pre}

4. Display the logs of a running instance of the `writerpick1` jobrun. You can use the `jobrun get --name writerpick1` command to display details of this jobrun including the instances of the jobrun. Because the `writerpick` job updated to reference specific keys in the `mydatabasesec-writer` secret and to reference the full `mydatabasesec` secret, the reference to the `username` and `password` keys in the `mydatabasesec-writer` secret overrides the reference to the full secret. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce jobrun logs --instance writerpick1-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'writerpick1-0-0'...
    ...

    username=writer
    certificate=-----BEGIN CERTIFICATE--------
    asdf;aksjdflkajsdflkjasldkfjalskdjflaksjdflk
    -----END CERTFICIATE----------
    password=wxyz
    ...
    ```
    {: screen}

### Scenario C.  Override key references with new keys
{: #secretcm-reference-overkey-withkey-cli}

You can update the reference to a specific key in a secret or configmap and override the value with a new value. 
{: shortdesc}

In this scenario, let's use the previously created `mydatabasecm` configmap, which contains the `url:myurl` key to update the value of the key.

1. Set an environment variable on a `keyref` job to reference a specific key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce job create -n keyref -i busybox -c env --env-from-configmap mydatabasecm:url
    ```
    {: pre}

2. (Optional) View the details of the `keyref` job. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce job get -n keyref
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'keyref'...
    ...

    Containers:
        Arguments:
        Commands:
        env
        Environment Variables:
        Reference Type           Name  Value  Reference Name  Reference Key
        ConfigMap key reference  url          mydatabasecm    url
        Image:                  busybox
        Name:                   keyref
    ...
    ```
    {: screen}

3. Run a job that uses the `keyref` job. 

    ```
    ibmcloud ce jobrun submit --name keyref1 --job keyref
    ```
    {: pre}

4.  Display the logs of a running instance of the `keyref1` jobrun. You can use the `jobrun get --name keyref1` command to display details of this jobrun including the instances of the jobrun. The jobrun used the `url=myurl` key reference. 

    ```
    ibmcloud ce jobrun logs --instance keyref1-0-0
    ```
    {: pre}

    **Example output**
    
    ```
    Logging job run instance 'keyref1-0-0'...
    ...

    url=myurl
    ...
    ```
    {: screen}

5. Update the `keyref` job to override the `url=myurl` with a new key. Use the `--env` option to update the `url` key. The `--env` option on the [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) command sets environment variables for the job in NAME=VALUE format.

    ```
    ibmcloud ce job update --name keyref --env url=newurl  
    ```
    {: pre}

6. (Optional) View the details of the `keyref` job. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce job get -n keyref
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'keyref'...
    ...

    Containers:
      Arguments:
      Commands:
        env
      Environment Variables:
        Reference Type  Name  Value   Reference Name  Reference Key
        Literal         url   newurl
      Image:                  busybox
      Name:                   keyref
    ...
    ```
    {: screen}

## Removing full references with the CLI
{: #secretcm-reference-fullremove-cli}

You can remove a fully referenced secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the fully referenced `mydatabasesec` secret from the `demo` job.  

1. Update the `demo` job to remove the reference to the `mydatabasesec` secret.  

    ```
    ibmcloud ce job update -n demo --env-from-secret-rm mydatabasesec 
    ```
    {: pre}

2. View the details of the `demo` job. The output illustrates that the reference to the `mydatabasesec` secret is removed. 

    ```
    ibmcloud ce job get -n demo 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'demo'...
    ...
    Containers:
      Arguments:
      Commands:
        env
      Environment Variables:
      Image:                  busybox
      Name:                   demo
    ...
    ```
    {: screen}

## Removing key references with the CLI
{: #secretcm-reference-keyremove-cli}

You can remove a referenced key in a secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the `url` key from the `keyref` job. 

Even though the `--env-from-configmap` option was used on a job to reference the `url` key in the `mydatabasecm` configmap, you can use the `--env-rm` option to remove individual keys. You can use the `--env-rm` option with the [`job update`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-update) or [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) commands to remove key references regardless of whether the keys are individual key references in a secret or configmap, or whether the keys were directly set on a job or app with the `--env` option. 
{: tip}

1. Update the `keydef` job to remove the reference to the `url` key.  

    ```
    ibmcloud ce job update -name keyref --env-rm url 
    ```
    {: pre}

2. View the details of the `keyref` job. The output illustrates that the reference to the `url` key is removed.  

    ```
    ibmcloud ce job get -n keyref 
    ```
    {: pre}

    **Example output**
    
    ```
    Getting job 'keyref'...
    ...

    Containers:
      Arguments:
      Commands:
        env
      Environment Variables:
      Image:                  busybox
      Name:                   keyref
    ...
    ```
    {: screen}

