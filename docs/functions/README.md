# Cosmic JS Functions

![Cosmic JS and AWS Logos](/docs/images/cosmicjs-aws-logos.jpg)

## How it works

You can deploy Node.js functions to AWS through your Bucket Dashboard located at _Your Bucket > Settings > Functions_. AWS Lambda functions are infinitely scalable, highly cost effective ([AWS gives you 1M requests per month free](https://aws.amazon.com/lambda/pricing/)), and you never have to pay for idle server time. **You can have unlimited Functions in your Cosmic JS Bucket and the feature is 100% free to use.**

## What's required?

1. Your AWS access key and secret key. (See instructions below)
2. Node.js codebase (zip or link to git repo) that follows Lambda requirements.

### How to get your AWS access keys
Follow these steps to get your AWS access keys:
1. [Create or login](http://console.aws.amazon.com) to your Amazon Web Services Account and go to the Identity & Access Management (IAM) page.
2. Click on <b>Users</b> and then <b>Add user</b>. Enter a name in the first field to remind you this User is from Cosmic, like <code>cosmic-admin</code>. Enable <b>Programmatic access</b> by clicking the checkbox. Click <b>Next</b> to go through to the Permissions page.

3. Click on <b>Attach existing policies directly</b>. Search for and select <b>AdministratorAccess</b> then click through to <b>Next: Review</b>. Check everything looks good and click <b>Create user</b>.

4. View and copy the <b>API Key</b> & <b>Secret</b> to a temporary place. You'll need it for all of your Cosmic Function deploys.

## Required Files

### Entry file

The `index.js` file of your codebase will need to export a `handler` function and follow the format for [AWS Lambda Node.js function handling](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html). The version of Node.js deployed is `v8.10` which means you can use the [async / await pattern](https://aws.amazon.com/blogs/compute/node-js-8-10-runtime-now-available-in-aws-lambda/). Here's a simple Hello World example:

```js
// index.js
module.exports.handler = function(event, context, callback) {
  const response = {
    statusCode: 200,
    headers: {
      'Access-Control-Allow-Origin': '*' // Required for CORS support to work
    },
    body: 'Hello World ' + process.env.SOME_OPTIONAL_VAR
  }
  callback(null, response)
}
```

### Function config file

The `function.json` file includes information that Cosmic JS uses to deploy your function. Here's an example:

```json
{
  "title": "Hello World",
  "description": "Says Hello World and some custom message from env var.",
  "image_url": "https://cosmic-s3.imgix.net/ed58d700-7b2c-11e8-9d6b-252d8b978aea-SendGrid-Logo.png",
  "stage": "staging",
  "env_vars": [
    {
      "key": "SOME_OPTIONAL_VAR",
      "value": ""
    }
  ],
  "routes": [
    {
      "path": "hello-world",
      "method": "get",
      "cors": true
    }
  ]
}
```

### `function.json` Properties

| Key            | Type   | Description                                                                        |
| -------------- | ------ | ---------------------------------------------------------------------------------- |
| title          | String | Function title                                                                     |
| description    | String | Function description (HTML allowed)                                                |
| image_url      | String | Image thumbnail URL                                                                |
| stage          | String | defaults to dev                                                                    |
| repo_url       | String | Function git repo url                                                              |
| env_vars       | Array  | key / value for environment variables                                              |
| routes         | Array  | Function routes: properties include path (string), method (string) and cors (bool) |
| dynamic_routes | Bool   | Allows dynamic routes to your function. Overrides the routes property.             |

## Dynamic Routes

Your Function can serve dynamic routes, like an Express application (see the Serverless Starter). To make routes dynamic, add the `dynamic_routes` property set to `true` in your `function.json` file:

```json
{
  "title": "Dynamic Routes",
  "description": "A serverless function with dynamic routes.",
  "image_url": "https://cosmicjs.com/images/logos/serverless.svg",
  "stage": "dev",
  "dynamic_routes": true
}
```

Your index.js file will look something like this:

```js
// index.js
const serverless = require('serverless-http')
const express = require('express')
const app = express()
app.get('/:slug?', (req, res) => {
  res.json({ message: 'Your dynamic slug is ' + req.params.slug });
})

module.exports.handler = serverless(app);
```

## Install your Function
Go to *Your Bucket > Settings > Functions* to deploy a new Function. Whether you install from git repo URL or .zip file, make sure to include both `index.js` and `function.json` files in your codebase.

## Deploy your Function

After your Function is installed, follow these steps:

1. Go to Your *Bucket > Settings > Functions > Your Function*.
1. Add your AWS credentials.
1. Add any other required environment variables.
1. Click "Deploy Function".

## Examples
View these Function examples on GitHub:

- [Function Starter](https://github.com/cosmicjs/function-starter)
  - Get started with Cosmic Functions.

- [SendGrid Email](https://github.com/cosmicjs/send-email-function)
  - Send an email using SendGrid.

- [Stripe Charge](https://github.com/cosmicjs/stripe-charge-function)
  - Submit a charge to Stripe.

We hope you enjoy the new freedom you have to deploy serverless functions using Cosmic JS. If you have any questions, you can [reach out to us on Twitter](https://twitter.com/cosmic_js) and [join the community on Slack](https://cosmicjs.com/community).
