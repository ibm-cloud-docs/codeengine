---

copyright:
  years: 2020
lastupdated: "2020-08-14"

keywords: code engine

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# CLI version history 
{: #cli_versions}

Find a summary of changes for each version of {{site.data.keyword.codeengineshort}} plug-in. Be sure to keep your CLI up-to-date so that you can use all of the available commands and flags.
{:shortdesc}

| Version | Release date | Changes |
| --------- | -------- | -------- |
| 0.3.1675 | 14 August 2020 | <ul><li>Added `job rerun` command to rerun a job based on the configuration of a previous job run.</li><li>If you do not specify values for `cpu` and`memory` when running a job, the defaults from the jobdef are used.</li><li> The `job create` command is now an alias for `job run` command.</li><li>Deprecated `--arraysize`. Use `array-indices` instead.</li></ul> |
| 0.3.1535 | 04 August 2020 | <ul><li>Deprecated `--project-api` when you target projects. Use `ibmcloud target -r` to select the region where the project resides.</li><li>Added support for the environment variable `IBMCLOUD_CE_TERSE`. When this variable is set to `true`, the CLI reduces the amount of output.</li><li>Added `--user` option for managing applications.</li><li> Fixed bug where a secret or configmap fails to update correctly.</li><li>Fixed bug where token expiry prevented user from targeting new projects.</li><li>Fixed bug where apps show all the tags in a user's account.</li><li>Improved performance of project list.</li><li>Added display of failed job indices.</li><li>Improved error messaging to display more informative output.</li><li>Improved `--help` option output to dynamically wrap and resize based on terminal width.</li><li>Updated many strings.</li></ul> |
| 0.3.1415 | 22 July 2020 | <ul><li>Added `--port` option on `app create`, `app update`, and `app get` commands to specify the port where the application listens.</li><li> Show expiry information on `project list` command output.</li><li>Announcements displayed in CLI once per hour.</li><li>Updated many strings.</li></ul>
| 0.3.1363 | 17 July 2020 | <ul><li>Changed plug-in name to `code-engine`.</li><li>Added `project target` command, which moves target functions under `project` command.</li><li>Added `--kubectl` option on `project target` and `target` commands to append the project to the default Kubernetes configuration file.</li><li> Fix added to manage projects with spaces in project name.</li><li>Added `jobdef update` command.</li><li>Added announcement banner.</li><li>Updated many strings.</li></ul>
| 0.2.1250 | 10 July 2020 | <ul><li>Fixed inconsistency between `cpu/mem` units on `app` commands.</li><li>Removed `kubectl` dependencies.</li><li>Updated `delete` actions to require confirmation.</li><li>Consistent `project-api` support for `target` and `project create --target` commands.</li><li>The `--registry-secret` command correctly sets image pull secrets.</li><li>Fixed `app update` to prevent overwriting of `minscale/maxscale`.</li><li>Added warnings for project expiration.</li><li>Fixed service binding credential selection logic.</li><li>Updated many strings.</li></ul>
| 0.2.1093 | 19 June 2020 | <ul><li>Added `env-from-secret` and `env-from-configmap` to `app update` usage string.</li><li>Fixed `min-scale` and `max-scale`.</li><li>Alphabetized help output.</li><li>Fixed `app create --no-wait`, status URL not available.</li><li>Added number of instances to `app get` command output.</li><li>Added `command` and `argument` to application usage.</li><li>Fixed `create secret` command for registry.</li><li>Fixed application revision name logic.</li><li>Added aliases for `min-scale` and `max-scale`.</li><li>Fixed nil pointer on app update.</li><li>Added references for environment variables to `application get` command output.</li><li>Improved error message when no project is targeted.</li></ul> |
| 0.2.966 | 11 June 2020 | <ul><li>Added logic to require confirmation to delete a resource.</li><li>Added `--force` option to `delete` commands that currently default to `true`.</li><li>Fixed bug where `cluster-local` was not properly set.</li><li>Added service binding support for job definitions.</li><li>Added `command` and `argument` options for applications.</li><li>Added usage details for `job run`.</li><li>Removed `kubectl` dependencies for some `jobdef` commands.</li><li>Fixed bug where the app revision was not appended.</li><li>No longer use `gcc (cgo)` for Linux builds.</li><li>Added logic so that deleting a currently targeted project also removes the target.</li><li>Improved messages and formatting.</li><li>Application URLs that are provided by `create` and `list` commands default to `https`.</li></ul> |
{: caption="Changes in the IBM Cloud {{site.data.keyword.codeengineshort}} CLI" caption-side="top"}
