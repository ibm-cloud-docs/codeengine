---

copyright:
  years: 2020
lastupdated: "2020-09-10"

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

The following table lists command information for setting environment variables on jobs and apps to reference secrets and configmaps.

| Action| Option format| Commands for jobs | Commands for apps |
|-----------------|-----------------|--------------|-----|
| Referencing a full secret | `--env-from-secret NAME` where `NAME` is the name of the secret. | [`jobdef create`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-create), [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update), [`job run`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-run), [`job rerun`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-rerun) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing a full configmap | `--env-from-configmap NAME` where `NAME` is the name of the configmap. |  [`jobdef create`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-create), [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update), [`job run`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-run), [`job rerun`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-rerun) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing specific keys in a secret | `--env-from-secret NAME:KEY_A,KEY_B` where `KEY` is the key of a key-value pair. |  [`jobdef create`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-create), [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update), [`job run`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-run), [`job rerun`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-rerun) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Referencing specific keys in a configmap | `--env-from-configmap NAME:KEY_A,KEY_B` where `KEY` is the key of a key-value pair. | [`jobdef create`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-create), [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update), [`job run`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-run), [`job rerun`](/docs/codeengine?topic=codeengine-kn-cli#cli-job-rerun) | [`app create`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-create), [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update)  |
| Removing a fully referenced secret | `--env-from-secret-rm NAME` where `NAME` is the name of the secret. | [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing a fully referenced configmap | `--env-from-configmap-rm NAME` where `NAME` is the name of the configmap. | [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing referenced keys in a secret | `--env-rm KEY_A --env-rm KEY_B` where `KEY` is the key of a key-value pair. | [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
| Removing referenced keys in a configmap | `--env-rm KEY_A --env-rm KEY_B` where `KEY` is the key of a key-value pair. | [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) | [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) |
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
    Successfully retrieved secret 'mydatabasesec'.
    ...

    Data:
    ---
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

3. Set an environment variable on a job definition to reference the full `mydatabasesec` secret.  Use the `--env-from-secret NAME` option where `NAME` specifies to reference the full secret. Because the `busybox` image does not print any output by default, the `-c env` command option specifies to print all the environment variables in the container. 

    ```
    ibmcloud ce jobdef create -n demo -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

4. (Optional) View the details of the `demo` job definition. The output displays the full reference to the `mydatabasesec` secret. 

    ```
    ibmcloud ce jobdef get -n demo
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

5. Run a job that uses the `demo` job definition. 

    ```
    ibmcloud ce job run -n demo1 --jd demo
    ```
    {: pre}

6. Display the job logs of the `demo1` job. Notice in the output the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce job logs -n demo1
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully.
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
    Successfully retrieved secret 'mydatabasesec'.
    ...

    Data:
    ---
    certificate: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tLS0tDQphc2RmO2Frc2pkZmxrYWpzZGZsa2phc2xka2ZqYWxza2RqZmxha3NqZGZsaw0KLS0tLS1FTkQgQ0VSVEZJQ0lBVEUtLS0tLS0tLS0t
    password: YWJjZA==
    username: cmVhZGVy
    ```
    {: screen}

9. Run a job that uses the `demo` job definition. Previously, you referenced the full secret `mydatabasesec` from the `demo` job definition. For a job to use the updated secret with the added `certificate` key-value pair, run a new job. If you are using apps instead of a job, an application must be restarted to use the updated secret with the additional key.

    ```
    ibmcloud ce job run -n demo2 --jd demo
    ```
    {: pre}

10. Display the job logs of the `demo2` job. Notice in the output the `certificate`, `username`, and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce job logs -n demo2
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully
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

1. Create the `mydatabase` configmap and specify the key-value pairs for a name and a url by using the `--from-literal KEY=VALUE` option.

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
    Successfully retrieved configmap 'mydatabasecm'.
    ...

    Data:
    ---
    name: myname
    url: myurl
    ```
    {: screen}

3. Set an environment variable on a job definition to reference the `url` key in the `mydatabasecm` configmap. Use the `--env-from-configmap NAME:KEY_A,KEY_B` option where `NAME:KEY_A` specifies to reference the `KEY_A` of the configmap. 

    ```
    ibmcloud ce jobdef create -n keydemo -i busybox -c env --env-from-configmap mydatabasecm:url 
    ```
    {: pre}

4. Run a job that uses the `keydemo` job definition. 

    ```
    ibmcloud ce job run -n keydemo1 --jd keydemo
    ```
    {: pre}

5. Display the job logs of the `keydemo1` job. Notice in the output that `url` is the only referenced key and that the `name` key is not referenced by the job.  

    ```
    ibmcloud ce job logs -n keydemo1
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully
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

1. Set an environment variable on the `writerjob` job definition to reference the full `mydatabasesec` secret, which was created previously. The `mydatabasesec` secret contains the `username=reader` and `password=abcd` keys.  

    ```
    ibmcloud ce jobdef create -n writerjob -i busybox -c env --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerjob` job definition. The output displays the full reference to the `mydatabasesec` secret. 

    ```
    ibmcloud ce jobdef get -n writerjob
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

3. Run a job that uses the `writerjob` job definition. 

    ```
    ibmcloud ce job run -n writerjob1 --jd writerjob
    ```
    {: pre}

4. Display the job logs of the `writerjob1` job. Notice in the output the `username` and `password` keys of the full secret `mydatabasesec` are displayed. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce job logs -n writerjob1
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully.
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
    ibmcloud ce secret create -n mydatabasesec-writer --from-literal username=writer --from-literal password=wxyz
    ```
    {: pre}

6. View details about the `mydatabasesec-writer` secret by using the `secret get` command. The values for the `password` and `username` keys of the secret are encoded.  

    ```
    ibmcloud ce secret get -n mydatabasesec-writer 
    ```
    {: pre}

    **Example output**
    
    ```
    Successfully retrieved secret 'mydatabasesec-writer'.
    ...

    Data:
    ---
    password: d3h5eg==
    username: d3JpdGVy
    ```
    {: screen}

7. Update the `writerjob` job definition to reference the full `mydatabasesec-writer` secret. 

    ```
    ibmcloud ce jobdef update -n writerjob --env-from-secret mydatabasesec-writer
    ```
    {: pre}

8. (Optional) View details of the updated `writerjob` job definition. The job definition fully references the `mydatabasesec` and the `mydatabase-writer` secrets. 

    ```
    ibmcloud ce jobdef get -n writerjob 
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

9. Run a job that uses the `writerjob` job definition. Because the `writerjob` job definition was updated to reference both the `myddatabasesec` secret and the `mydatabasesec-writer` secret and both of these secrets include keys for `username` and `password`, the last referenced full secret `mydatabasesec-writer` overrides the  `mydatabasesec` secret. 

    For a job to use the updated job definition with the updates to its fully referenced secrets, run a new job. If you are using apps instead of a job, an application must be restarted to use the secret with the overridden keys.

    ```
    ibmcloud ce job run -n writerjob2 --jd writerjob
    ```
    {: pre}

10.  Display the job logs of the `writerjob2` job. Notice in the output the `username` and `password` keys of the `mydatabasesec-writer` secret overrode the keys of the `mydatabasesec` secret. Secret values are added to the environment decoded. 

        ```
        ibmcloud ce job logs -n writerjob2
        ```
        {: pre}


    **Example output**
            
            ```
            Command 'job logs' performed successfully
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

In this scenario, let's use the previously created `mydatabasesec` and `mydatabasesec-writer` secrets and reference keys within the secrets from a job definition. 

1. Set an environment variable on a `writerpic` job definition to reference specific keys in the `mydatabasesec` and `mydatabasesec-writer` secrets. The `mydatabasesec` secret contains the `username=reader`, `password=abcd`, and `certificate=cert.pem` keys. The `mydatabasesec-writer` secret contains the `username=writer` and `password=wxyz` keys.  

    ```
    ibmcloud ce jobdef create -n writerpick -i busybox -c env --env-from-secret mydatabasesec-writer:username --env-from-secret mydatabasesec-writer:password --env-from-secret mydatabasesec 
    ```
    {: pre}

2. (Optional) View the details of the `writerpick` job definition. The output displays the full reference to the `mydatabasesec` secret and the key reference to the `password` and `username` keys of the `mydatabasesec-writer` secret. 

    ```
    ibmcloud ce jobdef get -n writerpick
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

3. Run a job that uses the `writerpick` job definition. 

    ```
    ibmcloud ce job run -n writerpick1 --jd writerpick
    ```
    {: pre}

4.  Display the job logs of the `writerpick1` job. Because the `writerpick` job definition was updated to reference specific keys in the `mydatabasesec-writer` secret and to reference the full `mydatabasesec` secret, the reference to the `username` and `password` keys in the `mydatabasesec-writer` secret overrides the reference to the full secret. Secret values are added to the environment decoded. 

    ```
    ibmcloud ce job logs -n writerpick1
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully.
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

1. Set an environment variable on a `keyref` job definition to reference a specific key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce jobdef create -n keyref -i busybox -c env --env-from-configmap mydatabasecm:url
    ```
    {: pre}

2. (Optional) View the details of the `keyref` job definition. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce jobdef get -n keyref
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

3. Run a job that uses the `keyref` job definition. 

    ```
    ibmcloud ce job run -n keyref1 --jd keyref
    ```
    {: pre}

4.  Display the job logs of the `keyref1` job. The job used the `url=myurl` key reference. 

    ```
    ibmcloud ce job logs -n keyref1 
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'job logs' performed successfully.
    ...

    url=myurl
    ...
    ```
    {: screen}

5. Update the `keyref` job definition to override the `url=myurl` with a new key. Use the `--env` option to update the `url` key. The `--env` option on the [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) command sets environment variables for instances of the job definition in NAME=VALUE format.

    ```
    ibmcloud ce jobdef update -n keyref --env url=newurl  
    ```
    {: pre}

6. (Optional) View the details of the `keyref` job definition. The output displays the key reference to the `url` key in the `mydatabasecm` configmap. 

    ```
    ibmcloud ce jobdef get -n keyref
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

## Removing full references with the CLI
{: #secretcm-reference-fullremove-cli}

You can remove a fully referenced secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the fully referenced `mydatabasesec` secret from the `demo` job definition.  

1. Update the `demo` job definition to remove the reference to the `mydatabasesec` secret.  

    ```
    ibmcloud ce jobdef update -n demo --env-from-secret-rm mydatabasesec 
    ```
    {: pre}

2. View the details of the `demo` job definition. The output displays the full reference to the `mydatabasesec` secret.

    ```
    ibmcloud ce jobdef get -n demo 
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully
    ...
    Name:              keyref

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

## Removing key references with the CLI
{: #secretcm-reference-keyremove-cli}

You can remove a referenced key in a secret or configmap from a job or app.  
{: shortdesc}

In this scenario, let's remove the `url` key from the `keyref` job definition. 

Even though the `--env-from-configmap` option was used on the job definition to reference the `url` key in the `mydatabasecm` configmap, you can use the `--env-rm` option to remove individual keys. You can use the `--env-rm` option with the [`jobdef update`](/docs/codeengine?topic=codeengine-kn-cli#cli-jobdef-update) or [`app update`](/docs/codeengine?topic=codeengine-kn-cli#cli-application-update) commands to remove key references regardless of whether the keys are individual key references in a secret or configmap, or whether the keys were directly set on a job definition or app with the `--env` option. 
{: tip}

1. Update the `keydef` job definition to remove the reference to the `url` key.  

    ```
    ibmcloud ce jobdef update -n keyref --env-rm url 
    ```
    {: pre}

2. View the details of the `keyref` job definition. The output illustrates that the reference to the `url` key is removed.  

    ```
    ibmcloud ce jobdef get -n keyref 
    ```
    {: pre}

    **Example output**
    
    ```
    Command 'jobdef get' performed successfully.
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

