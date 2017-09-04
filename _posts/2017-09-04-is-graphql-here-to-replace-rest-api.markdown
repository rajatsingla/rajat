---
layout: post
title:  Isgraphqlheretoreplacerestapi
date:   2017-09-04 16:24:47 +0000
---


Let us understand graphql with an example                

Github has REST v3  api,
Example:-
`https://api.github.com/search/repositories?q=tetris`
(for fetching repositories matching some query)
It returns something like this
```
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
....
....
```
By default it returns total_count with first 30 results, What if i want only `first 9 results`, no problem github has written code for this scenario, you can pass `&per_page=9`

But if i want results sorted with number of `stars` a repo has, no problem github has handeled that, you can pass `$sort=star`

But if i want only `total_count` matching my query, or better, if i want only `total_count` matching query1 and query2 in one api call, naaah that is not handeled.

Facebook has developed graphql to address this problem. With graphql you can specify in your query the exact data and format you need and server will respond according to that. Your api will no longer be a stubborn child and will be flexible.

Example of blog api:
```
In rest api
/users/<id>
/users/<id>/posts
/users/<id>/followers

Three api endpoints all stubborn
```

```
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

![meme](http://https://ci.memecdn.com/8984160.jpg)


