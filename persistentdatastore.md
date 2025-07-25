---

copyright:
years: 2025, 2025
lastupdated: "2025-07-24"

keywords: code engine, persistent data store, pds, object storage, mount bucket, s3fs, mount cos, apps, jobs

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with persistent data stores
{: #persistent-data-store}

You can mount an {{site.data.keyword.cos_full_notm}}(COS) bucket to your {{site.data.keyword.codeenginefull}} application or job by using a **persistent data store**. This feature allows your workloads to access the contents of a COS bucket through the local file system by using standard file operations.

A persistent data store in {{site.data.keyword.codeengineshort}} is a reference to an existing data store that {{site.data.keyword.codeengineshort}} does not manage. Currently, {{site.data.keyword.cos_full_notm}} is the only supported data store type. By creating a reference to your COS bucket, you can mount it directly into your application or job container's file system.

## Before you begin
{: #pds-prereqs}

Before you can work with persistent data stores, ensure that the following prerequisites are met.

- You must have an [{{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision).
- You must have a bucket available in your {{site.data.keyword.cos_short}} instance.
- You must create a service credential for your {{site.data.keyword.cos_short}} instance with [**HMAC credentials**](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main) enabled. The HMAC credential requires at least the **Writer** service access role to read from and write to the bucket. If you only need read access, choose the **Content Reader** service access role instead.
- You must have a [{{site.data.keyword.codeengineshort}} project](/docs/codeengine?topic=codeengine-manage-project) and it must be selected as the current context.

## Step 1: Create an HMAC secret in {{site.data.keyword.codeengineshort}}
{: #pds-create-secret}

To securely access your COS bucket, {{site.data.keyword.codeengineshort}} requires the HMAC credentials that are associated with your {{site.data.keyword.cos_short}} instance. You store these credentials in a secret within your {{site.data.keyword.codeengineshort}} project.

To create a secret of format `hmac`, use the **`secret create`** command.

```bash
ibmcloud ce secret create --name my-hmac-secret --format hmac --secret-access-key-prompt --access-key-id-prompt
```
{: pre}

Provide the corresponding values from your COS service credential when prompted by the **`secret create`** command.

## Step 2: Create a persistent data store
{: #pds-create-datastore}

Now, create the persistent data store resource in {{site.data.keyword.codeengineshort}}. This resource acts as a reference to your COS bucket and links it with the HMAC secret that you created.

```bash
ibmcloud ce persistentdatastore create --name my-cos-bucket-pds --cos-bucket-name my-cos-bucket --cos-access-secret my-hmac-secret
```
{: pre}

- Replace `my-cos-bucket-pds` with a unique name for your data store.
- Replace `my-cos-bucket` with the exact name of your COS bucket.
- Replace `my-hmac-secret` with the name of the HMAC secret.

## Step 3: Mount the data store into a workload
{: #pds-mount-workload}

After you create the persistent data store, you can mount it when you create or update an application or job. Use the `--mount-data-store` option with the format `MOUNT_PATH=PDS_NAME`.

### Mounting into an application
{: #pds-mount-app}

The following command creates an application named `myapp` and mounts the `my-cos-bucket-pds` data store to the `/mnt/bucket` directory inside the application container.

```bash
ibmcloud ce application create --name myapp --image icr.io/codeengine/helloworld --mount-data-store /mnt/bucket=my-cos-bucket-pds:
```
{: pre}

### Mounting into a job
{: #pds-mount-job}

Similarly, this command creates a job named `myjob` and mounts the same data store to the `/mnt/bucket` directory.

```bash
ibmcloud ce job create --name myjob --image icr.io/codeengine/helloworld --mount-data-store /mnt/bucket=my-cos-bucket-pds:
```
{: pre}

### Mounting a subpath within the bucket
{: #pds-mount-subpath}

You can also mount a specific subpath within your COS bucket by appending the relative path to the mount definition using a colon (`:`). This is useful when you want to isolate access to a specific folder within the bucket.

For example, to mount only the `path/in/bucket` directory from the `my-cos-bucket-pds` data store into `/mnt/bucket`:

```bash
ibmcloud ce application create --name myapp --image icr.io/codeengine/helloworld --mount-data-store /mnt/bucket=my-cos-bucket-pds:path/in/bucket
```
{: pre}

Or for a job:

```bash
ibmcloud ce job create --name myjob --image icr.io/codeengine/helloworld --mount-data-store /mnt/bucket=my-cos-bucket-pds:path/in/bucket
```
{: pre}

> **Note:** The `path/in/bucket` must be a valid prefix in your COS bucket. Only the contents under that path will be accessible from the mounted directory.

## Step 4: Accessing files in the mounted data store
{: #pds-access-files}

Once your application or job is running, the code can interact with the mounted COS bucket as if it were a local directory. All standard file system operations are supported.

For example, inside your container, you can list files, read content, and write new files:

```bash
# List files in the bucket
ls -l /mnt/bucket

# Read a file from the bucket
cat /mnt/bucket/my-document.txt

# Write a new file to the bucket
echo "Hello from Code Engine" > /mnt/bucket/new-file.txt
```
{: pre}

## Limitations
{: #pds-limitations}

The mount is implemented using [`s3fs`](https://github.com/s3fs-fuse/s3fs-fuse){: external}, which provides a FUSE-based file system interface to S3-compatible storage. Be aware of the following limitations:

- **Performance:**
  - {{site.data.keyword.cos_short}} has high latency for the time-to-first-byte, making them slower than local file systems for operations that require immediate access.
  - Operations that modify files, such as random writes or appends, require rewriting the entire object in the backend, which can be slow and inefficient as there is no random write access.
  - Metadata operations, like listing directories, can have poor performance.
- **Consistency:**
  - {{site.data.keyword.cos_full_notm}} provides strong read-after-write consistency for new objects, but eventual consistency for object overwrites and deletes. This means that after an update or deletion, read operations might temporarily return stale data.
  - Changes made to the bucket from outside the mount (e.g., directly via the COS API or another client) are not immediately detected and might not be visible for some time.
- **File System Semantics:**
  - Standard POSIX file system features are not fully supported. Specifically, there are **no atomic renames** of files or directories and **no hard links**.
- **Concurrency:**
  - There is no coordination between multiple clients (e.g., multiple app instances) mounting the same bucket. Concurrent writes to the same file from different instances can lead to data loss or corruption.
- **Event Subscriptions:**
  - If you have configured an event subscription for your {{site.data.keyword.cos_short}} bucket, be aware that file create operations performed through the mount may generate multiple update events. This can result in your Code Engine app or job being triggered more than once for a single file operation, which may affect downstream processing or event-driven workflows.
Due to these limitations, this feature is not suitable for all workloads. It is best suited for workloads that primarily read large files, such as in deep learning or data analytics, where good throughput can be achieved. It is not recommended for workloads that require low latency, frequent small writes, or transactional file operations.

## Next steps
{: #pds-next-steps}

Now that you understand how to work with persistent data stores, explore more advanced topics:

- [Working with applications in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads)
- [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan)
- [Working with secrets](/docs/codeengine?topic=codeengine-secret)
- [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer)
- [{{site.data.keyword.cos_full_notm}} Documentation](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)
