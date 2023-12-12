---

copyright:
  years: 2023, 2023
lastupdated: "2023-12-12"

keywords: code engine, function, testing funtions, local testing for functions, function code wrapper

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Testing {{site.data.keyword.codeengineshort}} functions locally
{: #fun-test-local}

{{site.data.keyword.codeenginefull}} functions are created from code snippets and so testing them locally isn't as straightforward as testing an app or job locally. One way that you can test functions locally by creating a wrapper for the code snippet and then running it locally. 
{: shortdesc}

To test your code with a wrapper, follow these general steps.

1. Create a directory called `test-local`.
2. Create a subdirectory called `func`.
3. Copy your function code into the `func` subdirectory.
4. Copy either the Python or Node.js wrapper code into the parent directory. 
5. Create a configuration file as JSON objects, similar to what is passed to by Code Engine to the [function when it is invoked](/docs/codeengine?topic=codeengine-fun-work#functions-data).
6. Run the wrapper code with the configuration file as a parameter.

You can use the following wrappers or create your own.

## Python wrapper
{: #fun-test-python}

```python
# syntax: python wrapper.py params.json

# import the Code Engine function: func/__main__.py
from func.__main__ import main
import sys, json

if __name__ == "__main__":
    # open file, read JSON config
    with open(str(sys.argv[1])) as confFile:
        params=json.load(confFile)
    # invoke the CE function and print the result
    print(main(params))
```
{: pre}

## Node.js wrapper
{: #fun-test-nodejs}

```nodejs
// syntax: node wrapper.js params.json

// require the Code Engine function: func/main.js
var func=require('./func/main.js')

// read the file with function parameters
const fs = require("fs");
const data = fs.readFileSync(process.argv[2]);

// invoke the CE function and log the result
console.log(func.main(JSON.parse(data)));
```
{: pre}




