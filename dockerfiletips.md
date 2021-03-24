---

copyright:
  years: 2021
lastupdated: "2021-03-24"

keywords: Dockerfile for code engine, build Dockerfile in code engine, container images in code engine, tools in Dockerfile

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Writing a Dockerfile for {{site.data.keyword.codeengineshort}}
{: #dockerfile}

Before you build your code into a container image, learn some of the basics of how a Docker build works within {{site.data.keyword.codeengineshort}}. Then, look at some best practices for your Dockerfile to reach these goals.
{: shortdesc}

When you create your build configuration, you decide which of the two available strategies to use.

1. Cloud Native Buildpacks inspect your source code and detect which runtime environment that your code is based on and how a container image is built from your sources. It is supported for several programming environments. You can find the supported list under [Choose a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

2. A Docker build creates a container based on how you describe it in a Dockerfile. The Dockerfile is then committed along with your source code to create the container.

While you can use either strategy for your build, you might choose Dockerfile, if, for example,

- Your programming environment is not supported by Buildpacks.
- Your project build must install additional packages in the container.

## Dockerfile basics
{: #dockerfile-basics}

A Dockerfile describes how a container is built. Within your Dockerfile, you choose a base image that includes the necessary tools that you need during your build and runtime. You can copy files from a build context into the image, run commands, define the runtime behavior such as environment variables, exposed ports, and set the entrypoint – the command that is invoked when the container is started. For more information about how Dockerfile instructions can be specified, see [Dockerfile reference](https://docs.docker.com/engine/reference/builder/){: external}.

In a {{site.data.keyword.codeengineshort}} build, you define a source that points to a Git repository. The context that is available to the Docker build is, by default, the root directory of your Git repository. For example, if you have a directory that is named `src` in your repository, then you can use the `COPY` statement in the Dockerfile to copy this directory into your image. For example,

```Dockerfile
COPY src /app/src
```
{: codeblock}

To copy the entire Git repository, specify the following `COPY` statement,

```Dockerfile
COPY . /app/src
```
{: codeblock}

If you copy the entire Git repository, but want to exclude some files, for example the `README.md` of the repository, then you can add a [`.dockerignore` file](https://docs.docker.com/engine/reference/builder/#dockerignore-file){: external}. Use the same file to also ignore the files and directories that you specify in your [.gitignore file](https://git-scm.com/docs/gitignore){: external}. This ensures that a build which you run locally has the same set of files available as the build running in Code Engine.
{: tip}

Always copy your application files into a subdirectory of the root (`/`) rather than into the root directly to avoid conflicts with operating system files. When you name your application directory, do not use one that is reserved by Unix-based operating systems, Kubernetes or {{{site.data.keyword.codeengineshort}}} builds, such as `/bin`, `/dev`, `/etc`, `/lib`, `/proc`, `/run`, `/sys`, `/usr`, `/var`, or `/workspace`. Naming your application directory `/app` is a best practice.
{: note}

If your source code repository contains the sources for different applications that are organized in directories, similar to the [{{site.data.keyword.codeengineshort}} samples repository](https://github.com/IBM/CodeEngine){: external}, then you can use a subdirectory as your context. In the [`ibmcloud ce build create`](/docs/codeengine?topic=codeengine-cli#cli-build-create) command, specify subdirectories by using the `--context-dir` option.

If your Dockerfile is not in the context directory, then you can point to it by using the `--dockerfile` argument.

To try out a Docker build on your local system before you build it in {{site.data.keyword.codeengineshort}}, you can use [Docker Desktop](https://www.docker.com/products/docker-desktop){: external}.

Let's now look at specific aspects of a Dockerfile that can help you to improve your Dockerfile. These examples focus on reducing the image size, improving the interoperability with {{site.data.keyword.codeengineshort}} applications, and to run containers as a non-root user.

## Reducing the size of a container image
{: #reduce-container}

Reducing the size of a container image brings a value in multiple aspects.

- Less space is needed to store the image in the container registry. You save quota for other images and save money.
- In some cases, the build run needs less time to complete because a smaller image can be transferred faster to the container registry than a much larger one. You again save money.
- The application or job that uses the image starts faster because the time that is needed to pull the image is shorter. As the resources that are needed to run your application or job are reserved while the image is pulled, you again save money. A fast startup time is especially relevant for applications in {{site.data.keyword.codeengineshort}} because it guarantees an acceptable response time for the requests of your users, even if the application is scaled down to zero.

Let's look at some best practices to reduce the size of your build.

### Combine several commands in a single `RUN` statement to reduce image size
{: #combine-commands}

In this example, you must install software in the container image, for example, Node.js. Use the base images for Node.js to build a Node.js application. 

To manually install Node.js, you can use the following Dockerfile example, 

```Dockerfile
FROM ubuntu

RUN apt update
RUN apt upgrade -y
RUN apt install -y nodejs
RUN apt clean
RUN rm -rf /var/lib/apt/lists/\*
```
{: codeblock}

In this example, several `RUN` statements are used to update, upgrade, install Node.js, clean, and remove the cache of files. While this sequence of statements is correct, the use of multiple `RUN` statements is not the best way to implement it. When a Dockerfile is processed, each statement in the Dockerfile creates a layer. Each layer contains the files that were created or updated and also information about what was deleted. A container image is the collection of all the layers. If a file is added in one statement and deleted in a second one, then the resulting image still contains the file in the layer for the first statement and then marks it as deleted in the second layer.

To save disk space, specify a single `RUN` statement to create a single layer for this set of commands,

```Dockerfile
FROM ubuntu

RUN apt update && apt upgrade -y && apt install -y nodejs && apt clean && rm -rf /var/lib/apt/lists/\*
```
{: codeblock}

To maintain a readable Dockerfile with one line per command, add line breaks to your code,

```Dockerfile
FROM ubuntu

RUN \
  apt update && \
  apt upgrade -y && \
  apt install -y nodejs && \
  apt clean && \
  rm -rf /var/lib/apt/lists/\*
```
{: codeblock}

By using this type of statement, you can reduce the container image size from about 174 MB to approximately 147 MB. Note that your example sizes might differ as the Ubuntu base image and the Node.js package can change.

This type of best practice applies not only to package installations, but also to similar tasks. In the next example, the download and extraction of a software package, again Node.js, can look similar to the following example,

```Dockerfile
FROM ubuntu

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl
RUN curl https://nodejs.org/dist/v12.19.0/node-v12.19.0-linux-x64.tar.gz -o /tmp/nodejs.tar.gz
RUN mkdir /opt/node
RUN tar -xzf /tmp/nodejs.tar.gz -C /opt/node --strip 1
RUN rm /tmp/nodejs.tar.gz
RUN apt remove -y curl
RUN apt clean
RUN rm -rf /var/lib/apt/lists/\*
```
{: codeblock}

The `rm` command removes the downloaded `nodejs` package, but the multiple `RUN` statements again create separate layers. In addition, to download the `nodejs` package, the `curl` package is temporarily installed. While the curl package itself is later removed, its dependencies that were implicitly installed are still there. A better Dockerfile looks like the following example,

```Dockerfile
FROM ubuntu

RUN \
  apt update && \
  apt upgrade -y && \
  apt install -y curl && \
  curl https://nodejs.org/dist/v12.19.0/node-v12.19.0-linux-x64.tar.gz -o /tmp/nodejs.tar.gz && \
  mkdir /opt/node && \
  tar -xzf /tmp/nodejs.tar.gz -C /opt/node --strip 1 && \
  rm /tmp/nodejs.tar.gz && \
  apt remove -y curl && \
  apt auto-remove -y && \
  apt clean && \
  rm -rf /var/lib/apt/lists/\*
```
{: codeblock}

The related commands are combined into a single `RUN` statement and the `apt auto-remove` command is added to remove the dependencies. This example reduces the image size from about 222 MB to approximately 162 MB.

### Use a tiny base image
{: #small-base-image}

The previous examples use Ubuntu as a base image. While this image contains many useful utilities, the more utilities that are in a base image, then the larger its size is. Additionally, by including more utilities, you increase the chance that you might encounter a security vulnerability, requiring you to rebuild your image. To avoid both of these issues, use a smaller base image. For example, 

- [Alpine](https://hub.docker.com/_/alpine) is an official Docker image with small size. For programming environments like Java or Node.js, you often find tags that are based on Alpine.

- [Distroless images from Google Container Tools](https://github.com/GoogleContainerTools/distroless) contain no operating system tools at all but the necessary runtime environment for different languages like Java and Node.js.

Compare these base images by building a container image that runs a Node.js program in a program.js file. For Ubuntu, the Dockerfile looks similar the following example, 

```Dockerfile
FROM ubuntu

RUN \
  apt update && \
  apt upgrade -y && \
  apt install -y nodejs && \
  apt clean && \
  rm -rf /var/lib/apt/lists/\*

ADD program.js /app/program.js

WORKDIR /app

ENTRYPOINT ["node", "program.js"]
```
{: codeblock}

For Alpine, the image is taken directly from Node.js,

```Dockerfile
FROM node:12-alpine

ADD program.js /app/program.js

WORKDIR /app

ENTRYPOINT ["node", "program.js"]
```
{: codeblock}

For distroless, use the following example,

```Dockerfile
FROM gcr.io/distroless/nodejs:12

ADD program.js /app/program.js

WORKDIR /app

CMD ["program.js"]
```
{: codeblock}

While the Ubuntu-based image is 147 MB, the image that is based on Alpine is 90 MB and the image that is based on distroless is 94 MB.

### Do not include sources and build tools to reduce image size
{: #dont-include-source}

In the previous Node.js based examples, a single source file is added to the container image. This example can use a single source file because no compilation was necessary. However, if a compilation is necessary, then use the necessary tools for the build only, but do not include them in the resulting image. For example, specify a Java application that uses Maven as example. A poorly coded Dockerfile looks similar to the following example, 

```Dockerfile
FROM maven:3-jdk-11-openj9

WORKDIR /app
COPY . /app

RUN mvn package

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/target/java-application-1.0-SNAPSHOT-fat.jar"]
```
{: codeblock}

The resulting container image contains all of the source code and all of the intermediate files from Maven (such as its artifact cache, class files that are later packaged into a JAR file) as well as the Maven build tool. In addition, the Java Development Kit (JDK) is also included when a much smaller Java Runtime Environment (JRE) is required at run time. As a result, the image size is 466 MB.

To make the image smaller, use a feature called multi-stage builds. Each stage in a Docker build has its own base image and can run commands in its stage. At the end, a final image is built that copies in artifacts from previous stages. To build a container image from source code, a common pattern is to have two stages:

1. The builder stage that uses a base image that contains all of the necessary tools to compile the source code into the binary for the runtime.
2. The runtime stage that uses a base image with the runtime environment that is necessary to run the binary. The binary from the builder stage is copied into this stage.

For the Maven project, the result looks similar to the following example,

```Dockerfile
FROM maven:3-jdk-11-openj9 AS builder

WORKDIR /app
COPY . /app

RUN mvn package

FROM adoptopenjdk:11-jre-openj9

WORKDIR /app
COPY --from=builder /app/target/java-application-1.0-SNAPSHOT-fat.jar /app/java-application.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/java-application.jar"]
```
{: codeblock}

In this example, the builder stage uses the Maven base image to build the JAR file of the application. The runtime stage uses the smaller JRE base image. By using the `COPY --from=STAGE_NAME` command, the JAR file is copied from the builder stage into the runtime stage. The resulting image has a size of 242 MB, saving around 48%.

This pattern can also be used for other programming languages where a compilation needs to be performed.

- Node applications that require a build, for example an Angular or React build. Here, the builder and runtime base image might end up being the same (both node), but not all build time artifacts and sources need to be copied into the runtime image.
- Any programming language that compiles source code into a native executable that runs without a runtime environment, for example Go or Rust.

For those languages that produce a native executable and do not need a runtime environment at all, use another Docker capability for the runtime stage: scratch. Scratch can be used as a base in the `FROM` command, but is not a final container image. Instead, it tells the Docker build to not use a base image at all. Without any operating system files from a base image, the result image can contain as little as a single file: your binary that is copied over from the builder stage. Note that depending on the programming language and your code, you might have to make further adjustments on compiler options as binary files might rely on some operating system files to exist.

### Keep your image clean
{: #clean-basics}

When you are first developing your Dockerfile and debugging how it works, you might install some temporary tools or apply other workloads that are not required to be in the final container image. Removing those temporary files and workloads keeps your image clean, small, and more secure.

## Improving the start time of your image
{: #image-startup}

For maximum efficiency, your container image must start as fast as possible. For applications, the relevant metric is how long it takes for the HTTP endpoint to be available and ready to accept and process incoming HTTP requests. Start speed is especially important for {{site.data.keyword.codeengineshort}} applications that are based on Knative. Such applications can be configured to scale down to zero running instances when there is no traffic, thus consuming no resources and costing no money. When a request comes in, an instance is started to handle the request. Your container must start as fast as possible to respond to the new request.

To improve the startup of your application, investigate the implementation of your application and see whether you can apply patterns such as:

- Parallelization of independent initialization work, for example, to establish a connection to a database and to read the configuration file to communicate with a mail server from environment variables.
- Delaying of initialization work that is not needed for application startup and instead perform them on first need basis.

In addition, you can also avoid a common pitfall when you implement a web application that uses a framework such as Angular, React, or Vue. Each of these frameworks is based on Node.js with NPM and includes a command-line interface that can make it easy to set up a project. For example, a React application that is created with [create-react-app](https://github.com/facebook/create-react-app) command sets up a `package.json` file that includes some predefined scripts. One of these scripts is `start`, which brings up a web server with your web application. Your Dockerfile can look similar to the following example,

```Dockerfile
FROM nodejs:12-alpine

ADD . /app
WORKDIR /app

RUN npm install

EXPOSE 3000
ENTRYPOINT ["npm", "run", "start"]
```
{: codeblock}

While this type of Dockerfile works, it is not fast as whenever the `npm run start` command is invoked, the application is compiled and then started. This delay is especially noticeable with applications that go beyond a small sample size. The correct approach is to compile the application at build time and serve it only at startup,

```Dockerfile
FROM node:12-alpine AS builder

ADD . /app
WORKDIR /app

RUN npm install && npm run build

FROM node:12-alpine

RUN npm install -g serve

COPY --from=builder /app/build /app

EXPOSE 8080
ENTRYPOINT ["serve", "-l", "8080", "/app"]
```
{: codeblock}

You see again the builder and runtime two-stage pattern. Also note that the updated sample uses a different port, `8080`. While this example works with any other port, `8080` is the default port for {{site.data.keyword.codeengineshort}} applications. In addition, by using the compiled build, all of the sources and tools that are installed in the `node_modules` are not included in the final container image, which reduces its size 281 - 97 MB.

## Running a container as non-root
{: #container-non-root}

Well-designed systems follow the principle of least privilege - an application or a user gets only those privileges that it requires to perform a specific action. In {{site.data.keyword.codeengineshort}}, you run an application server or some batch logic, which, in most cases, does not require administrative access to the system. Therefore, it must not run as root in its container. A good practice is to set up the container image with a defined user and to run as non-root. For example, based on our previous scenario,

```Dockerfile
FROM node:12-alpine AS builder

ADD . /app
WORKDIR /app
RUN npm install && npm run build

FROM node:12-alpine

RUN npm install -g serve

COPY --from=builder /app/build /app

USER 1100:1100
EXPOSE 8080
ENTRYPOINT [ "serve", "-l", "8080", "/app" ]
```
{: codeblock}

The Dockerfile uses the `USER` command to specify that it wants to run as user and group 1100. Note that this command does not implicitly create a named user and group in the container image. In most cases, this structure is acceptable, but if your application logic requires the user and also its home directory to exist, then you must create the user and group explicitly:

```Dockerfile
FROM node:12-alpine AS builder

ADD . /app
WORKDIR /app
RUN npm install && npm run build

FROM node:12-alpine

RUN npm install -g serve && \
  addgroup nonroot --gid 1100 && \
  adduser nonroot --ingroup nonroot --uid 1100 --home /home/nonroot --disabled-password

COPY --from=builder /app/build /app

USER 1100:1100
EXPOSE 8080
ENTRYPOINT [ "serve", "-l", "8080", "/app" ]
```
{: codeblock}

The `RUN` command in the runtime stage was extended to call the `addgroup` and `adduser` commands to create a group and a user with a home directory.
