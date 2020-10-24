---

copyright:
  years: 2020
lastupdated: "2020-10-23"

keywords: code engine

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
{:note .note}
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


# CLI version history 
{: #cli_versions}

Find a summary of changes for each version of {{site.data.keyword.codeengineshort}} plug-in. Be sure to keep your CLI up-to-date so that you can use all of the available commands and flags.
{:shortdesc}

| Version | Release date | Changes |
| --------- | -------- | -------- |
| 0.4.2439 | 23 October 2020 | <ul><li>Added the `—ephemeral-storage` option to the `app create`, `app update`, and `app get` commands.</li><li>Fixed a bug where the incorrect size was appended to the build strategy name.</li><li>Renamed `build create --revision` option to `build create —commit`.</li><li>Changed the default for the `project create` command. A project is now selected for context after it is created, unless the `--no-select` option is specified.</li><li>Deprecated the `proj create --select` command option.</li></ul>|
| 0.4.2397 | 15 October 2020 | <ul><li>Added the `--from-env-file` option to the `configmap create`, `configmap update`, `secret create`, and `secret update` commands. These commands can now accept a file that contains one or more lines that match a `KEY=VALUE` format.</li><li>Renamed the application request timeout option on the `app create` and `app update` commands from `--timeout` to `--request-timeout`, to reduce confusion when using wait-related options with these commands.</li><li>Added the `--strategy` and `size` options to the `build update` command.</li><li>Updated the `subscription cos get` command to display resource conditions.</li><li>Updated the `app bind` and `job bind` commands to wait by default for bindings to become ready. </li><li>Updated the `app bind` command to wait for a new revision to become ready.</li></ul>|
| 0.4.2365 | 06 October 2020 | <ul><li>Added support for {{site.data.keyword.cos_full_notm}} (COS) event sources. Use the `subscription cos` commands to manage COS event sources.</li></ul>|
| 0.4.2335 | 02 October 2020 | <ul><li>Added support for Ping event sources. Use the `subscription ping` commands to manage Ping event sources.</li><li> Added the `--arguments-clear` and `--commands-clear` options to the `app update`, `job update`, and `jobrun resubmit` commands to clear arguments and commands.</li><li>The `app create --concurrency` option now defaults to `0`. </li><li>Updated the display output of CPU information for the `app get`, `job get`, and `jobrun get` commands.</li><li>Improved the output of the `project get` and `project list` commands to no longer display expiry information when a project is being deleted.</li></ul> |
| 0.4.2276 | 25 September 2020 | <ul><li>Added the `build update` command.</li><li> Added the `--wait-timeout` option to the `app bind` and `job bind` commands to specify the time in seconds to wait for the service binding to be ready. If this option is not specified, the binding is performed asynchronously.</li></ul> |
| 0.4.2227 | 21 September 2020 | <ul><li>Added the `--wait` option to the `app update` command. This option specifies that the `app update` waits for the new revision to be ready before it exits.</li></ul> |
| 0.4.2217 | 18 September 2020 | <ul><li>Fixed issue that affected service bindings that are attached to jobs.</li><li>Added support for `job delete` to orphan associated `jobruns`.</li><li>Fixed issue that caused stalled `jobruns`.</li><li>Fixed messaging inconsistencies for `jobruns`.</li><li>Added support to `registry create` command for `password-from-file` option.</li><li>Alphabetized command namespaces.</li><li>Fixed issue that caused panic when instances are displayed.</li></ul> |
| 0.4.2192 | 15 September 2020 | <ul><li>Renamed `job` commands to `jobrun` commands. Use the `jobrun` commands to run and work with instances of your job.</li><li>Renamed `jobdef` commands to `job` commands. Use the `job` commands to create and work with job configuration information. </li><li>Updated the `jobrun logs` command to input an instance name instead of an index value. </li><li>Added `build` commands for building container images from your source code. Use the `build` commands to create and work with build configuration information. </li><li>Added `buildrun` commands to build container images from your source code. Use the `buildrun` commands to run and work with instances of your build. </li><li>Added `registry` commands to configure and work with image registry access secrets.</li><li>Added `repo` commands to configure and work with Git repository access secrets. </li><li>Removed the `--from-registry` option from the `secret create` command. Use the `secret` commands to work with generic secrets.</li><li>Simplified the display output of `get` and `list` commands.</li><li>Fixed bug where `app delete` fails to remove all app instances.</li><li>Improved the error message that is displayed when an account exceeds number of allowed projects. </li><li>Improved the CLI start time.</li><li>Deprecated the `project --target` command. Use `project select` instead to specify a project for context.</li></ul> |
| 0.3.1973 | 02 September 2020 | <ul><li>Added the `--retryindex` option to the `job logs` command. </li><li>Added aliases for the `--cmd` and `--arg` options to the `job run`, `job rerun`, `jobdef create`, and `jobdef update` commands. This addition is similar to the `--cmd` and `--arg` options for the `app create` and `app update` commands.</li><li>Added the `app logs` command to display the logs of an application instance. </li><li>Improved service binding output to display status with the `app get` and `jobdef get` commands.</li><li>Improved error tracing.</li><li>Improved the performance of the `app delete` command.</li><li>Updated job references to `v1beta1`.  Any jobs that were created prior to this CLI version are no longer accessible.</li><li>Updated the `job run`, `job rerun`, `jobdef create`, and `jobdef update` commands to limit the job name to 53 characters.</li><li>Updated the `job run` and `job rerun` commands to change the maximum for the `--array-indices` option to `9999`.</li><li>Updated the `project get` command to display the project name and ID.<li>Updated the output of the `project list` command to display expiry information for all regions.</li><li>Fixed an issue where the CLI attempted to delete service bindings during project deletion, even if no project was targeted.</li><li>Fixed an issue where job names longer than 30 characters in job logs were not handled properly.</li><li>Fixed an issue where the container name was set from the jobdef or job name, such that it is now set with the container name.</li><li>Fixed an issue where in some cases, the `--option` output fails to find `--output-jasonpath={some.path}`.</li><li>Fixed an issue where an invalid `kubeconfig` caused all project commands to fail. </li></ul> |
| 0.3.1802 | 21 August 2020 | <ul><li>Added `--output` option for `get` and `list` commands for projects, apps, job definitions, jobs, configmaps, and secrets. Use this option to show JSON, YAML, or jsonpath results. </li><li>Added support for jobs and applications to reference secrets and configmaps. </li><li>Added options to remove environment variables, secret references, and configmap references from jobs and applications. The options are  `--env-rm`, `--env-from-secret-rm`, and `--env-from-configmap-rm`. </li><li>Fixed an issue that prevented old tokens from being overwritten when `kubeconfig` files are merged.</li><li>Fixed an issue where the expiry date was not shown on `project get` command results.</li></ul> |
| 0.3.1712 | 17 August 2020 | <ul><li>Improved trace output for Kubernetes API calls and errors.</li><li>Fixed an issue with the `project target` command that caused merge errors when multiple `kubeconfig` files are merged.</li><li>Added alias `-f` for the `--from-file` option for the `configmap create`, `configmap update`, `secret create`, and `secret update` commands.</li><li>Added `--registry-secret` option for `job run`, `jobdef create`, and `jobdef update` commands.</li><li>Added the `--concurrency-target` option to `app create` and `app update` commands.</li></ul> |
| 0.3.1675 | 14 August 2020 | <ul><li>Added `job rerun` command to rerun a job based on the configuration of a previous job run.</li><li>If you do not specify values for `cpu` and `memory` when a job is run, the defaults from the `jobdef` are used.</li><li> The `job create` command is now an alias for `job run` command.</li><li>Deprecated `--arraysize`. Use `array-indices` instead.</li></ul> |
| 0.3.1535 | 04 August 2020 | <ul><li>Deprecated `--project-api` when you target projects. Use `ibmcloud target -r` to select the region where the project resides.</li><li>Added support for the environment variable `IBMCLOUD_CE_TERSE`. When this variable is set to `true`, the CLI reduces the amount of output.</li><li>Added `--user` option for managing applications.</li><li> Fixed bug where a secret or configmap fails to update correctly.</li><li>Fixed bug where token expiry prevented user from targeting new projects.</li><li>Fixed bug where apps show all the tags in a user's account.</li><li>Improved performance of project list.</li><li>Added display of failed job indices.</li><li>Improved error messaging to display more informative output.</li><li>Improved `--help` option output to dynamically wrap and resize based on terminal width.</li><li>Updated many strings.</li></ul> |
| 0.3.1415 | 22 July 2020 | <ul><li>Added `--port` option on `app create`, `app update`, and `app get` commands to specify the port where the application listens.</li><li> Show expiry information on `project list` command output.</li><li>Announcements displayed in CLI once per hour.</li><li>Updated many strings.</li></ul>
| 0.3.1363 | 17 July 2020 | <ul><li>Changed plug-in name to `code-engine`.</li><li>Added `project target` command, which moves target functions under `project` command.</li><li>Added `--kubectl` option on `project target` and `target` commands to append the project to the default Kubernetes configuration file.</li><li> Fix added to manage projects with spaces in project name.</li><li>Added `jobdef update` command.</li><li>Added announcement banner.</li><li>Updated many strings.</li></ul>
| 0.2.1250 | 10 July 2020 | <ul><li>Fixed inconsistency between `cpu/mem` units on `app` commands.</li><li>Removed `kubectl` dependencies.</li><li>Updated `delete` actions to require confirmation.</li><li>Consistent `project-api` support for `target` and `project create --target` commands.</li><li>The `--registry-secret` command correctly sets image pull secrets.</li><li>Fixed `app update` to prevent overwriting of `minscale/maxscale`.</li><li>Added warnings for project expiration.</li><li>Fixed service binding credential selection logic.</li><li>Updated many strings.</li></ul>
| 0.2.1093 | 19 June 2020 | <ul><li>Added `env-from-secret` and `env-from-configmap` to `app update` usage string.</li><li>Fixed `min-scale` and `max-scale`.</li><li>Alphabetized help output.</li><li>Fixed `app create --no-wait`, status URL not available.</li><li>Added number of instances to `app get` command output.</li><li>Added `command` and `argument` to application usage.</li><li>Fixed `create secret` command for registry.</li><li>Fixed application revision name logic.</li><li>Added aliases for `min-scale` and `max-scale`.</li><li>Fixed nil pointer on app update.</li><li>Added references for environment variables to `application get` command output.</li><li>Improved error message when no project is targeted.</li></ul> |
| 0.2.966 | 11 June 2020 | <ul><li>Added logic to require confirmation to delete a resource.</li><li>Added `--force` option to `delete` commands that currently default to `true`.</li><li>Fixed bug where `cluster-local` was not properly set.</li><li>Added service binding support for job definitions.</li><li>Added `command` and `argument` options for applications.</li><li>Added usage details for `job run`.</li><li>Removed `kubectl` dependencies for some `jobdef` commands.</li><li>Fixed bug where the app revision was not appended.</li><li>No longer use `gcc (cgo)` for Linux builds.</li><li>Added logic so that deleting a currently targeted project also removes the target.</li><li>Improved messages and formatting.</li><li>Application URLs that are provided by `create` and `list` commands default to `https`.</li></ul> |
{: caption="Changes in the IBM Cloud {{site.data.keyword.codeengineshort}} CLI" caption-side="top"} 
