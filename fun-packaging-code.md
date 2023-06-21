<staging>---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-21"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Packaging dependencies for your Function
{: #fun-package}

You can create Functions in many different programming languages. When your Function code grows complex, you can add code modules as dependencies for your Function. Each language has its own modules to use with your Function code. For example, Node.js dependencies are usually existing `npm` modules, whereas Python and Golang use Python packages or Golang modules. These dependencies must be declared with your action source code and compressed into one zip before you can run your code as a Function. 

## Packaging modules for a Node.js Function
{: #function-nodejs-ce}

Package your Function source code as a file called `main.js` together with a `package.json` file that lists the dependent modules, by compressing them into a `function.zip` file.

1. Create your Function by writing your code into a `main.js` file 

    ```javascript
    function main(args) {
	  	  const oneLinerJoke = require('one-liner-joke');
	  	  let getRandomJoke = oneLinerJoke.getRandomJoke();

  		  return {
              	headers: { 'Content-Type': 'text/plain;charset=utf-8' },
          	    body: getRandomJoke
      	}
    }

    module.exports.main = main;
    ```
    {: codeblock}
  
2. Create a `package.json` containing your required dependencies for your Function

    ```sh
    {
	    "name": "my-action",
	    "main": "main.js",
    	"dependencies" : {
   		"one-liner-joke" : "1.2.2"
     	}
    }
    ```
    {: codeblock}

3. Compress these files into an archive called function.zip.

    ```sh
    zip -r function.zip main.js package.json
    ```
    {: pre}
  
    Now you have an injectable compressed Function that can be run on {{site.data.keyword.codeengineshort}}.

4. Create your compressed file as a Function in {{site.data.keyword.codeengineshort}}.
    
    - If your app uses Node.js version 16, your Function can run without providing the runtime.
  
        ```sh
        ibmcloud ce fn create --name action-node-zip --runtime nodejs-16 --code archive.zip
        ```
        {: pre}
  
    - If your app uses a different version of Node.js, you can create a custom image that uses your runtime.
  
        ```sh
        ibmcloud ce fn create --name action-custom-image --runtime-type custom --runtime icr.io/<namespace>/<repository>:<tag> --registry-secret my-icrio-secret --code archive.zip
        ```
        {: pre}

For more information the `fn-x create` command and its options, see [Create a Function](#function-command-create).

## Packaging modules for a Python Function
{: #function-python}

Package your Function source code as `__main__.py`, together with a `requirements.txt` file that lists the dependent modules, and compress them into a `function.zip` file. Note that the name of the source file must be `__main__.py`.

1. Create your Function by writing your code into a `main.py` file 

    ```py
    import pyjokes
    def main(params):
	    return {
	    	      "headers": { 'Content-Type': 'text/plain;charset=utf-8' },
	    	      "body": pyjokes.get_joke()
    	}
    ```
    {: pre}

2. Create a `requirements.txt` containing your required dependencies for your Function

    ```sh
    pyjokes==0.6.0
    ```
    {: pre}

3. Compress these files into an archive called `function.zip`.
  
    ```txt
    zip -r function.zip __main__.py requirements.txt
    ```
    {: pre}
  

4. Create your compressed file as a Function in {{site.data.keyword.codeengineshort}}.
  
    - If your app uses Python version 3.9, your Function can run without providing the runtime.
  
        ```sh
        ibmcloud ce fn create -n python-function-pyjokes -r python-3.9 --rt managed --code function.zip --cpu 0.25 --memory 1G
        ```
        {: pre}
  
    - If your app uses a different version of Python, you can create a custom image that uses your runtime.
  
      ```sh
      ibmcloud ce fn create --name action-custom-image --runtime-type custom --runtime icr.io/<namespace>/<repository>:<tag> --registry-secret my-icrio-secret --code function.zip
      ```
      {: pre}


## Packaging modules for a Golang Function
{: #function-golang}

Package your Function source code as a file called `main.go`, together with the `go.mod` and `go.sum` files and compress them into a `function.zip` file.

1. Create your Function by writing your code into a `main.go` file

    ```go
    package main

    import (
    	"fmt"
	    "os"

    	"github.com/rs/zerolog"
    )

    func init() {
    	zerolog.TimeFieldFormat = zerolog.TimeFormatUnix
    }

    func Main(params map[string]interface{}) map[string]interface{} {
    	fmt.Println("Start")

	    // define the action response object
	    response := make(map[string]interface{})

	    // add process environment variables to params so
	    // that it becomes part of the response body
	    params["env"] = os.Environ()

	    // log all action parameters
	    fmt.Printf("params: %v\n", params)

	    // return statusCode, response headers and body
	    response["statusCode"] = 418
	    response["headers"] = map[string]interface{}{
	    	"Content-Type": "application/json;charset=utf-8",
		    "Set-Cookie": [...]string{
			    "UserID=Anonymous; Max-Age=3600; Version=",
			    "SessionID=asdfgh123456; Path = /",
		    },
	    }
	    response["body"] = params

	    return response
    }

    ```
    {: codeblock}

2. Create a `go.mod` containing your required dependencies for your Function

    ```go
    module go-function

    go 1.17

    require github.com/rs/zerolog v1.29.0

    require (
    	github.com/mattn/go-colorable v0.1.12 // indirect
    	github.com/mattn/go-isatty v0.0.14 // indirect
    	golang.org/x/sys v0.0.0-20210927094055-39ccf1dd6fa6 // indirect
    )

    ```
    {: codeblock}

3. Create a `go.sum` file by running the following command.
  
    ```txt
    go mod tidy
    ```
    {: pre}
  
4. Package the code and `go.mod` file to an archive called `function.zip`.

    ```sh
    zip -r function.zip main.go go.mod go.sum
    ```
    {: pre}

    Now your injectable compressed Function can run on {{site.data.keyword.codeengineshort}}.
  
5. Create your compressed file as a Function in {{site.data.keyword.codeengineshort}}.
  
      - If your app uses Golang version 1.17, your Function can run without providing the runtime.
  
          ```sh
          ibmcloud ce fn create -n go-function-zerolog -r golang-1.17 --rt managed --code function.zip --cpu 0.25 --memory 1G
          ```
          {: pre}
  
      - If your app uses a different version of Golang, you can create a custom image that uses your runtime.
  
          ```sh
          ibmcloud ce fn create --name action-custom-image --runtime-type custom --runtime icr.io/<namespace>/<repository>:<tag> --registry-secret my-icrio-secret --code function.zip
          ```
          {: pre}
  
For more information about the `fn create` command and its options, see [Create a Function](#function-command-create).
