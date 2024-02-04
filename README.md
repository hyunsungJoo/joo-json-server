# joo-json-server

![LGTM](https://i.lgtm.fun/2ozo.png)

### Install
```
$ npm install json-server
$ npm install json-server --prefix . // 폴더 내 설정
```

### Usage
- Create a db.json file($ vi db.json)
```
cat db.json

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



# Fly.io
1. branch 및 pr 생성 0.1.0/fly
2. Dockerfile 생성($ vi Dockerfile) 
```
$ cat Dockerfile

FROM node:20.11

WORKDIR /app

RUN npm install -g npm

RUN npm install -g json-server

COPY ./db.json /app

CMD ["json-server", "-p", "80", "-w", "/app/db.json"]

```
3. https://fly.io/ 가입 - (주의! hobby plan 가입)
4. 무료 플랜 : https://fly.io/docs/about/pricing/#free-allowances
5. install cmd - https://fly.io/docs/hands-on/install-flyctl/
```
sudo curl -L https://fly.io/install.sh | sh
```

6. vi ~/.zshrc 밑에 내용 추가
```
# fly
export FLYCTL_INSTALL="~/.fly"export PATH="$FLYCTL_INSTALL/bin:$PATH"
```

7. 확인
```
$ tail -n 3 ~/.zshrc
# fly
export FLYCTL_INSTALL="~/.fly"
export PATH="$FLYCTL_INSTALL/bin:$PATH"

$ source ~/.zshrc
$ flyctl auth login
```

8. Setting(fly.toml 수정)
```
$ cat fly.toml

# fly.toml app configuration file generated for joo-json-server on 2024-02-04T12:53:39+09:00
#
# See https://fly.io/docs/reference/configuration/ for information about how to use this file.
#

app = 'joo-json-server'
primary_region = 'nrt'

[build]

[http_service]
  internal_port = 80
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 3
  processes = ['app']

[[vm]]
  cpu_kind = 'shared'
  cpus = 1
  memory_mb = 256

```

8. Launch
```
$ flyctl launch

⚠️ Do you want to tweak these settings before proceeding? Yes
```
![image](https://github.com/hyunsungJoo/joo-json-server/assets/91647614/04d79465-958e-419a-a283-c1ecf74dc803)

9. Setting(fly.toml 수정)
```
$ cat fly.toml

# fly.toml app configuration file generated for joo-json-server on 2024-02-04T12:53:39+09:00
#
# See https://fly.io/docs/reference/configuration/ for information about how to use this file.
#

app = 'joo-json-server'
primary_region = 'nrt'

[build]

[http_service]
  internal_port = 80
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 3
  processes = ['app']

[[vm]]
  cpu_kind = 'shared'
  cpus = 1
  memory_mb = 256

```

10. Deploy
```
$ flyctl deploy
```
 

