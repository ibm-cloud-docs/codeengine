---

copyright:
  years: 2023, 2023
lastupdated: "2023-12-11"

keywords: code engine, function, testing funtions, local testing for functions, function code wrapper

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Testing {{site.data.keyword.codeengineshort}} functions locally
{: #fun-test-local}

{{site.data.keyword.codeenginefull}} functions are created from code snippets and so testing them locally isn't as straightforward as testing an app or job locally. One way that you can test functions locally by creating a wrapper for the code snippet and then running it locally. 
{: shortdesc}

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




