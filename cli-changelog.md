---

copyright:
  years: 2020
lastupdated: "2020-07-09"

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
| 0.2.1093 | 19 June 2020 | <ul><li>Added `env-from-secret` and `env-from-configmap` to `app update` usage string.</li><li>Fixed `min-scale` and `max-scale`.</li><li>Alphabetized help output.</li><li>Fixed `app create --no-wait`, status URL not available.</li><li>Added number of instances to `app get` command output.</li><li>Added `command` and `argument` to application usage.</li><li>Fixed `create secret` command for registry.</li><li>Fixed application revision name logic.</li><li>Added aliases for `min-scale` and `max-scale`.</li><li>Fixed nil pointer on app update.</li><li>Added references for environment variables to `application get` command output.</li><li>Improved error message when no project is targeted.</li></ul> |
| 0.2.966 | 11 June 2020 | <ul><li>Added logic to require confirmation to delete a resource.</li><li>Added `--force` option to `delete` commands that currently default to `true`.</li><li>Fixed bug where `cluster-local` was not properly set.</li><li>Added service binding support for job definitions.</li><li>Added `command` and `argument` options for applications.</li><li>Added usage details for `job run`.</li><li>Removed `kubectl` dependencies for some `jobdef` commands.</li><li>Fixed bug where the app revision was not appended.</li><li>No longer use `gcc (cgo)` for Linux builds.</li><li>Added logic so that deleting a project that's currently targeted also removes the target.</li><li>Improved messages and formatting.</li><li>Application URLs that are provided by `create` and `list` commands default to `https`.</li></ul> |
{: caption="Changes in the IBM Cloud {{site.data.keyword.codeengineshort}} CLI" caption-side="top"}
