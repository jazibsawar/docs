---
sidebar: auto
---

# Cosmic JS GraphQL API

Learn how to make requests to the Cosmic JS GraphQL API.

## GraphQL API

Connect to your Cosmic JS Bucket through GraphQL queries to the Cosmic JS API.

### Required Parameters

All queries require a `bucket_slug` parameter.

### Optional Parameters

For queries that return arrays, optional parameters `limit` and `skip` can be used to paginate returned data. If you have added a `read_key` to your Bucket, this will need to be included in every request.

All API requests begin from the host URL:

```
https://graphql.cosmicjs.com/v1
```


### Get All Objects

Returns Objects from a Bucket by querying by `bucket_slug`.

#### Try it

<iframe src="https://graphql.cosmicjs.com/v1?query=%7B%0A%20%20objects(bucket_slug%3A%20%22creative-agency%22%2C%20limit%3A%204)%20%7B%0A%20%20%20%20title%0A%20%20%20%20type_slug%0A%20%20%7D%0A%7D" frameborder="0" style="width: 100%; height: 470px;"></iframe>

::: tip 
To see the REST equivalent, visit [https://api.cosmicjs.com/v1/creative-agency/objects?pretty=true&limit=4](https://api.cosmicjs.com/v1/creative-agency/objects?pretty=true&limit=4)
:::

### Get Objects by Type

Returns Objects from a Bucket by querying by `bucket_slug` and `type_slug`.

#### Try it

<iframe src="https://graphql.cosmicjs.com/v1?query=%7B%0A%20%20objectsByType(bucket_slug%3A%20%22creative-agency%22%2C%20type_slug%3A%20%22team-members%22%2C%20limit%3A%204%2C%20skip%3A%202)%20%7B%0A%20%20%20%20title%0A%20%20%20%20metadata%0A%20%20%20%20type_slug%0A%20%20%7D%0A%7D" frameborder="0" style="width: 100%; height: 870px;"></iframe>

::: tip 
To see the REST equivalent, visit [https://api.cosmicjs.com/v1/creative-agency/object-type/team-members?pretty=true&limit=4&skip=2](https://api.cosmicjs.com/v1/creative-agency/object-type/team-members?pretty=true&limit=4&skip=2)
:::

### Get Single Object

Returns a single Object by querying by `bucket_slug` and `slug`.

#### Try it out

<iframe src="https://graphql.cosmicjs.com/v1?query=%7B%0A%20%20object(bucket_slug%3A%20%22creative-agency%22%2C%20slug%3A%20%22about%22)%20%7B%0A%20%20%20%20title%0A%20%20%20%20metadata%0A%20%20%7D%0A%7D" frameborder="0" style="width: 100%; height: 450px;"></iframe>

::: tip 
To see the REST equivalent, visit [https://api.cosmicjs.com/v1/creative-agency/object/about?pretty=true](https://api.cosmicjs.com/v1/creative-agency/object/about?pretty=true)
:::

### Examples

These examples get content from the [Creative Agency app](https://api.cosmicjs.com/apps/creative-agency).

#### CURL

Get all the Objects in the [Creative Agency app](/apps/creative-agency). Run the following in your command line app:

```bash
curl -XPOST -H "Content-Type:application/graphql"  -d 'query { objects(bucket_slug: "creative-agency") { title, metadata } }' https://graphql.cosmicjs.com/v1
```

#### AJAX

Get one object from the [Creative Agency app](/apps/creative-agency).

<iframe width="100%" height="650" src="//jsfiddle.net/WQXXT/4476/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>