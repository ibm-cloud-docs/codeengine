---

copyright:
  years: 2024
lastupdated: "2025-07-01"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Exchanging data with functions
{: #fun-exchanging-data}

Invoking a {{site.data.keyword.codeengineshort}} functions service (or simply a function) is accomplished on the client side through HTTP requests. Information can be passed to the function in the following ways:

* As part of the URL (path and optionally, query parameters)
* Through HTTP request headers
* Through the HTTP request body

A caller receives these values on the client side as an HTTP response. The response data passes as follows:

* As HTTP response code
* Through HTTP response headers
* Through the HTTP response body

All rules and capabilities to invoke a function through HTTP requests and the resulting HTTP responses are the _external data interface_.

An incoming HTTP request is forwarded to the function code for processing by using the rules of the _internal request data interface_. The results that are provided by the function code must follow the rules of the _internal response data interface_.

The following diagram shows information flow from a client that uses the external data interface. The process uses the {{site.data.keyword.codeengineshort}} functions service and the internal request data interface to the function code. Likewise, the resulting data flows from the function code to the internal response data interface through the {{site.data.keyword.codeengineshort}} functions service, and the external data interface flows back to the caller.

![Functions interfaces.](images/ce_functions_interfaces.svg "Functions interfaces"){: caption="Information flow for {{site.data.keyword.codeengineshort}} functions" caption-side="bottom"}

## External request data interface
{: #fun-external-data-interface-request}

The external data interface definition is derived from standardized HTTP.

### MIME types
{: #fun-external-data-interface-MIME-types}

MIME types are used to define the format of the HTTP request information and the HTTP response.

The following IANA MIME types are supported for the content-type (`Content-Type`) of the HTTP requests or HTTP responses. MIME type parameters are supported, but not included in this list:

* JSON type:
    * `application/json; <parameters>`
* Binary types:
    * `audio/*; <parameters>`
    * `application/octet-stream; <parameters>`
    * `example/*; <parameters>`
    * `font/*; <parameters>`
    * `image/*; <parameters>`
    * `model/*; <parameters>`
    * `multipart/*; <parameters>`
    * `video/*; <parameters>`
* Text types:
    * `text/plain; <parameters>`
    * `text/html; <parameters>`
    * `text/*; <parameters>`
* Percent-encoded type:
    * `application/x-www-form-urlencoded; <parameters>`

### Request data
{: #fun-external-data-interface-request-data}

When a function is invoked, it can receive arbitrary data (request payload) in text or binary form. The presence of a `Content-Type` value in the HTTP request header determines the form and encoding of the data that is sent to the function. The data structure, the format, and the content type must match. The {{site.data.keyword.codeengineshort}} functions service runs a minimal validation check on the data by considering the content-type and responds with the HTTP status code `400` in certain cases; for example, if the JSON data format or encoding is invalid.

For all other selected `Content-Type` values, it is expected that the data format matches the restrictions of the MIME-type.

### Providing request data as query parameters
{: #fun-external-data-interface-providing-request-data=as=query}

Request data can be provided as key-value pairs in URL-encoded format (also called percent-encoded) in the HTTP URL.

Percent-encoding is widely used in web technology. All 8-bit characters are written as hexadecimal values preceded by a percentage sign (%). This type of encoding is also known as URL-encoding.

Example of invoking a function by using query parameters:

```javascript
curl -v "https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/?planet1=Mars&planet2=Jupiter"
```
{: screen}

### Providing request data in the request body
{: #fun-external-data-interface-providing-request-data-in-body}

Request data is provided in the body section of the HTTP request. The format of the data must match the provided `Content-Type` value.

Examples of invoking a function by using body data on UNIX&reg;:

```javascript
curl -v -H "Content-Type: application/x-www-form-urlencoded" -d 'location=planet%20earth' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud

curl -v -H "Content-Type: application/json" -d "{'planet1': 'Mars', 'planet2': 'Jupiter'}" https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
```
{: screen}

Example of invoking a function by using body data in Windows&trade;:

```javascript
curl -v  -H "Content-Type: application/json" -d "{\"key_1\":\"Mars\",\"planet2\":\"Jupiter\"}"  "https://function-nodejs-95.1057yuwab63w.us-east.codeengine.appdomain.cloud"
```
{: screen}

If the `Content-Type` value is missing for a request, {{site.data.keyword.codeengineshort}} handles the data payload as described for `application/json`.
{: tip}

### Providing request header data
{: #fun-external-data-interface-providing-request-header}

Request data is provided in key-value pairs in the header section of the HTTP request.

Example of invoking a function by using header fields:

```javascript
curl -v -H "Sample_Data: Sample_Value"  https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
```
{: screen}

### Providing request mixed data
{: #fun-external-data-interface-providing-request-mixed-data}

{{site.data.keyword.codeengineshort}} functions support the use of different ways to provide request data within a single HTTP request.

Example of invoking a function by using body data and header fields:

```javascript
curl -v -H "Sample_Data: Sample_Value" -H "Content-Type: application/x-www-form-urlencoded" -d 'planet1=Mars&planet2=Jupiter' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
```
{: screen}

Example of invoking a function by using body data, headers, and query parameters:

```javascript
curl -v -H "Sample_Data: Sample_Value" -H "Content-Type: application/x-www-form-urlencoded" -d 'planet1=Mars&planet2=Jupiter' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/?planet1=Mars&planet2=Jupiter
```
{: screen}

## Internal request data interface
{: #fun-internal-data-interface-requests}

The internal request data interface describes how the {{site.data.keyword.codeengineshort}} functions service delivers request data that is received on the external data interface to the function code. Independent of the coding language, you can implement function logic to put all request parameters in the main() function as the first parameter.

You can use any name for this parameter; in the proceeding examples, the parameter is called `args`.
{: tip}

Also, the function code receives a set of automatically injected pre-defined environment variables.

Python example:

```javascript
import os
def main(args):
  # raw_input_data = args.__ce_body;  # uncomment this line if client is providing data in the request body
  all_input=args;
  env=dict(os.environ)
  print("Return body:",all_input)
  return {
    "statusCode": 200,
    "body" : all_input,
  }
```
{: screen}

Node.js example:

```javascript
function main(args) {
  const body = {
    args,
    env: process.env,
  };

  console.log(`Return body: ${JSON.stringify(body, null, 2)}`);

  return {
    statusCode: 200,
    "body" :  body,
  };
}

module.exports.main = main;
```
{: screen}

The {{site.data.keyword.codeengineshort}} functions service uses different encodings for the input data to help ensure that the function code can access the input data in the `args` argument. The encodings help ensure that structured data, plain text, data, and binary data can be part of the input data.

### Text encoding
{: #fun-internal-data-interface-requests-text}

Text encoding is used for elements in the input `args` parameter that contain text payload. The encoding is necessary to help ensure that special characters are escaped and do not damage the data structure of the `args` parameter.

{{site.data.keyword.codeengineshort}} runs the text content encoding before it calls the main() function. The function's program logic might need to unescape them to re-create the original data.

Supported escape characters:

* Backspace is replaced with `\b`.
* Form feed is replaced with `\f`.
* Newline is replaced with `\n`.
* Carriage return is replaced with `\r`.
* Tab is replaced with `\t`.
* Double quotation marks are replaced with `\"`.
* Backslash is replaced with `\\`.

#### Base64 encoding
{: #fun-internal-data-interface-requests-Base64}

Base64 encoding is used for elements in the input `args` parameter that can break the internal data structure of the `args` parameter. Encoding it as Base64 helps ensure that the whole value consists only of readable characters in a 64-character alphabet.

For example:

```text
"eyAicGxhbmV0MSI6Ik1hcnMiLCAicGxhbmV0MiI6Ikp1cGl0ZXIiIH0="
```
{: screen}

#### Percent encoding (URL-encoding)
{: #fun-internal-data-interface-requests-percent}

Percent-encoding is widely used in web technology. All 8-bit characters are written as hexadecimal value preceded by a percentage sign (%). This type of encoding is also known as URL-encoding. The function receives the `form-urlencoded` type data in raw format in the `__ce_body` parameter.

The {{site.data.keyword.codeengineshort}} functions service passes the query parameters as-is (the leading `?` is not part of it) into the `__ce_query` field of the `args` parameter. This way, the function code receives this parameter in URL-encoded format; for example:

```text
"x%5cb=1%22f4%20and%20"
```
{: screen}

### The `args` parameter
{: #fun-args}

The `args` parameter is a language-specific data structure (JSON object for Node.js and `dict` (dictionary) type for Python) filled with the request input data in the following format:

| Top-level elements | Description |
|--------------------|-------------|
| `__ce_<service_variable>`        | {{site.data.keyword.codeengineshort}} service internal input argument.   |
| `__ce_headers`      | A copy of the HTTP request header element.   |
| `<property>` (optional)   | Top-level properties available if the HTTP request input data is provided in structured format (only if a content-type of `application/json` is used).  |
{: caption="Elements for the `args` parameter"}

```javascript
  {
    "args": {
      "__ce_body": "eyAicGxhbmV0MSI6Ik1hcnMiLCAicGxhbmV0MiI6Ikp1cGl0ZXIiIH0=",
      "__ce_headers": {
        "Accept": "*/*",
        "User-Agent": "curl/7.58.0",
        "X-Request-Id": "d03a1af0-bfc8-4a50-be7d-a72040c02cc9",
        "Content-Type": "application/json",
      },
      "__ce_method": "GET",
      "__ce_path": "/",
      "__ce_query": "",
      "planet1": "Mars",
      "planet2": "Jupiter"
      }
  }
```
{: screen}

#### `args` parameter set for internal input arguments (`__ce_*`)
{: #fun-args-internal}

The {{site.data.keyword.codeengineshort}} functions service injects reserved input arguments to the `args` input data.

The following parameters can appear in the `args` argument depending how the caller provides the request data:

| Parameter name     | Value type        | Description |
|--------------------|-------------------|-------------|
| `__ce_method`        | String            | The HTTP request method (either a GET or POST request). |
|`__ce_headers`       | Map of key-value pairs  | Key-value pairs of HTTP request header. |
| `__ce_path`          | String            | URL path of the incoming HTTP request.  |
| `__ce_body`          | String            | The request body entity, as a Base64-encoded string when request content type is binary, or as a plain string, otherwise.  |
| `__ce_query`         | String            | The query parameters from the request as an unparsed string. The `__ce_query` parameter is a single string that contains the query parameters that are parsed from the URL, without the leading question mark (?), and separated by an ampersand (&).  |
{: caption="Parameters for a {{site.data.keyword.codeengineshort}} function's input arguments"}

The internal `__ce_*` parameters cannot be overwritten with request data that is provided in the HTTP request. HTTP calls trying to overwrite fails with status code `400` (Bad Request).

#### Contents of `args` parameter if a caller provides request data by query parameters
{: #fun-args-query=parameters}

A function receives query parameter data as key-value pairs in the `__ce_query` parameter, and is percent-encoded (URL-encoded). Also, each single query parameter is a key-value pair within the decoded format:

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | No                | Body |
| `__ce_headers`       | Yes               | Header with no content-type |
| `__ce_query`         | Yes               | Query parameter (URL-encoded) |
| Top-level property | Yes               | Key-value pair (URL-decoded and text-encoded)  |
{: caption="args parameter from query parameters when invoking functions"}

Python example of accessing query parameters:

```javascript
import os
def main(args):
  query_parm_1 = args.get("key", "default_value") # get the value of one query parameter

  try:
    query = args["__ce_query"]  # get all query parms
  except:
    query= "not part of request"

  return {
    "statusCode": 200,
    "body": query,
  }
```
{: screen}

Node.js example of accessing query parameters:

```javascript
function main(args) {
  var query_parm_1 = args.key     // get the value of one query parameter
  var query = args.__ce_query     // get all query parameters

  return {
    statusCode: 200,
    "body" : query,
  };
}

module.exports.main = main;
```
{: screen}

#### Contents of `args` parameter if a caller provides request data by header data
{: #fun-args-heder-data}

A function receives request header data as key-value pairs in the `__ce_headers` parameter. The key-value pair is converted into a canonical format, regardless of which format that the key is set on the external data interface. For instance, both `mykey` or `MYKEY` are converted to `Mykey`:

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | No                | Body            |
| `__ce_headers`       | Yes               | Header in key-value pair (text-encoded) (key is in canonical format). |
| `__ce_query`         | ""                | The query parameter is an empty string. |
| Top-level property | No                |   |
{: caption="args parameter from header parameters when invoking functions"}

Python example of accessing header data:

```javascript
import os
def main(args):

  try:
    header = args["__ce_headers"]  # get complete header
    # value_1 = args["__ce_headers"]["Key_1"]  # get value of the Header parm with "Key_1"
  except:
    header = "not part of request"

  return {
    "statusCode": 200,
    "body": header,
  }
```
{: screen}

Node.js example of accessing header data:

```javascript
function main(args) {
  // var header_parm_1 = args.__ce_headers.Key_1  //get the value of one header parameter
  var header = args.__ce_headers  // get all header parameters

  return {
    statusCode: 200,
    "body" : header,
  };
}

module.exports.main = main;
```
{: screen}

#### `args` parameter from request data of content-type `application/json`
{: #fun-args-header-application-json}

A function receives the keys and values of the JSON document as dedicated top-level property parameters.

When no value is set for `Content-type` in the HTTP request, then the {{site.data.keyword.codeengineshort}} function uses `application/json` as the default.

In addition, the JSON payload is made available to the function as-is (as byte array) in Base64-encoded format in the `__ce_body` parameter.

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | Yes               | Request data (Base64-encoded) |
| `__ce_headers`       | Yes               | Content-type is set |
| `__ce_query`         | ""                | Empty string |
| Top-level property | Yes               | Key-value pair for each top-level element (text-encoded)   |
{: caption="args parameter from query parameters when invoking functions"}

Python example of accessing `application/json` input data:

```javascript
import os
def main(args):
  try:
    body_encoded = args["__ce_body"]  # get complete header (base64 encoded)
    value_1 = args["key_1"]           # get value of the Header parm with "key_1"
  except:
    value_1 = "not part of request"

  return {
    "statusCode": 200,
    "body": value_1,
  }
```
{: screen}

Node.js example of accessing `application/json` input data:

```javascript
function main(args) {
  var body  = args.__ce_body  // get complete request body (base64 encoded)
  var value_1 = args.key_1    // get value of one single key

  return {
    statusCode: 200,
    "body" : value_1,
  };
}

module.exports.main = main;
```
{: screen}

#### `args` parameter from request data of content-type `application/octet-stream`
{: #fun-args-request-data-application-octet-stream}

A function receives binary data in Base64-encoded format for the `__ce_body` binary data in the `__ce_body` parameter:

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | Yes               | Request data (Base64-encoded) |
| `__ce_headers`       | Yes               | Content-type is set |
| `__ce_query`         | ""                | Empty string |
| Top-level property | No                |   |
{: caption="args parameter from request data"}

Python example of accessing `application/octet-stream` input data:

```javascript
import os
import base64

def main(args):
  try:
    body = base64.b64decode(args['__ce_body']).decode("utf-8")   # read binary data into the body variable
  except:
    body = "not binary data found"

  return {
    "headers": { "Content-Type": "text/plain" },  # text/plain, if ensured binary data do not conain backslash and double quotes
    "statusCode": 200,
    "body": body,
  }
```
{: screen}

Node.js example of accessing `application/octet-stream` input data:

```javascript
function main(args) {
  var base64EncodedBody = args.__ce_body   // get complete request body (base64 encoded)
  var body = Buffer.from(args.__ce_body, 'base64').toString('utf-8') //  read binary data into the body variable

  return {
    statusCode: 200,
    "body" : body,
  };
}

module.exports.main = main;
```
{: screen}

#### `args` parameter from request data of content-type `text/plain`
{: #fun-args-request-data-application-text-plain}

A function receives text type data in Base64-encoded format in the `__ce_body` parameter:

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | Yes               | Request data (text-encoded) |
| `__ce_headers`       | Yes               | Content-type is set |
| `__ce_query`         | ""                | Empty string |
| Top-level property | No                |   |
{: caption="args parameter from request data"}

The function's program logic might need to unescape them to re-create the original data.

Python example of accessing `text/plain` input data:
```javascript
import os
def main(args):
  body = args['__ce_body']  # get request body, is text encoded (escaped)

  return {
    "headers": { "Content-Type": "text/plain" },
    "statusCode": 200,
    "body": body,
  }
```
{: screen}

Node.js example of accessing `text/plain` input data:
```javascript
function main(args) {
  var body  = args.__ce_body  // get complete request body (text encoded)

  return {
    statusCode: 200,
    "body" : body,
  };
}

module.exports.main = main;
```
{: screen}

#### `args` parameter from request data of content-type `application/x-www-form-urlencoded`
{: #fun-args-request-data-application-application-x-www-form-urlencoded}

A function receives the complete body data in text-encoded format in the `__ce_body` parameter:

| `args` field         | Is this set?          | Description |
|--------------------|-------------------|-------------|
| `__ce_body`          | Yes               | Request data (text-encoded) |
| `__ce_headers`       | Yes               | Content-type is set |
| `__ce_query`         | ""                | Empty string |
| Top-level property | No                |   |
{: caption="args parameter from request data"}

Python example of accessing `application/x-www-form-urlencoded` input data:

```javascript
import os
def main(args):
  body = args['__ce_body']  # get request body, is url-encoded (%)

  return {
    "headers": { "Content-Type": "text/plain" },
    "statusCode": 200,
    "body": body,
  }
```
{: screen}

Node.js example of accessing `application/x-www-form-urlencoded` input data:

```javascript
function main(args) {
  var body  = args.__ce_body  //get request body, is url-encoded (%)

  return {
    statusCode: 200,
    "body" : body,
  };
}

module.exports.main = main;
```
{: screen}

#### `args` parameter from request data of content-type `application/x-www-form-urlencoded` and query parameters
{: #fun-args-request-data-application-application-x-www-form-urlencoded-query}

All combinations of mixed data types are possible, but consider that for HTTP requests with URL query parameters and body parameters, the body parameters take precedence over query parameters.

### {{site.data.keyword.codeengineshort}} function environment variables
{: #fun-env-vars}

While function call parameters are derived from the incoming HTTP request, a {{site.data.keyword.codeengineshort}} function also has access to a set of pre-defined environment variables derived from system settings:

* CE_ALLOW_CONCURRENT
* CE_API_BASE_URL
* CE_DOMAIN
* CE_EXECUTION_ENV
* CE_FUNCTION
* CE_PROJECT_ID
* CE_REGION
* CE_SUBDOMAIN

For more information about these environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

Python example of accessing environment variables:

```javascript
import os

def main(args):
  curEnv=dict(os.environ)
  return {
    "headers": { "Content-Type": "application/json" },
    "statusCode": 200,
    "body": {
      "env": curEnv,
    }
  }
```
{: screen}

Node.js example of accessing environment variables:

```javascript
function main(args) {
  var curEnv = process.env; //read the function's env vars

  return {
    "headers": { "Content-Type": "application/json" },
    "statusCode": 200,
    "body": {
      "env": curEnv,
    }
  };
}

module.exports.main = main;
```
{: screen}

## Internal response data interface
{: #fun-internal-response-data-interface}

The internal response data interface depicts how function code provides response data. The {{site.data.keyword.codeengineshort}} functions service processes the data and provides an HTTP response to the caller.

Independent of the programming language, the function code must provide the response data as data structure in the return statement.

Dependent of the programming language, the result object is either a JSON object (Node.js language) or a dictionary (Python language) with the following structure:

| Functions result data |   Requirement  | Description                     |
|---------------------------|----------------------|---------------------------------|
| `headers`                   | Optional             | A result object in which the keys are header names and the values are strings, numbers, or Boolean values. To send multiple values for a single header, the header's value is an array of the multiple values. No headers are set by default. |
| `statusCode`                | Should (default 200) | A valid HTTP status code. |
| `body`                      | Optional (default: empty) | A string that is either plain text, a JSON object or array, or a Base64-encoded string for binary data. The body is considered empty if it is null, an empty string (""), or undefined.|
{: caption="Result object structure in a JSON object (Node.js language) or a dictionary (Python language)"}

Example result data structure to provide function execution result data:

```javascript
import os
def main(args):
  return {
    headers: {
      "content_type" : "application/json" ,
      "key" , "value"
    },
    "statusCode": 200,
    body: {"myMessage" : "sample message"}
  }
```
{: screen}

Always set `body` and `statusCode`. The implicit setting of `statusCode` and body is only available for compatibility to deprecated {{site.data.keyword.codeengineshort}} functions.
{: note}

### `headers` element
{: #fun-headers-element}

 The main intention of the headers section is to define the content-type in which the function is going to provide the response data. Result data supports the identical `MIME-Type` value as accepted on request.

Depending on the value of the `Content-Type` value, the body field in the result structure must contain the following aspects:

| Content type       | Value that is assigned to the body element | Example                     |
|--------------------|------------------------------|-----------------------------|
| `application/json`   | JSON object                  | `body : { key_1: val1 }`      |
| Not set (default)  | String                       | `body :  "some text"`         |
| `text/*`             | String                       | `body :  "some text"`         |
| `audio/*`, `example/*`, `font/'`, `image/*`, `video/*`, and all remaining types | Base64-encoded | `body: "SGVsbG8gV29ybGQhCg=="` |
{: caption="Body field result structure"}

Also the function code can use key-value pairs in the HTTP response header to provide response data. Therefore, the code must put a unique key name and its value in the headers section of the data structure that is used in the return statement.

Take note of these key name considerations:

* Key names are case-insensitive
* The most recent value assignment of identical key names is used
* Backslashes or blanks are not supported

Take note of these value considerations:
* Values must be text-encoded
* Values must be of data type string or array of string

Example of returning response data as a header key-value pair:

```javascript
import os
def main(args):

  return {
    "headers": {
      "Content-Type": "text/plain",
      "key_1" : "sample_value",
    },
    "statusCode": 200,
    "body": "" ,
  }

```
{: screen}

### `statusCode` element
{: #fun-statusCode-element}

Functions code must explicitly set a status code (default `200`) to inform the caller about the execution result. You can use any valid HTTP return status code (that is, status code `200` to `599`).

The {{site.data.keyword.codeengineshort}} functions service returns the function's status code in the header field (`x-faas-actionstatus`) and as an HTTP status code.

If the `statusCode` is invalid, then the {{site.data.keyword.codeengineshort}} functions service returns the HTTP return code `422` (Invalid function code cannot be processed) without the `x-faas-actionstatus` header field and without extra response data.

If the result size limit for functions is reached, an HTTP status code of `400` is returned to the client.

Example of returning response status code:

```javascript
import os
  def main(args):

  return {
    "statusCode": 200,
    "body": "" ,
  }
```
{: screen}

### `body` element
{: #fun-body-element}

Function code can include the `body` section of the return data structure to provide the function's response data. The function code is responsible for delivering the `body` element in the return data structure in matching format to the `Content-Type`. If the function response `Content-Type` is missing, then the function code returns `Content-Type: text/plain; charset=utf-8` at the external interface, and the data from the `body` field in its unaltered form.

Consider the following body rules, depending on the content-type used.

#### Body value of content-type `application/json`
{: #fun-body-element-application-json}

Function code must provide the value of the `body` element as a valid data structure (NodeJs-JSON or Python-Dictionary). The keys and values of the data structure must follow JSON syntax rules so that the {{site.data.keyword.codeengineshort}} service can deliver the response data in the `application/json` HTTP response data section.

Backslashes (`\`) and double quotation marks (`"`) in the data structure are delivered in text-encoded format in the HTTP response data section.
{: note}

Python example of an `application/json` response:

```javascript
  import os
  def main(args):
    # python dictionary
    result_body = { "key_1" : "myfolder\myFile" }

    return {
      "headers": {
        "Content-Type": "application/json",
      },
      "statusCode": 200,
      "body": result_body,
    }
```
{: screen}

Node.js example of an `application/json` response:

```javascript
function main(args) {
  // JSON data structure
  // Note: Backslash must be text encoded
  result_body =  { "key1" : "myfolder\\myFile"}

  return {
	  statusCode: 200,
	  headers: {
	    'Content-Type': "application/json",
	  },
	  "body" : result_body ,
  };
}
module.exports.main = main;
```
{: screen}

#### Body value of content-type `application/octet-stream`
{: #fun-body-element-application-octet-stream}

The result data for the function code must be Base64-encoded before you add it to the result structure.

Python example of an `application/octet-stream` response:

```javascript
import os
import base64

def main(args):
  result_body = "myfolder_myFile"
  enc_result_body=base64.encodebytes(result_body.encode()).decode("utf-8").strip()

  return {
    "headers": {
      "Content-Type": "application/octet-stream",
    },
    "statusCode": 200,
    "body": enc_result_body,
  }
```
{: screen}

Node.js example of an `application/octet-stream` response:
```javascript
function main(args) {
  var result_body = "###\unreturned body###\n"
  var buff = new Buffer(result_body , 'utf8');

  return {
    statusCode: 200,
    headers: {
      'Content-Type': "application/octet-stream",
    },
    "body" : buff.toString('base64') ,
  };
}

module.exports.main = main;
```
{: screen}

#### Body value of content-type `text/plain`
{: #fun-body-element-text-plain}

Function code must provide the whole response in a single string. The {{site.data.keyword.codeengineshort}} functions service does not check the response data; the data is transferred to the caller as provided.

Python example of a `text/plain` response:

```javascript
def main(args):
  result_body = "myfolder_myFile"

  return {
    "headers": {
      "Content-Type": "text/plain;charset=utf-8",
    },
    "statusCode": 200,
    "body": result_body,
  }
```
{: screen}

#### Body value of content-type `application/x-www-form-urlencoded` (percent-encoded content)
{: #fun-body-element-x-www-form-urlencoded}

Function code must help ensure that the response data is URL-encoded before it is added to the result data structure. The {{site.data.keyword.codeengineshort}} functions service does not check the response data for correct syntax. The data is transferred to the caller as provided.

Python example of an `application/x-www-form-urlencoded` response:

```javascript
import os
def main(args):
  result_body = "myfolder%20myFile"

  return {
    "headers": {
    "Content-Type": "application/x-www-form-urlencoded",
    },
    "statusCode": 200,
    "body": result_body,
  }
```
{: screen}

## External response data interface
{: #fun-external-data-interface-response}

The external data interface definition is derived from standardized HTTP. MIME types in the HTTP Response header are used to define the format of the HTTP response.

### MIME types
{: #fun-external-data-interface-response-mime}

When {{site.data.keyword.codeengineshort}} returns data to the external world, {{site.data.keyword.codeengineshort}} functions can support the same IANA MIME types as described in [MIME types](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-MIME-types).

### Response data
{: #fun-external-data-interface-response-response-data}

The external data interface returns the response data structure as HTTP header, HTTP status code, and HTTP response data to the caller of the function.

#### HTTP header fields
{: #fun-external-data-interface-response-http-header-fields}

The HTTP header contains all key-value pairs that the function code added to the result data structure.

The {{site.data.keyword.codeengineshort}} functions service adds the following key-value pairs:

| Field name           | Description |
|----------------------|-----------------------------------------------------------|
| `x-request-id`         | The external request ID for the invoked function.      |
| `x-faas-activation-id` | The {{site.data.keyword.codeengineshort}} functions service internal ID for the invocation.        |
| `x-faas-actionstatus`  | The status code the function code set.        |
{: caption="Key-value pairs in {{site.data.keyword.codeengineshort}} functions"}

Header key names are always replied in lowercase.
{: note}

#### HTTP status code
{: #fun-external-data-interface-response-http-status-code}

The origin of the HTTP status code can be the {{site.data.keyword.codeengineshort}} functions service itself or the status code set by the function code. The presence of the header field `x-faas-statuscode` is the indicator of the origin.

The meaning of the HTTP status code can be read in the {{site.data.keyword.codeengineshort}} functions documentation if the `x-faas-actionstatus` header field is not set. However, if the header field is set, then the logic of the function defines the meaning of the HTTP status code.

{{site.data.keyword.codeengineshort}} functions service runs a limited validity check on the response data and content-type, and returns an HTTP status code of `400` if the data format or encoding (generated by the function code) is invalid.
{: note}

#### HTTP response data
{: #fun-external-data-interface-response-http-response-data}

The HTTP response data on the external data interface are identical as supplied in the result data structure by the function code. Only if the `MIME-Type` is `application/json` then the key and values in the provided JSON response are modified. All backslashes and double quotation marks are escaped.

For example, the caller gets `application/json` response data. The function code that provides the response data is as follows:

```javascript
import os
def main(args):
  # python dictionary
  result_body = { "key_1" : "myfolder\myFile" }

  return {
    "headers": {
      "Content-Type": "application/json",
      "key" : "sample",
    },
    "statusCode": 200,
    "body": result_body,
  }
```
{: screen}

The `curl` client that uses the response `statusCcode`, the `header` fields, and the response data, is as follows:

```javascript
  curl -v -i  https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/
	 -> Response:
	stdout>
   * Host default-encoded-response.1lpigeajq5fg.us-east.codeengine.appdomain.cloud:443 was resolved.
   * IPv6: 2606:4700:90:0:7554:9304:2cbe:8cbf
   * IPv4: 172.65.197.223
   * using HTTP/1.x
   > GET / HTTP/1.1
   > Host: default-encoded-response.1lpigeajq5fg.us-east.codeengine.appdomain.cloud
   > User-Agent: curl/8.8.0
   > Accept: *//*

   * Request completely sent off
   < HTTP/1.1 200 OK
   < content-type: application/json
   < key: sample
   < x-faas-actionstatus: 200
   < x-faas-activation-id: 5cbab12c-5c6e-4000-96cf-0f7fcb42a979
   < x-request-id: e7098271-4780-4893-bbd4-64d4c8d7605e
   < content-length: 13
   { "key_1" : "myfolder\\myFile }* Connection
 ```
 {: screen}

## {{site.data.keyword.codeengineshort}} function invocation examples
{: #fun-invocation-examples}

Follow these steps to see the creation of a {{site.data.keyword.codeengineshort}} function with the CLI and the usage of the external data interface:

 1. Save the following code as `hello.js` locally:
    ```javascript
    function main(args) {
      return { headers: { content_type: "application/json" },
        statusCode: 200,
        body: {args: args}
      };
    }
    ```
    {: screen}

 2. After you log on to {{site.data.keyword.Bluemix}} and selecting the {{site.data.keyword.codeengineshort}} functions service, create a new function:

    ```javascript
    ibmcloud ce fn create --name sample --runtime nodejs --inline-code sample.js --cpu 0.5 --memory 2G
    ```
    {: screen}

    Example output:

    ```javascript
    Creating function 'sample'...
    OK
    Run 'ibmcloud ce function get -n sample' to see more details.

    ibmcloud ce function get -n sample

    Getting function 'sample'...
    OK

    Name:    sample
    ...
    Status:  Ready
    URL:     https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ...
    ```
    {: screen}

 3. Use the external data interface with a `curl` command to invoke the function:

    ```javascript
    curl -v https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_headers": {
            "Accept": "*/*",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "813804ec-ef14-42e9-bce3-c162373defae"
            },
            "__ce_method": "GET",
            "__ce_path": "/"
        }
    }
    ```
    {: screen}

 4. Invoke the function by using query parameters:

    ```javascript
    curl -v "https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/?planet1=Mars&planet2=Jupiter"
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_headers": {
            "Accept": "*/*",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "d03a1af0-bfc8-4a50-be7d-a72040c02cc9"
            },
            "__ce_method": "GET",
            "__ce_path": "/",
            "__ce_query": "planet1=Mars&planet2=Jupiter",
            "planet1": "Mars",
            "planet2": "Jupiter"
        }
    }
    ```
    {: screen}

    The query parameter is available unfolded in the arguments and also unmodified in `__ce_query`.

 5. Invoke the function by using form data:

    ```javascript
    curl -H "Content-Type: application/x-www-form-urlencoded" -d 'planet1=Mars&planet2=Jupiter' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_body": "planet1=Mars&planet2=Jupiter",
            "__ce_headers": {
            "Accept": "*/*",
            "Content-Length": "28",
            "Content-Type": "application/x-www-form-urlencoded",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "eb3e2179-c396-4eee-98cb-809316f0a765"
            },
            "__ce_method": "POST",
            "__ce_path": "/"
        }
    }
    ```
    {: screen}

    The content of the request body is available unmodified in the `__ce_body` argument with JSON-reserved characters that are being escaped.

 6. Invoke the function by using a JSON data object:

    ```javascript
    curl -H "Content-Type: application/json" -d '{"planet1": "Mars", "planet2": "Jupiter"}' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_body": "eyJwbGFuZXQxIjogIk1hcnMiLCAicGxhbmV0MiI6ICJKdXBpdGVyIn0=",
            "__ce_headers": {
            "Accept": "*/*",
            "Content-Length": "41",
            "Content-Type": "application/json",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "c06ffcc3-fdae-4430-b881-01d68876c54c"
            },
            "__ce_method": "POST",
            "__ce_path": "/",
            "planet1": "Mars",
            "planet2": "Jupiter"
        }
    }
    ```
    {: screen}

    The content of the request body is available unfolded into the function arguments (`args`) with JSON reserved characters that are being escaped and also unmodified as a Base64-encoded string in `__ce_body`.

 7. Invoke the function by using JSON data and query parameters:

    ```javascript
    curl -H "Content-Type: application/json" -d '{"planet1": "Mars", "planet2": "Jupiter"}' "https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud?planet2=Venus&planet3=Uranus"
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
        "__ce_body": "eyJwbGFuZXQxIjogIk1hcnMiLCAicGxhbmV0MiI6ICJKdXBpdGVyIn0=",
            "__ce_headers": {
            "Accept": "*/*",
            "Content-Length": "41",
            "Content-Type": "application/json",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "daff83a5-fe53-43ef-8dc4-606e42dd8306"
            },
            "__ce_method": "POST",
            "__ce_path": "/",
            "planet1": "Mars",
            "planet2": "Jupiter",
            "planet3": "Uranus"
        }
    }
    ```
    {: screen}

    The body parameters and query parameters are unfolded into the function arguments (`args`). Body parameters overwrite the query parameters. The request body is available in `__ce_body` (Base64-encoded). The query parameters are available in `__ce_query`.

 8. Invoke the function by using text content type:

    ```javascript
    curl -H "Content-Type: text/plain" -d 'Here we have some text. The JSON special characters like \ or " are escaped.' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_body": "Here we have some text. The JSON special characters like \\ or \ are escaped.",
            "__ce_headers": {
            "Accept": "*/*",
            "Content-Length": "76",
            "Content-Type": "text/plain",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "43d259eb-4247-41a9-894a-1dbd98eb16fb"
            },
            "__ce_method": "POST",
            "__ce_path": "/"
        }
    }
    ```
    {: screen}

    The content of the request body is available unmodified in `__ce_body`, but with JSON special characters escaped with `\\` or `\`.

 9. Invoke the function by using binary content type:

    ```javascript
    curl -H "Content-Type: application/octet-stream" -d 'This string is treaded as binary data.' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ```
    {: screen}

    Example output:

    ```javascript
    {
        "args": {
            "__ce_body": "VGhpcyBzdHJpbmcgaXMgdHJlYWRlZCBhcyBiaW5hcnkgZGF0YS4=",
            "__ce_headers": {
            "Accept": "*/*",
            "Content-Length": "38",
            "Content-Type": "application/octet-stream",
            "User-Agent": "curl/7.58.0",
            "X-Request-Id": "a90826e0-db13-4b8a-809f-60cea2a27d96"
            },
            "__ce_method": "POST",
            "__ce_path": "/"
        }
    }
    ```
    {: screen}
