---

copyright:
  years: 2020
lastupdated: "2020-09-29"

keywords: event, code engine, ping, cos, Cloud object storage, object storage, trigger

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


# Eventing for {{site.data.keyword.codeenginefull_notm}}
{: #eventing}

You can extend the functionality of your applications by including messages (events) from event producers. Your application can then react to these events and perform actions based on them.
{: shortdesc}

{{site.data.keyword.codeenginefull}} includes a [ping event producer](#eventing-ping) which generates an event at regular intervals.



## Adding a ping event to your application
{: #eventing-ping}

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-kn-install-cli).
- [Create and target a project](/docs/codeengine?topic=codeengine-manage-project).

### Creating a ping event to an existing app
{: #eventing-ping-existing-app}

You can add a ping event to your application through the CLI by using the `subscription ping create` command. 

```
ibmcloud ce subscription ping create --name NAME --destination APPLICATION --schedule CRON
```
{: pre}
<table>
<caption><code>subscription ping create</code> components</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>subscription ping create</code></td>
<td>The command to create the ping event producer.</td>
</tr>
<tr>
<td><code>--name</code></td>
<td>The name of the Ping event source.
</td>
</tr>
<tr>
<td><code>--destination</code></td>
<td>The addressable destination to where events are sent. This destination is a {{site.data.keyword.codeengineshort}} application.</td>
</tr>
<tr>
<td><code>--schedule</code></td>
<td>Schedule specification in crontab format; for example `*/2 * * * *` for every two minutes. By default, the Ping event is triggered every minute.</td>
</tr>
</table>

For example, to create a ping subscription called `mypingevent` that attaches to an existing app called `myapp` that fires every day at midnight,

```
ibmcloud ce subscription ping create --name mypingevent --destination myapp --schedule 0 0 * * *
```
{: pre}

To verify that your ping subscription was successful, run `ibmcloud ce subscription ping get --name mypingevent`. 

**Example output**

```
Got Ping source 'mypingevent'

Name:         mypingevent  
Destination:  http://myapp.74c96c5f-f73a.svc.cluster.local  
Schedule:     0 0 * * *  
Data:           
Age:          5m46s  
Ready:        true  
Events:
Type    Reason                Age                    From                   Messages  
Normal  PingSourceReconciled  5m45s (x3 over 5m46s)  pingsource-controller  PingSource reconciled: "74c86d5f-f73a/mypingevent"  
Normal  FinalizerUpdate       5m45s                  pingsource-controller  Updated "mypingevent" finalizers 
```
{: screen}

From this output, you can see that the destination application is `http://myapp.74c96c5f-f73a.svc.cluster.local`, the schedule is `0 0 * * *` (midnight), and the Ready state is `true`.

### Creating a ping event for an app you haven't yet created
{: #eventing-ping-new-app}

You can also create a ping subscription to an application that is not yet created by using the `--force` option. Try creating a ping event for an app that doesn't exist yet, for example, called `myapp2`.

```
ibmcloud ce subscription ping create --name mypingevent2 --destination myapp2 --force
```
{: pre}

Run `subscription ping get`

```
ibmcloud ce subscription ping get --name mypingevent2
```
{: pre}

**Example output**

```
Got Ping source 'mypingevent2'

Name:         mypingevent2  
Destination:    
Schedule:     * * * * *  
Data:           
Age:          52s  
Ready:        false  
Events:
Type     Reason           Age                 From                   Messages  
Normal   FinalizerUpdate  52s                 pingsource-controller  Updated "mypingevent2" finalizers  
```
{: screen}

Note that the destination field is empty and the Ready state is `false`. Now create an app called `myapp2` and run `subscription ping get` command again.

**Example output**

```
Got Ping source 'mypingevent2'

Name:         mypingevent2  
Destination:  http://myapp2.74c96c5f-f73a.svc.cluster.local  
Schedule:     * * * * *  
Data:           
Age:          3m1s  
Ready:        true  
Events:
Type     Reason                Age                  From                   Messages  
Normal   FinalizerUpdate       3m1s                 pingsource-controller  Updated "mypingevent2" finalizers  
```
{: screen}

This time, the destination lists `myapp2` and the Ready state is `true`.

## Deleting a ping event

You can delete a ping event by running the `subscription ping delete` command. For example,

```
ibmcloud ce subscription ping delete --name mypingevent2`
```
{: pre}

If you delete an application, the ping event is not deleted, but instead moves to ready state `false`. If you recreate the app (or another application with the same name), your event reconnects and the ready state is `true`.
{: note}



