# joo-json-server

![LGTM](https://i.lgtm.fun/2ozo.png)

### Install
```
$ npm install json-server
$ npm install json-server --prefix . // 폴더 내 설정
```

### Usage
- Create a db.json file
```
$ vi db.json

{
  "posts": [
    { "id": "1", "title": "a title", "views": 100 },
    { "id": "2", "title": "another title", "views": 200 }
  ],
  "comments": [
    { "id": "1", "text": "a comment about post 1", "postId": "1" },
    { "id": "2", "text": "another comment about post 1", "postId": "1" }
  ],
  "profile": {
    "name": "typicode"
  },
  "kms": [
    { "id": "1", "name": "kim"},
    { "id": "2", "name": "hong"}
  ]
}
```


### Run
```
$ npx json-server db.json

JSON Server started on PORT :3000
Press CTRL-C to stop
Watching db.json...

( ˶ˆ ᗜ ˆ˵ )

Index:
http://localhost:3000/

Static files:
Serving ./public directory if it exists

Endpoints:
http://localhost:3000/posts
http://localhost:3000/comments
http://localhost:3000/profile

```


### FROM
- https://www.npmjs.com/package/json-server
