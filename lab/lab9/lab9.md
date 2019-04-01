# lab 9

## Example00

```
~/b/C/l/l/d/example00 ❯❯❯ podman run docker/whalesay cowsay boo                               spring2019
Trying to pull docker.io/docker/whalesay...Getting image source signatures
Copying blob e190868d63f8 [======================================] 1.4GiB / 1.4GiB
Copying blob 909cd34c6fd7 [======================================] 1.4GiB / 1.4GiB
Copying blob 0b9bfabab7c1 [======================================] 1.4GiB / 1.4GiB
Copying blob a3ed95caeb02 [======================================] 1.4GiB / 1.4GiB
Copying blob 00bf65475aba [======================================] 1.4GiB / 1.4GiB
Copying blob c57b6bcc83e3 [======================================] 1.4GiB / 1.4GiB
Copying blob a3ed95caeb02 [======================================] 1.4GiB / 1.4GiB
Copying blob 8978f6879e2f [======================================] 1.4GiB / 1.4GiB
Copying blob 8eed3712d2cf [======================================] 1.4GiB / 1.4GiB
Copying blob a3ed95caeb02 [======================================] 1.4GiB / 1.4GiB
Writing manifest to image destination
Storing signatures
 _____
< boo >
 -----
    \
     \
      \
                    ##        .
              ## ## ##       ==
           ## ## ## ##      ===
       /""""""""""""""""___/ ===
  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
       \______ o          __/
        \    \        __/
          \____\______/
```

## example01

```
~/b/C/l/l/d/example01 ❯❯❯ podman run -it ubuntu bash

root@e1ffb7ac1e02:/# cat /etc/os-release
NAME="Ubuntu"
VERSION="18.04.2 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.2 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic
root@e1ffb7ac1e02:/#
```

The package install is the same as normal so I won't post it here

## example02

```
b/C/l/l/d/example02 ❯❯❯ docker ps                                                           spring2019
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS            >
96b96b8f1338        rocket.chat         "node main.js"           About a minute ago   Up About a minute >
3ca53e14e617        mongo:3.2           "docker-entrypoint.s…"   3 minutes ago        Up 2 minutes      >

rocketchat-desktop wont connect but netcat does, it seems to be a networking issue
~ ❯❯❯ nc 0 3000
why rocketchat
HTTP/1.1 400 Bad Request
```

## example03

```
~/b/C/l/l/d/example03 ❯❯❯ sudo podman run -p 5000:5000 8f968090cae7
 * Serving Flask app "hello.py"
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
10.88.0.1 - - [29/Mar/2019 17:49:38] "GET / HTTP/1.1" 200 -
10.88.0.1 - - [29/Mar/2019 17:49:38] "GET /favicon.ico HTTP/1.1" 404 -
```
![flask screenshot](./flask.png)

## example04

```
~ ❯❯❯ curl http://localhost:1337/message
~ ❯❯❯ curl http://localhost:1337/message
~ ❯❯❯ curl -XPOST http://localhost:1337/message?text=hello
zsh: no matches found: http://localhost:1337/message?text=hello
~ ❯❯❯ bsdh curl -XPOST http://localhost:1337/message?text=hello
~ ❯❯❯ bash
[luke@Yum-Yum]: ~>$ curl -XPOST http://localhost:1337/message?text=hello
{
  "text": "hello",
  "createdAt": 1553883175771,
  "updatedAt": 1553883175771,
  "id": "5c9e6027a605273a3aa8e190"
}[luke@Yum-Yum]: ~>$ curl -XPOST http://localhost:1337/message?text=hola
{
  "text": "hola",
  "createdAt": 1553883180375,
  "updatedAt": 1553883180375,
  "id": "5c9e602ca605276940a8e191"
}[luke@Yum-Yum]: ~>$ curl http://localhost:1337/message
[
  {
    "text": "hello",
    "createdAt": 1553883175771,
    "updatedAt": 1553883175771,
    "id": "5c9e6027a605273a3aa8e190"
  },
  {
    "text": "hola",
    "createdAt": 1553883180375,
    "updatedAt": 1553883180375,
    "id": "5c9e602ca605276940a8e191"
  }
][luke@Yum-Yum]: ~>$ curl -XPUT http://localhost:1337/message/5c9e6027a605273a3aa8e190?text=hey
{
  "text": "hey",
  "createdAt": 1553883175771,
  "updatedAt": 1553883215236,
  "id": "5c9e6027a605273a3aa8e190"
}[luke@Yum-Yum]: ~>$ curl -XDELETE http://localhost:1337/message/5c9e602ca605276940a8e191
{
  "text": "hola",
  "createdAt": 1553883180375,
  "updatedAt": 1553883180375,
  "id": "5c9e602ca605276940a8e191"
}[luke@Yum-Yum]: ~>$ curl http://localhost:1337/message
[
  {
    "text": "hey",
    "createdAt": 1553883175771,
    "updatedAt": 1553883215236,
    "id": "5c9e6027a605273a3aa8e190"
  }
  ```
