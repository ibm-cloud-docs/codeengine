---

copyright:
  years: 2022, 2023
lastupdated: "2023-12-07"

keywords: domain mapping, custom domain, applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Implementing applications with gRPC
{: #app-grpc}

With {{site.data.keyword.codeengineshort}}, you can configure your applications to run as gRPC servers to handle client calls by taking advantage of gRPC features. 
{: shortdesc}

gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers. Provides for efficient binary serialization, bidirectional streaming, load balancing for client and servers, tracing, health checking, and authentication. For more information, see [gRPC documentation](https://grpc.io/docs/guides/index.html){: external}.

## Benefits of using gRPC
{: #app-grpc-benefits}

gRPC provides several advantages in facilitating communications between clients and servers. A fundamental aspect of gRPC is to define a clear interface that encapsulates all the methods and parameters available for a remote invocation. On the server side, this interface is implemented to handle and respond to client requests effectively.

This approach of working with gRPC with your {{site.data.keyword.codeengineshort}} applications offers benefits.

* Interoperability -  gRPC clients and servers can run and communicate with each other in various environments. For example, you can define your servers with the Go language, while your clients are defined in Java.

* Serialization -  gRPC uses protocol buffers for message serialization, which is more efficient in terms of size and speed, than using JSON in HTTP APIs.

* Streaming -  gRPC supports bidirectional streaming so that clients and servers send and receive messages simultaneously over a single connection.

* Error detection -  gRPC enforces a strongly typed contract between the client and server through the protocol buffers (``.proto`` files). This contract makes sure that the client and server agree on interfaces and data structure, which provides for better code generation, validation, and error handling.

* Security -  gRPC supports various authentication and encryption methods, including mutual TLS, which provides secure communication between the client and server.

 
## Configuring {{site.data.keyword.codeengineshort}} applications to use gRPC
{: #app-grpc-config-cli}

gRPC is supported for {{site.data.keyword.codeengineshort}} applications at a project level, which means that your {{site.data.keyword.codeengineshort}} gRPC server application can only serve traffic to clients that run in the same project.

You must use the {{site.data.keyword.codeengineshort}} CLI to configure a {{site.data.keyword.codeengineshort}} gRPC application.

Before you begin

From {{site.data.keyword.codeengineshort}}:
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create and deploy an application with the [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. To indicate that this application supports gRPC, which uses HTTP/2 as a transport mode, you must specify the `--port` option with the format `[NAME:]PORT`; for example, `--port h2c:8080`. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. By default, {{site.data.keyword.codeengineshort}} assumes that apps listen for incoming connections on port `8080`.

    In the following example, use `myapp-grpcserver` as the name of the server application and specify `icr.io/codeengine/grpc-server` as the image to reference. 

    ```txt
    ibmcloud ce application create --name myapp-grpcserver --port h2c:8080 --min-scale 1 --image icr.io/codeengine/grpc-server
    ```
    {: pre}


2. Run the **`application get`** command to display the details about the app. 

    ```txt
    ibmcloud ce application get --name myapp-grpcserver
    ```
    {: pre}

    Example output 

    ```txt
    [...]
    OK

    Name:               myapp-grpcserver
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    [...]
    Port:               h2c:8080
    [...]
    ```
    {: screen}

Now that your server app is created and deployed to use gRPC, you must deploy a client application within the same project to access the server with gRPC. For more information about {{site.data.keyword.codeengineshort}} sample code for deploying a gRPC server and client application, see [{{site.data.keyword.codeengineshort}} `grpc` sample](https://github.com/IBM/CodeEngine/tree/main/grpc){: external}. 


{{site.data.keyword.codeengineshort}} sample images that are built from the [{{site.data.keyword.codeenginefull_notm}} samples repository on GitHub](https://github.com/IBM/CodeEngine){: external} are available in {{site.data.keyword.registrylong}} in the public `icr.io/codeengine` namespace.
{: note}




