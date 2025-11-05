---

copyright:
  years: 2025

lastupdated: "2025-11-05"


keywords: change log, version history, vsi image, serverless fleets

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

<!-- The content in this topic is auto-generated except for reuse-snippets indicated with {[ ]}. -->

# Worker Image Changelog v1.0
{: #fleets-worker-changelog-v1_0}

View information of version changes for major, minor, and patch updates that are available for your {{site.data.keyword.codeengineshort}} fleet workers that run this version. When a new version of the worker image becomes available, fleet workers will automatically use the latest available version of this image. 



## Version v1.0
{: #fleets-worker-changelog-contents-v1_0}



### Worker image `v1.0.55`, released 03 November 2025
{: #fleets-worker-boms-v1_0_55}

The following table shows the components included in the {{site.data.keyword.codeengineshort}} fleet worker image v1.0.55.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|UBUNTU_24_04| Kernel: 6.8.0-1040<br/>podman: 4.9.3<br/>s3fs: 1.93|Resolves the following CVEs: <br/>N/A|
| Nvidia CUDA | Driver: 580.95.05<br/> Toolkit: 12.6.3<br/> NVIDIA Fabric Manager: 580.95.05||

{: caption="Worker image v1.0.55" caption-side="bottom"}
{: #fleets-worker-boms-v1_0_55-component-table}


### Worker image `v1.0.49`, released 26 October 2025
{: #fleets-worker-boms-v1_0_49}

The following table shows the components included in the {{site.data.keyword.codeengineshort}} fleet worker image v1.0.49.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|UBUNTU_24_04| Kernel: 6.8.0-1039<br/>podman: 4.9.3<br/>s3fs: 1.93|Resolves the following CVEs: <br/>[CVE-2025-40778](https://nvd.nist.gov/vuln/detail/CVE-2025-40778){: external}, [CVE-2025-40780](https://nvd.nist.gov/vuln/detail/CVE-2025-40780){: external}, [CVE-2025-8677](https://nvd.nist.gov/vuln/detail/CVE-2025-8677){: external}|
| Nvidia CUDA | Driver: 580.95.05<br/> Toolkit: 12.6.3<br/> NVIDIA Fabric Manager: 580.95.05||

{: caption="Worker image v1.0.49" caption-side="bottom"}
{: #fleets-worker-boms-v1_0_49-component-table}


### Worker image `v1.0.42`, released 20 October 2025
{: #fleets-worker-boms-v1_0_42}

The following table shows the components included in the {{site.data.keyword.codeengineshort}} fleet worker image v1.0.42.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|UBUNTU_24_04| Kernel: 6.8.0-1038<br/>podman: 4.9.3<br/>s3fs: 1.93|Resolves the following CVEs: <br/>[CVE-2024-10963](https://nvd.nist.gov/vuln/detail/CVE-2024-10963){: external}, [CVE-2025-41244](https://nvd.nist.gov/vuln/detail/CVE-2025-41244){: external}, [CVE-2025-9230](https://nvd.nist.gov/vuln/detail/CVE-2025-9230){: external}|
| Nvidia CUDA | Driver: 580.95.05<br/> Toolkit: 12.6.3<br/> NVIDIA Fabric Manager: 580.95.05||

{: caption="Worker image v1.0.42" caption-side="bottom"}
{: #fleets-worker-boms-v1_0_42-component-table}


### Worker image `v1.0.15`, released 26 September 2025
{: #fleets-worker-boms-v1_0_15}

The following table shows the components included in the {{site.data.keyword.codeengineshort}} fleet worker image v1.0.15.
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|UBUNTU_24_04| Kernel: 6.8.0-1036<br/>podman: 4.9.3<br/>s3fs: 1.93|Resolves the following CVEs: <br/>[CVE-2022-49043](https://nvd.nist.gov/vuln/detail/CVE-2022-49043){: external}, [CVE-2022-4968](https://nvd.nist.gov/vuln/detail/CVE-2022-4968){: external}, [CVE-2023-27043](https://nvd.nist.gov/vuln/detail/CVE-2023-27043){: external}, [CVE-2024-10224](https://nvd.nist.gov/vuln/detail/CVE-2024-10224){: external}, [CVE-2024-11003](https://nvd.nist.gov/vuln/detail/CVE-2024-11003){: external}, [CVE-2024-11053](https://nvd.nist.gov/vuln/detail/CVE-2024-11053){: external}, [CVE-2024-11187](https://nvd.nist.gov/vuln/detail/CVE-2024-11187){: external}, [CVE-2024-11584](https://nvd.nist.gov/vuln/detail/CVE-2024-11584){: external}, [CVE-2024-12084](https://nvd.nist.gov/vuln/detail/CVE-2024-12084){: external}, [CVE-2024-12085](https://nvd.nist.gov/vuln/detail/CVE-2024-12085){: external}, [CVE-2024-12086](https://nvd.nist.gov/vuln/detail/CVE-2024-12086){: external}, [CVE-2024-12087](https://nvd.nist.gov/vuln/detail/CVE-2024-12087){: external}, [CVE-2024-12088](https://nvd.nist.gov/vuln/detail/CVE-2024-12088){: external}, [CVE-2024-12133](https://nvd.nist.gov/vuln/detail/CVE-2024-12133){: external}, [CVE-2024-12243](https://nvd.nist.gov/vuln/detail/CVE-2024-12243){: external}, [CVE-2024-12254](https://nvd.nist.gov/vuln/detail/CVE-2024-12254){: external}, [CVE-2024-12705](https://nvd.nist.gov/vuln/detail/CVE-2024-12705){: external}, [CVE-2024-12718](https://nvd.nist.gov/vuln/detail/CVE-2024-12718){: external}, [CVE-2024-12747](https://nvd.nist.gov/vuln/detail/CVE-2024-12747){: external}, [CVE-2024-13176](https://nvd.nist.gov/vuln/detail/CVE-2024-13176){: external}, [CVE-2024-20696](https://nvd.nist.gov/vuln/detail/CVE-2024-20696){: external}, [CVE-2024-23337](https://nvd.nist.gov/vuln/detail/CVE-2024-23337){: external}, [CVE-2024-25260](https://nvd.nist.gov/vuln/detail/CVE-2024-25260){: external}, [CVE-2024-26458](https://nvd.nist.gov/vuln/detail/CVE-2024-26458){: external}, [CVE-2024-26461](https://nvd.nist.gov/vuln/detail/CVE-2024-26461){: external}, [CVE-2024-26462](https://nvd.nist.gov/vuln/detail/CVE-2024-26462){: external}, [CVE-2024-34459](https://nvd.nist.gov/vuln/detail/CVE-2024-34459){: external}, [CVE-2024-3596](https://nvd.nist.gov/vuln/detail/CVE-2024-3596){: external}, [CVE-2024-37891](https://nvd.nist.gov/vuln/detail/CVE-2024-37891){: external}, [CVE-2024-43802](https://nvd.nist.gov/vuln/detail/CVE-2024-43802){: external}, [CVE-2024-45490](https://nvd.nist.gov/vuln/detail/CVE-2024-45490){: external}, [CVE-2024-45491](https://nvd.nist.gov/vuln/detail/CVE-2024-45491){: external}, [CVE-2024-45492](https://nvd.nist.gov/vuln/detail/CVE-2024-45492){: external}, [CVE-2024-45774](https://nvd.nist.gov/vuln/detail/CVE-2024-45774){: external}, [CVE-2024-45775](https://nvd.nist.gov/vuln/detail/CVE-2024-45775){: external}, [CVE-2024-45776](https://nvd.nist.gov/vuln/detail/CVE-2024-45776){: external}, [CVE-2024-45777](https://nvd.nist.gov/vuln/detail/CVE-2024-45777){: external}, [CVE-2024-45778](https://nvd.nist.gov/vuln/detail/CVE-2024-45778){: external}, [CVE-2024-45779](https://nvd.nist.gov/vuln/detail/CVE-2024-45779){: external}, [CVE-2024-45780](https://nvd.nist.gov/vuln/detail/CVE-2024-45780){: external}, [CVE-2024-45781](https://nvd.nist.gov/vuln/detail/CVE-2024-45781){: external}, [CVE-2024-45782](https://nvd.nist.gov/vuln/detail/CVE-2024-45782){: external}, [CVE-2024-45783](https://nvd.nist.gov/vuln/detail/CVE-2024-45783){: external}, [CVE-2024-47081](https://nvd.nist.gov/vuln/detail/CVE-2024-47081){: external}, [CVE-2024-47606](https://nvd.nist.gov/vuln/detail/CVE-2024-47606){: external}, [CVE-2024-47814](https://nvd.nist.gov/vuln/detail/CVE-2024-47814){: external}, [CVE-2024-48957](https://nvd.nist.gov/vuln/detail/CVE-2024-48957){: external}, [CVE-2024-48958](https://nvd.nist.gov/vuln/detail/CVE-2024-48958){: external}, [CVE-2024-48990](https://nvd.nist.gov/vuln/detail/CVE-2024-48990){: external}, [CVE-2024-48991](https://nvd.nist.gov/vuln/detail/CVE-2024-48991){: external}, [CVE-2024-48992](https://nvd.nist.gov/vuln/detail/CVE-2024-48992){: external}, [CVE-2024-50349](https://nvd.nist.gov/vuln/detail/CVE-2024-50349){: external}, [CVE-2024-50602](https://nvd.nist.gov/vuln/detail/CVE-2024-50602){: external}, [CVE-2024-52006](https://nvd.nist.gov/vuln/detail/CVE-2024-52006){: external}, [CVE-2024-52533](https://nvd.nist.gov/vuln/detail/CVE-2024-52533){: external}, [CVE-2024-53427](https://nvd.nist.gov/vuln/detail/CVE-2024-53427){: external}, [CVE-2024-55549](https://nvd.nist.gov/vuln/detail/CVE-2024-55549){: external}, [CVE-2024-56171](https://nvd.nist.gov/vuln/detail/CVE-2024-56171){: external}, [CVE-2024-56201](https://nvd.nist.gov/vuln/detail/CVE-2024-56201){: external}, [CVE-2024-56326](https://nvd.nist.gov/vuln/detail/CVE-2024-56326){: external}, [CVE-2024-56406](https://nvd.nist.gov/vuln/detail/CVE-2024-56406){: external}, [CVE-2024-5742](https://nvd.nist.gov/vuln/detail/CVE-2024-5742){: external}, [CVE-2024-6174](https://nvd.nist.gov/vuln/detail/CVE-2024-6174){: external}, [CVE-2024-6232](https://nvd.nist.gov/vuln/detail/CVE-2024-6232){: external}, [CVE-2024-6345](https://nvd.nist.gov/vuln/detail/CVE-2024-6345){: external}, [CVE-2024-6923](https://nvd.nist.gov/vuln/detail/CVE-2024-6923){: external}, [CVE-2024-7592](https://nvd.nist.gov/vuln/detail/CVE-2024-7592){: external}, [CVE-2024-8088](https://nvd.nist.gov/vuln/detail/CVE-2024-8088){: external}, [CVE-2024-8096](https://nvd.nist.gov/vuln/detail/CVE-2024-8096){: external}, [CVE-2024-8176](https://nvd.nist.gov/vuln/detail/CVE-2024-8176){: external}, [CVE-2024-9143](https://nvd.nist.gov/vuln/detail/CVE-2024-9143){: external}, [CVE-2024-9287](https://nvd.nist.gov/vuln/detail/CVE-2024-9287){: external}, [CVE-2024-9681](https://nvd.nist.gov/vuln/detail/CVE-2024-9681){: external}, [CVE-2025-0622](https://nvd.nist.gov/vuln/detail/CVE-2025-0622){: external}, [CVE-2025-0624](https://nvd.nist.gov/vuln/detail/CVE-2025-0624){: external}, [CVE-2025-0677](https://nvd.nist.gov/vuln/detail/CVE-2025-0677){: external}, [CVE-2025-0678](https://nvd.nist.gov/vuln/detail/CVE-2025-0678){: external}, [CVE-2025-0684](https://nvd.nist.gov/vuln/detail/CVE-2025-0684){: external}, [CVE-2025-0685](https://nvd.nist.gov/vuln/detail/CVE-2025-0685){: external}, [CVE-2025-0686](https://nvd.nist.gov/vuln/detail/CVE-2025-0686){: external}, [CVE-2025-0689](https://nvd.nist.gov/vuln/detail/CVE-2025-0689){: external}, [CVE-2025-0690](https://nvd.nist.gov/vuln/detail/CVE-2025-0690){: external}, [CVE-2025-0938](https://nvd.nist.gov/vuln/detail/CVE-2025-0938){: external}, [CVE-2025-1118](https://nvd.nist.gov/vuln/detail/CVE-2025-1118){: external}, [CVE-2025-1125](https://nvd.nist.gov/vuln/detail/CVE-2025-1125){: external}, [CVE-2025-1215](https://nvd.nist.gov/vuln/detail/CVE-2025-1215){: external}, [CVE-2025-1365](https://nvd.nist.gov/vuln/detail/CVE-2025-1365){: external}, [CVE-2025-1371](https://nvd.nist.gov/vuln/detail/CVE-2025-1371){: external}, [CVE-2025-1372](https://nvd.nist.gov/vuln/detail/CVE-2025-1372){: external}, [CVE-2025-1377](https://nvd.nist.gov/vuln/detail/CVE-2025-1377){: external}, [CVE-2025-1390](https://nvd.nist.gov/vuln/detail/CVE-2025-1390){: external}, [CVE-2025-1632](https://nvd.nist.gov/vuln/detail/CVE-2025-1632){: external}, [CVE-2025-1795](https://nvd.nist.gov/vuln/detail/CVE-2025-1795){: external}, [CVE-2025-22134](https://nvd.nist.gov/vuln/detail/CVE-2025-22134){: external}, [CVE-2025-22247](https://nvd.nist.gov/vuln/detail/CVE-2025-22247){: external}, [CVE-2025-24014](https://nvd.nist.gov/vuln/detail/CVE-2025-24014){: external}, [CVE-2025-24528](https://nvd.nist.gov/vuln/detail/CVE-2025-24528){: external}, [CVE-2025-24855](https://nvd.nist.gov/vuln/detail/CVE-2025-24855){: external}, [CVE-2025-24928](https://nvd.nist.gov/vuln/detail/CVE-2025-24928){: external}, [CVE-2025-25724](https://nvd.nist.gov/vuln/detail/CVE-2025-25724){: external}, [CVE-2025-26465](https://nvd.nist.gov/vuln/detail/CVE-2025-26465){: external}, [CVE-2025-26466](https://nvd.nist.gov/vuln/detail/CVE-2025-26466){: external}, [CVE-2025-26603](https://nvd.nist.gov/vuln/detail/CVE-2025-26603){: external}, [CVE-2025-27113](https://nvd.nist.gov/vuln/detail/CVE-2025-27113){: external}, [CVE-2025-27516](https://nvd.nist.gov/vuln/detail/CVE-2025-27516){: external}, [CVE-2025-27613](https://nvd.nist.gov/vuln/detail/CVE-2025-27613){: external}, [CVE-2025-27614](https://nvd.nist.gov/vuln/detail/CVE-2025-27614){: external}, [CVE-2025-29087](https://nvd.nist.gov/vuln/detail/CVE-2025-29087){: external}, [CVE-2025-29088](https://nvd.nist.gov/vuln/detail/CVE-2025-29088){: external}, [CVE-2025-30258](https://nvd.nist.gov/vuln/detail/CVE-2025-30258){: external}, [CVE-2025-31115](https://nvd.nist.gov/vuln/detail/CVE-2025-31115){: external}, [CVE-2025-32414](https://nvd.nist.gov/vuln/detail/CVE-2025-32414){: external}, [CVE-2025-32415](https://nvd.nist.gov/vuln/detail/CVE-2025-32415){: external}, [CVE-2025-32462](https://nvd.nist.gov/vuln/detail/CVE-2025-32462){: external}, [CVE-2025-32463](https://nvd.nist.gov/vuln/detail/CVE-2025-32463){: external}, [CVE-2025-32728](https://nvd.nist.gov/vuln/detail/CVE-2025-32728){: external}, [CVE-2025-3277](https://nvd.nist.gov/vuln/detail/CVE-2025-3277){: external}, [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/CVE-2025-32988){: external}, [CVE-2025-32989](https://nvd.nist.gov/vuln/detail/CVE-2025-32989){: external}, [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/CVE-2025-32990){: external}, [CVE-2025-3576](https://nvd.nist.gov/vuln/detail/CVE-2025-3576){: external}, [CVE-2025-40909](https://nvd.nist.gov/vuln/detail/CVE-2025-40909){: external}, [CVE-2025-4138](https://nvd.nist.gov/vuln/detail/CVE-2025-4138){: external}, [CVE-2025-4330](https://nvd.nist.gov/vuln/detail/CVE-2025-4330){: external}, [CVE-2025-4373](https://nvd.nist.gov/vuln/detail/CVE-2025-4373){: external}, [CVE-2025-4435](https://nvd.nist.gov/vuln/detail/CVE-2025-4435){: external}, [CVE-2025-4516](https://nvd.nist.gov/vuln/detail/CVE-2025-4516){: external}, [CVE-2025-4517](https://nvd.nist.gov/vuln/detail/CVE-2025-4517){: external}, [CVE-2025-4598](https://nvd.nist.gov/vuln/detail/CVE-2025-4598){: external}, [CVE-2025-46835](https://nvd.nist.gov/vuln/detail/CVE-2025-46835){: external}, [CVE-2025-47268](https://nvd.nist.gov/vuln/detail/CVE-2025-47268){: external}, [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/CVE-2025-47273){: external}, [CVE-2025-48060](https://nvd.nist.gov/vuln/detail/CVE-2025-48060){: external}, [CVE-2025-48384](https://nvd.nist.gov/vuln/detail/CVE-2025-48384){: external}, [CVE-2025-48385](https://nvd.nist.gov/vuln/detail/CVE-2025-48385){: external}, [CVE-2025-48386](https://nvd.nist.gov/vuln/detail/CVE-2025-48386){: external}, [CVE-2025-4877](https://nvd.nist.gov/vuln/detail/CVE-2025-4877){: external}, [CVE-2025-4878](https://nvd.nist.gov/vuln/detail/CVE-2025-4878){: external}, [CVE-2025-48964](https://nvd.nist.gov/vuln/detail/CVE-2025-48964){: external}, [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/CVE-2025-49794){: external}, [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/CVE-2025-49796){: external}, [CVE-2025-50181](https://nvd.nist.gov/vuln/detail/CVE-2025-50181){: external}, [CVE-2025-5054](https://nvd.nist.gov/vuln/detail/CVE-2025-5054){: external}, [CVE-2025-5318](https://nvd.nist.gov/vuln/detail/CVE-2025-5318){: external}, [CVE-2025-5351](https://nvd.nist.gov/vuln/detail/CVE-2025-5351){: external}, [CVE-2025-5372](https://nvd.nist.gov/vuln/detail/CVE-2025-5372){: external}, [CVE-2025-53905](https://nvd.nist.gov/vuln/detail/CVE-2025-53905){: external}, [CVE-2025-53906](https://nvd.nist.gov/vuln/detail/CVE-2025-53906){: external}, [CVE-2025-5467](https://nvd.nist.gov/vuln/detail/CVE-2025-5467){: external}, [CVE-2025-5914](https://nvd.nist.gov/vuln/detail/CVE-2025-5914){: external}, [CVE-2025-5915](https://nvd.nist.gov/vuln/detail/CVE-2025-5915){: external}, [CVE-2025-5916](https://nvd.nist.gov/vuln/detail/CVE-2025-5916){: external}, [CVE-2025-5917](https://nvd.nist.gov/vuln/detail/CVE-2025-5917){: external}, [CVE-2025-5987](https://nvd.nist.gov/vuln/detail/CVE-2025-5987){: external}, [CVE-2025-6019](https://nvd.nist.gov/vuln/detail/CVE-2025-6019){: external}, [CVE-2025-6020](https://nvd.nist.gov/vuln/detail/CVE-2025-6020){: external}, [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/CVE-2025-6021){: external}, [CVE-2025-6069](https://nvd.nist.gov/vuln/detail/CVE-2025-6069){: external}, [CVE-2025-6170](https://nvd.nist.gov/vuln/detail/CVE-2025-6170){: external}, [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/CVE-2025-6395){: external}, [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/CVE-2025-6965){: external}, [CVE-2025-7709](https://nvd.nist.gov/vuln/detail/CVE-2025-7709){: external}, [CVE-2025-8067](https://nvd.nist.gov/vuln/detail/CVE-2025-8067){: external}, [CVE-2025-8194](https://nvd.nist.gov/vuln/detail/CVE-2025-8194){: external}, [CVE-2025-9714](https://nvd.nist.gov/vuln/detail/CVE-2025-9714){: external}|
| Nvidia CUDA | Driver: 580.82.07<br/> Toolkit: 12.6.3||

{: caption="Worker image v1.0.15" caption-side="bottom"}
{: #fleets-worker-boms-v1_0_15-component-table}



<!-- Sample formatting of a proper changelog entry below - keep for reference 
### Worker image `v1.0.56`, released 30 September 2025
{: #fleets-worker-boms-v1_0_56}

The following table shows the components included in the {[kn-service]} fleet worker image `v1.0.56`. 
{: shortdesc}

| Component | Version | Description |
| ---- | ---- | ---- |
|UBUNTU_24_04| Kernel: 6.8.0-1033<br/>podman: 4.9.3<br/>s3fs: 1.93|Resolves the following CVEs: [CVE-2024-11584](https://nvd.nist.gov/vuln/detail/CVE-2024-11584){: external}, [CVE-2024-6174](https://nvd.nist.gov/vuln/detail/CVE-2024-6174){: external}, [CVE-2025-37797](https://nvd.nist.gov/vuln/detail/CVE-2025-37797){: external}, [CVE-2025-38083](https://nvd.nist.gov/vuln/detail/CVE-2025-38083){: external}, [CVE-2025-40909](https://nvd.nist.gov/vuln/detail/CVE-2025-40909){: external}, and [CVE-2025-6965](https://nvd.nist.gov/vuln/detail/CVE-2025-6965){: external}.|
| Nvidia CUDA | Driver: 580.65.06<br/> Toolkit: 12.6.3||

{: caption="Worker image v1.0.56" caption-side="bottom"}
{: #fleets-worker-boms-v1_0_56-component-table}
-->
