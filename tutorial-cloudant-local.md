---

copyright:
  years: 2022, 2022
lastupdated: "2022-08-03"

keywords: code engine, tutorial, build, local, application, access, build run, image

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Building applications that store information in {{site.data.keyword.cloudant}} 
{: #tutorial-cloudant-local}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Learn how to build your {{site.data.keyword.codeengineshort}} application from source code that is stored on your local workstation. This tutorial uses sample source that is used to build the app. This application connects to an {{site.data.keyword.cloudant}} database and stores input from that app.
{: shortdesc}

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks.

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).
- [Git](https://git-scm.com/downloads){: external}
- [Node.js and NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){: external}

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Create an {{site.data.keyword.cloudant}} service instance and database
{: #create-cloudant}
{: step}

Your first step is to create an {{site.data.keyword.cloudant}} service instance and then create a database. You can create one [from the console](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant) or by using CLI commands. In addition, create service credentials that you can pass to your application.

1. Create an {{site.data.keyword.cloudant}} service instance, follow the steps in [Getting started with {{site.data.keyword.cloudant}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant). Name your instance `CloudantFruitCounter`. Be sure to complete the task by creating your service credentials.
2. Open the {{site.data.keyword.cloudant}} dashboard for your instance and click **Create database**.
3. In the **Create database** window, enter the database name `fruitcounter`.
4. Do not select the  **Partitioned** option, and click **Create**.

## Test your application locally
{: #test-cloudant-local}
{: step}

Before you create your code as an application in {{site.data.keyword.codeengineshort}}, test your code locally to make sure that it is functioning correctly.

1. Retrieve the {{site.data.keyword.cloudant}} service credentials from the {{site.data.keyword.cloudant}} dashboard. For more information about retrieving credentials, see [Creating service credentials](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant#creating-service-credentials).
2. Set environment variables with the values from the service credentials.

    ```txt
    export CLOUDANT_URL=<your_url>
    ```
    {: codeblock}
    
    ```txt
    export CLOUDANT_APIKEY=<your_key>
    ```
    {: codeblock}
    
    ```txt
    export DBNAME="fruitcounter"
    ```
    {: codeblock}

3. Clone the `fruit-counter` repository, change to this directory, and then install and start the dependencies.

    ```txt
    git clone https://github.com/IBM/CodeEngine
    cd CodeEngine/fruit-counter
    npm install
    npm run start
    ```
    {: pre}
    
4. Open a browser and go to [http://localhost:8080](http://localhost:8080){: external}.
5. Pick your favorite fruit and submit your choice. The app accepts your choice and displays a running total of picks.
 
You can verify that your fruit choice was registered in the Cloudant by going to your {{site.data.keyword.cloudant}} database dashboard.

Let's look at how this program works.

This application is a simple Node.js application that uses two main packages.

- [`@ibm-cloud/cloudant`](https://github.com/IBM/cloudant-node-sdk){: external} to connect to {{site.data.keyword.cloudant}} and to read and write data.
- [Express](https://expressjs.com/){: external} to create a web server that allows users to submit their choice of fruit and see a running total of our data.

This application is made up of two main files.

server.js
:    The `server.js` file is used to run the web server and communicates with Cloudant. After a user selects a fruit choice, the front end page submits the value to the `/fruit` route (see below), the `app.route` function stores a new document in Cloudant with the fruit choice, and then reads back the running total to return to the front end page. 
:    The read operation uses a Cloudant design document and a `MapReduce` view to aggregate documents. For more information about views and design documents, see [Creating Views (MapReduce)](/docs/Cloudant?topic=Cloudant-creating-views-mapreduce).

index.html
:    The `index.html` file is the web page of the application that uses the `Vue.js` framework. When this page loads, it displays the available fruit options.
:    After you submit your choice, the framework makes an HTTP POST request with your fruit selection to the `/fruit` route of the application. The application return contains the running total of fruit choices, which is then displayed.

## Deploying your application to {{site.data.keyword.codeengineshort}}
{: #deploy-cloudant-ce}
{: step}

Now that you understand how this application works, you can deploy it to {{site.data.keyword.codeengineshort}}. You can follow the steps to deploy an [application from a public repository](/docs/codeengine?topic=codeengine-deploy-app), specifying `CODEENGINEREPO` as your image repository.  Be sure to include the environment variables that you gathered and set locally in step 2. 

Because you cloned the repository when you [tested your application locally](#test-cloudant-local), you can use the **`app create`** command to both build an image from your local source and deploy your application that references this built image. 

1. Run the **app create** command. You must provide a name for your application and the location of the source code. The following example creates an application called `myfruitcounter` that uses the `docker` strategy and provides the location for the source code in the current directory (`.`). You must also set the environment variables to connect to Cloudant.

    ```txt
    ibmcloud ce app create --name myfruitcounter --build-source . --strategy dockerfile --env CLOUDANT_URL=<your_url> --env CLOUDANT_APIKEY=<your_key> --env DBNAME=fruitcounter  
    ```
    {: pre}

    Example output

    ```txt
    Creating application 'myfruitcounter'...
    Packaging files to upload from source path '.'...
    Submitting build run 'myfruitcounter-run-220727-142949868'...
    Creating image 'private.us.icr.io/ce--6ef04-n2lgvg2l59v/app-myfruitcounter:220727-1929-y8ej0'...
    Waiting for build run to complete...
    Build run status: 'Running'
    Build run completed successfully.
    Run 'ibmcloud ce buildrun get -n myfruitcounter-run-220727-142949868' to check the build run status.
    Waiting for application 'myfruitcounter' to become ready.
    Configuration 'myfruitcounter' is waiting for a Revision to become ready.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready.
    Run 'ibmcloud ce application get -n myfruitcounter' to check the application status.
    OK                                                

    https://myfruitcounter.n2lfrg2876v.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

2. Test the app by opening the provided URL for the fruit picker app. Pick your favorite fruit and submit. The running total of fruit choices is displayed. You can refresh the application and choose another fruit. The addition is displayed in the running total.



