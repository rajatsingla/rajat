---
layout: post
title:  Is Graphql here to replace REST Api
date:   2017-09-04 16:24:47 +0000
---


GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data. GraphQL isn't tied to any specific database or storage engine and is instead backed by your existing code and data.

A GraphQL service is created by defining types and fields on those types, then providing functions for each field on each type.

Let us understand graphql with an example                

Github has REST v3  api,
Example:-
`https://api.github.com/search/repositories?q=tetris`
(for fetching repositories matching some query)
It returns something like this
```json
{
"total_count": 14126,
"incomplete_results": false,
"items": [
{
"id": 76954504,
"name": "react-tetris",
"full_name": "chvin/react-tetris",
"owner": {
"login": "chvin",
"id": 5383506,
"avatar_url": "https://avatars2.githubusercontent.com/u/5383506?v=4",
"gravatar_id": "",
"url": "https://api.github.com/users/chvin",


```
By default it returns total_count with first 30 results, What if i want only `first 9 results`, no problem github has written code for this scenario, you can pass `&per_page=9`

But if i want results sorted with number of `stars` a repo has, no problem github has handeled that, you can pass `$sort=star`

But if i want only `total_count` matching my query, or better, if i want only `total_count` matching query1 and query2 in one api call, naaah that is not handeled.

Facebook has developed graphql to address this problem. With graphql you can specify in your query the exact data and format you need and server will respond according to that. Your api will no longer be a stubborn child and will be flexible.

Example of blog api:
```html
In rest api
/users/<id>
/users/<id>/posts
/users/<id>/followers

Three api endpoints all stubborn
```

```python
In graphql api

query{
	User(id: 12){
		name,
		posts{
			title
		},
		followers(last: 3){
			name
		}
	}
}

One api endpoint, flexible as water
```
It will take some time to accept graphql in web development, but surely it has come to stay.
github has already introduced Graphql api v4

Did some one say `SOAP`!

![](https://ci.memecdn.com/8984160.jpg)


