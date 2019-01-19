[![serverless](http://public.serverless.com/badges/v3.svg)](http://www.serverless.com)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg?style=flt-square)](https://standardjs.com)
# ⚡ Physis Serverless Basic APIS

We are using dynamodb with dynamoose setup

#### Basic implementation of JSON API endpoints for creating, reading, update and delete (CRUD) for a generic data structure called just item with the interest of making of this a boilerplate for quick starting projects based on [Serverless Framework](https://serverless.com/) focused in [AWS Lambda](https://aws.amazon.com/lambda/?nc1=h_ls).

## Features
* Includes __webpack 4 support__ for packaging and including babel transpilation.
* Yarn support (_previous versions of serverless webpack did not have well yarn support_).
* Complete supprt for __ES6+ syntax__ up to stage 2.
* Basic schema for "Item" model with [__Dynamoose__](https://github.com/automategreen/dynamoose).
* Create, Read, Update, Delete, List and Batch creation of items.
* In the case of new item data entries it includes auto id creation based on uuid/v1.
* Handlers only manages IO.
* Error parsing, logging and response to endpoint.
* API Gateway path described for every http verb included.

## Starting
```bash
$ yarn
$ export AWS_PROFILE="Your AWS credentials profile"
$ serverless deploy
```

## Adding a new Lambda Function

## 📢 Highlight
  Every handler is built inside a template strutured for reusing with the folowing parts:

  ```javascript
  export const handler = async ({ body }, context, callback) => {
    // Action invocation through promisified method
    // handleErr and to are declared below.
    const [err, result] = await to(crudItem(body))

    // Error handling
    if (err) {
    callback(null, handleErr(err))
    } else {
      // Response construction
      const response = {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(result)
      }

      console.log(` => Action logging...`)
      callback(null, response)
    }
  }

  // 🚧 Outside the handler 🚧
  // Function responsible of data manipulation (✨ Where magic happens)
  const crudItem = data => {
    const itemData = JSON.parse(data)
    // Dynamoose promisified API method for data manipulation
    return Item.crud()
  }

  // *** Error handling support in promises
  const to = promise =>
    promise
      .then(data => [null, data])
      .catch(err => [pe(err)]) // parse-error (npm module)

  const handleErr = (error, statusCode = 500) => {
    console.error(' => ERROR:', error.stack)

    return {
      statusCode,
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ error })
    }
  }
  ```


### Endpoint description

#### Basic Endpoint Structure
`GET` -> `https://[api-gateway-code].execute-api.[aws-region].amazonaws.com/[stage]/api/<api-name>

#### All the other endpoint list is TBA




## 😎 Happy Coding and Enjoy. Peace!! 🤘
