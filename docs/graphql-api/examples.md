# Examples

## Node.js

The following example will get 2 Blog Posts from the Bucket Simple React Blog.

1. Install [`axios`](https://www.npmjs.com/package/axios)

```bash
npm install axios
```

2. Add the following code to a file titled `index.js`

```javascript
// index.js
const axios = require('axios')
axios.post('https://graphql.cosmicjs.com/v1', {
  query: `{ 
    getObjects(
      bucket_slug: "simple-react-blog",
      input: { type: "posts", limit: 2 }
    ){
      title
    }
  }`
})
.then(function (response) {
  const objects = response.data.data.getObjects
  console.log(objects)
})
.catch(function (error) {
  console.log(error)
});
```

3. Run the following command

```bash
node index.js
```

## Apollo
You can use [Apollo Client](https://github.com/apollographql/apollo-client) to connect to the Cosmic JS GraphQL API. You will need to use a browser build system as noted on the [Apollo Client README](https://github.com/apollographql/apollo-client/blob/master/README.md#installation).
1. Install Apollo packages
```bash
npm install apollo-boost graphql
```
2. Create a file titled `index.js` and add the following example code:
```javascript
// index.js
import ApolloClient from "apollo-boost";
const client = new ApolloClient({
  uri: "https://graphql.cosmicjs.com/v1"
});

import { gql } from "apollo-boost";

client
  .query({
    query: gql`
      {
        getObjects(
          bucket_slug: "simple-react-blog",
          input: { type: "posts", limit: 2 }
        ){
          title
          content
        }
      }
    `
  })
  .then(result => {
    console.log(result)
    document.getElementById('root').innerHTML = JSON.stringify(result.data.getObjects);
  });
```
3. Install [`webpack-cli`](https://www.npmjs.com/package/webpack-cli)
```bash
npm i -g webpack-cli
```
4. Create a file titled `webpack.config.js`
```javascript
// webpack.config.js
const path = require('path');
module.exports = {
  entry: './index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};
```
5. Create an HTML file titled `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Cosmic JS GraphQL Apollo Example</title>
</head>
<body>
  <div id="root"></div>
  <script src="dist/bundle.js"></script>
</body>
</html>
```
6. Run webpack
```
webpack
```
7. View the `index.html` file in a browser.


## Ajax

Get one Object using client-side AJAX method.

<iframe width="100%" height="550" src="//jsfiddle.net/3kuy6s9f/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
