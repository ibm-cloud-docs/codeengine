---

copyright:
  years: 2024
lastupdated: "2024-10-16"

keywords: code engine, functions, stateless code snippet, code snippet, stateless

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# Exchanging data with functions
{: #fun-exchanging-data}

Invoking a {{site.data.keyword.codeengineshort}} function is accomplished on the client side through HTTP requests through an external HTTP interface. Information can be passed to a function:

* as part of the URL (path and optionally, query parameters)
* through request headers
* through the request body

The following diagram shows information flow from an external (caller) data interface, to the {{site.data.keyword.codeengineshort}} function controller. An internal (function) request and response data interface for processing, and then return back to the external caller:

![Functions interfaces.](images/ce_functions_interfaces.svg "Functions interfaces"){: caption="External (caller) data interface and internal (function) data interface" caption-side="bottom"}

This flow depicts a client (caller) information that enters from an external data interface. The {{site.data.keyword.codeengineshort}} function controller then wraps the information. Finally, it passes the information to the function as part of the function's call parameters by using an internal request data interface. The function can then process, and when complete, it provides response data such as an HTTP status code, response headers, and a response body through that internal response data interface. The {{site.data.keyword.codeengineshort}} function controller unwraps the response data from the function, and then returns the data to the client in the HTTP response through the external data interface.

In the external data interface request and response body, the caller or the function can choose to exchange unstructured text or binary messages, or structured content.

## External data interface
{: #fun-external-data-interface}

Depending on the request or response content types, appropriate elements of the JSON input or output messages are used to exchange data with the external world.

### MIME types
{: #fun-external-data-interface-MIME-types}

The following IANA MIME types are supported for the content-type of an {{site.data.keyword.codeengineshort}} function request or response. Options are supported, but not included in this list:

* JSON type: `application/json; ...`
* Binary types:
    * `audio/...; ...`
    * `application/octet-stream; ...`
    * `example/...; ...`
    * `font/...; ...`
    * `image/...; ...`
    * `model/...; ...`
    * `multipart/...; ...`
    * `video/...; ...`
* Text types:
    * `text/plain; ...`
    * `text/html; ...`
    * `text/...; ...`
* Percent-encoded type: `application/x-www-form-urlencoded; ...`

### Function request data encoding
{: #fun-external-data-interface-function-request-data-encoding}

When a function is invoked, it can receive arbitrary data (request payload) in text or binary form. The presence of a `Content-Type` request header determines the form and encoding of the data that is sent to the function. The data structure and format, and the content type, must match. {{site.data.keyword.codeengineshort}} runs a minimal validity check on the data and content type, and responds with HTTP status code `400` if data format or encoding is invalid.

Depending on the value of `Content-Type`, the function receives input data:

#### JSON content
{: #function-request-data-encoding-json}

The function receives the keys and values of the JSON document as dedicated parameters.

In addition, the JSON payload is made available to the function as-is (byte array) by using the `__ce_body` parameter, but in Base64-encoded form.

Example JSON content:

```javascript
        import os

        def main(args):
            return {
                "headers": {
                    "Content-Type": "text/plain",
                },

                "statusCode": 200,
                "body": {"name":"value", "number": 0, "boolvalue":True, "struct": {"inner": ["value1","value2"] } },
            }
```
{: screen}

#### Percent-encoded content
{: #function-request-data-encoding-percent-encoded}

Percent-encoding is widely used in web technology. All 8-bit characters are written as hexadecimal value preceded by a percentage sign (%). This type of encoding is also known as URL-encoding. The payload is made available to the function as-is (byte array) by using the `__ce_body` parameter, whereas the percent-encoded values are unaltered and therefore the function code requires decoding them.

Example percent-encoded content:

```javascript
    import os

    def main(args):
        return {
            "headers": {
                "Content-Type": "application/x-www-form-urlencoded",
            },

            "statusCode": 200,
            "body": "returned%20url-encoded%20body",
        }
```
{: screen}

#### Text content
{: #function-request-data-encoding-text}

The text payload is made available to the function as-is (byte array) by using the `__ce_body` parameter. The caller can send an arbitrary sequence of 7-bit or 8-bit characters as the request payload. As the input to the function code is a JSON formatted data structure, some characters are escaped to make them compatible to JSON. {{site.data.keyword.codeengineshort}} runs this escaping before it forwards the request payload to the function. The function's program logic might need to unescape them to re-create the original data.

Supported escape characters:

* Backspace is replaced with `\b`.
* Form feed is replaced with `\f`.
* Newline is replaced with `\n`.
* Carriage return is replaced with `\r`.
* Tab is replaced with `\t`.
* Double quotation marks are replaced with `\"`.
* Backslash is replaced with `\\`.

Example text content, with correctly escaped response characters in Python:

```javascript
    import os

    def main(args):
        return {
            "headers": {
                "Content-Type": "text/plain",
            },

            "statusCode": 200,
            "body": "###\n\nreturned text body\n\n###\n",
        }
```
{: screen}

#### Binary content
{: #function-request-data-encoding-binary}

Data payload is made available to the function as-is (byte array) by using the `__ce_body` parameter, but in Base64-encoded form.

Example binary content:

```javascript
    import os
    import base64

    def main(args):
        responseBody="###\n\nreturned body\n\n###\n"
        encodedResponse=base64.encodebytes(responseBody.encode()).decode("utf-8").strip()
        return {
            "headers": {
                "Content-Type": "application/octet-stream",
            },

            "statusCode": 200,
            "body": encodedResponse,
        }
```
{: screen}

#### If the function request `Content-Type` is missing
{: #function-request-data-encoding-missing-content-type}

If `Content-Type` is missing for a request, then {{site.data.keyword.codeengineshort}} handles the data payload as described for `application/json`.

### Function response data encoding
{: #fun-external-data-interface-function-response-data-encoding}

A function can return arbitrary data in text or binary form, whereas the presence of a `Content-Type` response header determines the form and encoding of the data returned.

{{site.data.keyword.codeengineshort}} runs a limited validity check on the response data and content type, and returns an HTTP status code `400` if the data format or encoding (generated by the function code) is invalid.

When {{site.data.keyword.codeengineshort}} returns data to the external world, {{site.data.keyword.codeengineshort}} functions can support the same IANA MIME types as described in [MIME types](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-MIME-types)
When a caller invokes the function, the caller can send an optional `Accept-Encoding` request header that {{site.data.keyword.codeengineshort}} forwards to the function. However, it is at the discretion of the function to return the response in accordance with the accepted encoding.

The function code must set the `Content-Type` response header and format and encode the data as follows:

#### JSON content
{: #function-response-data-encoding-json}

The function sets `Content-Type` to `application/json` and returns the JSON object in the `body` field.

For an example of JSON content, see the [function request data encoding example for JSON content](/docs/codeengine?topic=codeengine-fun-exchanging-data#function-request-data-encoding-json).

#### Percent-encoded content
{: #function-response-data-encoding-percent-encoded}

The function sets `Content-Type` to `application/x-www-form-urlencoded` and returns a percent-encoded string in the `body` field.

For an example of percent-encoded content, see the [function request data encoding example for percent-encoded content](/docs/codeengine?topic=codeengine-fun-exchanging-data#function-request-data-encoding-percent-encoded).

#### Text content
{: #function-response-data-encoding-percent-text}

The function sets `Content-Type` to one of the text types (for example, `text/plain`) and returns the character string in the `body` field.

For an example of text content, see the [function request data encoding example for text content](/docs/codeengine?topic=codeengine-fun-exchanging-data#function-request-data-encoding-text).

#### Binary content
{: #function-response-data-encoding-binary}

The function sets `Content-Type` to one of the binary types (for example, `application/octet-stream`) and encodes the data to a Base64 string, and returns the string in the `body` field. JSON-reserved characters need to be escaped.

For an example of binary content, see the [function request data encoding example for binary content](/docs/codeengine?topic=codeengine-fun-exchanging-data#function-request-data-encoding-binary).

#### If the function response `Content-Type` is missing
{: #function-response-data-encoding-percent-missing-content-type}

The function code can opt to omit a response `Content-Type`, in which case {{site.data.keyword.codeengineshort}} returns `Content-Type: text/plain; charset=utf-8` at the external interface, and the data from the `body` field in its unaltered form.

## Internal data interface
{: #fun-internal-data-interface}

### {{site.data.keyword.codeengineshort}} function entry
{: #fun-function-entry}

In general, the main method of a {{site.data.keyword.codeengineshort}} function exchanges data with the caller by using a JSON-formatted message structure (function input or output messages). The message content is independent of the chosen runtime ([Node.js or Python](/docs/codeengine?topic=codeengine-fun-runtime), and is handed over to the function's main method by using a single parameter. The type of parameter depends on the runtime: it is a JSON object for Node.js and of `dict` type for Python.

Example of a function JSON input structure:

```javascript
{
    "__ce_headers": {
      "Accept": "*/*",
      "Content-Length": "14",
      "Content-Type": "application/json",
      "X-Request-Id": "e83112cb-0468-488f-a795-ca9a4319fc07"
      ...
    },
    "__ce_method": "POST",
    "__ce_path": "/",
    "body": ...
    "argument1": ...
}
```
{: screen}

The following HTTP parameters can be found in a {{site.data.keyword.codeengineshort}} function's input arguments:

| HTTP parameter | Type | Description |
|----------------|------|-------------|
| `__ce_method` | String | The HTTP method of the request.|
| `__ce_headers` | Map string to string | The request headers as provided in the incoming HTTP request. |
| `__ce_path` | String | The path of the HTTP request.|
| `__ce_body` | String | The request body entity, as a Base64-encoded string when request content type is binary, or as a plain string, otherwise.|
| `__ce_query` | String | The query parameters from the request as an unparsed string. The `__ce_query` parameter is a single string that contains the query parameters that are parsed from the URL, without the leading question mark (?), and separated by an ampersand (&).|
{: caption="HTTP parameters in a {{site.data.keyword.codeengineshort}} function's input arguments"}

A request cannot override any of the named `__ce_` parameters. Doing so results in a failed request with status equal to `400 Bad Request`.

For HTTP requests with `Content-Type` of `application/json` or `application/x-www-form-urlencoded`, the data is also available in the function arguments as top-level properties.

For HTTP requests with URL query parameters, the query parameters are available as priority in the function's argument. Body parameters take precedence over query parameters.

The request headers are transferred without modification: all character casing is retained, but JSON reserved characters are escaped.

#### {{site.data.keyword.codeengineshort}} function environment variables
{: #fun-function-envvars}

While function call parameters are derived from the incoming HTTP request, a {{site.data.keyword.codeengineshort}} function also has access to a set of predefined environment variables derived from system settings:
* `CE_ALLOW_CONCURRENT`
* `CE_API_BASE_URL`
* `CE_DOMAIN`
* `CE_EXECUTION_ENV`
* `CE_FUNCTION`
* `CE_PROJECT_ID`
* `CE_REGION`
* `CE_SUBDOMAIN`

For more information about these environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

Example of accessing environment variables from {{site.data.keyword.codeengineshort}} functions in Node.js:

```javascript
function main(args) {

  return {
      headers: { 'Content-Type': 'application/json' },
      statusCode: 200,
      body: {
        args: args,
        env: process.env
      }
  }
}

module.exports.main = main;
```
{: screen}

Example of accessing environment variables from {{site.data.keyword.codeengineshort}} functions in Python:

```javascript
import os

def main(args):
    return {
        "headers": { "Content-Type": "application/json;charset=utf-8" },
        "statusCode": 200,
        "body": {
            "env": dict(os.environ),
            "args": args
        }
    }
```
{: screen}

### {{site.data.keyword.codeengineshort}} function entry examples
{: #fun-function-entry-examples}

Follow these steps as an example of creating a {{site.data.keyword.codeengineshort}} function entry:

1. Save the following code as `hello.js`:
  ```javascript
    function main(args) {
          return { headers: { content_type: "application/json" },
              statusCode: 200,
  		          body: {args: args}
          };
    }
    ```
{: screen}

2. Create or update the function with this code:

    ```javascript
    ibmcloud ce fn create --name sample --runtime nodejs-18 --inline-code sample.js --cpu 0.5 --memory 2G
    ```
    {: codeblock}

    Example output:
    ```javascript
    Creating function 'sample'...
    OK
    Run 'ibmcloud ce function get -n sample' to see more details.

    # ibmcloud ce function get -n sample
    Getting function 'sample'...
    OK

    Name:    sample
    ...
    Status:  Ready
    URL:     https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud
    ...
    ```
    {: screen}

3. Run this simple invocation:

    ```javascript
    curl -v https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/ | jq .
    ```
    {: codeblock}

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
    curl -v "https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud/?planet1=Mars&planet2=Jupiter" | jq .
    ```
    {: codeblock}

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
    curl -H "Content-Type: application/x-www-form-urlencoded" -d 'planet1=Mars&planet2=Jupiter' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud | jq .
    ```
    {: codeblock}

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

    The content of the request body is available unmodified in the `__ce_body` argument with JSON reserved characters being escaped.

6. Invoke the function by using a JSON data object:

    ```javascript
    curl -H "Content-Type: application/json" -d '{"planet1": "Mars", "planet2": "Jupiter"}' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud | jq .
    ```
    {: codeblock}

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

    The content of the request body is available unfolded into the function arguments (`args`) with JSON reserved characters being escaped and also unmodified as a Base64-encoded string in `__ce_body`.

7. Invoke the function by using JSON data and query parameters:
    ```javascript
    curl -H "Content-Type: application/json" -d '{"planet1": "Mars", "planet2": "Jupiter"}' "https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud?planet2=Venus&planet3=Uranus" | jq .
    ```
    {: codeblock}

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

7. Invoke the function by using text content type:

    ```javascript
    curl -H "Content-Type: text/plain" -d 'Here we have some text. The JSON special characters like \ or " are escaped.' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud | jq .
    ```
    {: codeblock}

    Example output:
    ```javascript
    {
        "args": {
            "__ce_body": "Here we have some text. The JSON special characters like \\ or \" are escaped.",
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

    The content of the request body is available unmodified in `__ce_body`, but with JSON special characters escaped with `''`.

8. Invoke the function by using binary content type:

    ```javascript
    curl -H "Content-Type: application/octet-stream" -d 'This string is treaded as binary data.' https://sample.1kweru2e873.eu-gb.codeengine.appdomain.cloud | jq .
    ```
    {: codeblock}

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

#### Decoding binary body content from Base64
{: #fun-decode-binary-body-content}

You can decode a function's binary body content from Base64 as follows.

Example of decoding functions in Node.js:

```javascript
function main(args) {
    binaryRequestBody = new Buffer(args.__ce_body, 'base64').toString('utf-8')

	// The buffer binaryRequestBody now contains a copy of the request body.
	....

}
```
{: screen}

Example of decoding functions in Python:

```javascript
import base64

def main(args):
    try:
        binaryRequestBody = base64.b64decode(args['__ce_body'])
    except:
        return {
            "body": "Error decoding body from Base64.",
            "statusCode": 400
        }

	# The byte array binaryRequestBody now contains a copy of the request body.
	...
```
{: screen}

### {{site.data.keyword.codeengineshort}} function results
{: #fun-function-results}

A {{site.data.keyword.codeengineshort}} function returns a JSON object with the following top-level priorities:

| JSON property | Description |
|---------------|-------------|
| `header` | A JSON object in which the keys are header names and the values are strings, numbers, or Boolean values. To send multiple values for a single header, the header's value is a JSON array of the multiple values. No headers are set by default. |
| `statusCode` | A valid HTTP status code. If body content is present, the default is `200 OK`. If no body content is present, the default is `204 No Content`. |
| `body` | A string that is either plain text, a JSON object or array, or a Base64-encoded string for binary data. The body is considered empty if it is null, an empty string (""), or undefined. The default is an empty body. |
{: caption="JSON property results in a {{site.data.keyword.codeengineshort}} function"}

Depending on the value of `Content-Type` set in the header field of the function results, the content of the body field needs to contain the following information:

| `Content-Type` | Body value | Example |
|----------------|------------|---------|
| Empty or `application/json` | A JSON object | `body: { env: process.env }` |
| `text/*` | A text string | `body: "Some text for the response body."` |
| `audio/*`, `example/*`, `font/'`, `image/*`, `video/*`, and all remaining types | A Base64-encoded string | `body: "SGVsbG8gV29ybGQhCg=="` |
{: caption="Contents of body field for different content types in a {{site.data.keyword.codeengineshort}} function"}

The response headers in the function results are transferred without modification to the HTTP response headers: all character casing is retained, but JSON reserved characters are escaped.

Example {{site.data.keyword.codeengineshort}} function results for Node.js:

```javascript
function main(args) {
  return {
    headers: { content_type: "application/octet-stream" },
    statusCode: 200,
    body: Buffer.from([0x08, 0x71, 0x06, 0x12, 0xFF, 0xA1]).toString('base64') }
  };
```
{: screen}

Example {{site.data.keyword.codeengineshort}} function results for Python:

```javascript
import base64

def main(args):
    return {
        "headers": { "Content-Type": "application/octet-stream" },
        "statusCode": "418",
        "body": base64.encodebytes(b"\x80\xFF\x00\xaa\xc3\x42")
    }
```
{: screen}

The default content type for an HTTP response is `application/json`, and the body can be any allowed JSON value. If the content type is not `application/json`, then the function must specify the content type in the response headers of the function's result.

If the result size limit for functions is reached, an HTTP status code `400` is returned to the client.

The function specified headers, status code, and body are returned to the HTTP client, which completes the request. If the content type header is defined, the controller determines whether the response is binary data or plain text and decodes the string by using a Base64 decoder as needed. If the body is not decoded correctly, an HTTP status code `400` is returned to the client.

#### Encoding binary body content to Base64
{: #fun-encode-binary-body-content}

You can encode a function's binary body content to Base64 as follows.

Example of encoding functions in Node.js:

```javascript
function main(args) {
  return {
    headers: { content_type: "application/octet-stream" },
    statusCode: 200,
    body: Buffer.from([0x08, 0x71, 0x06, 0x12, 0xFF, 0xA1]).toString('base64')
  }
}
```
{: screen}

Example of encoding functions in Python:

```javascript
import base64

def main(args):
    return {
        "headers": { "Content-Type": "application/octet-stream" },
        "statusCode": "418",
        "body": base64.encodebytes(b"\x80\xFF\x00\xaa\xc3\x42")
    }
```
{: screen}
