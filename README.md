# docker cache invalidate repro

```
git clone https://github.com/matti/docker-invalidate-repro
cd docker-invalidate-repro
docker-compose pull
docker-compose build
```

everything should be cached, but it's not:

```
Building context
Step 1/6 : FROM alpine:3.11
 ---> e7d92cdc71fe
Step 2/6 : RUN apk add --no-cache   bash
 ---> Using cache
 ---> 015ba239eaab
Step 3/6 : WORKDIR /folder
 ---> Using cache
 ---> 268b719c447c
Step 4/6 : COPY folder .
 ---> 2d8ff607ee20
Step 5/6 : RUN ls -la
 ---> Running in 7f10127a5ea9
total 12
drwxr-xr-x    1 root     root          4096 Feb 13 13:30 .
drwxr-xr-x    1 root     root          4096 Feb 13 13:30 ..
-rw-r--r--    1 root     root             9 Feb 13 13:30 file
Removing intermediate container 7f10127a5ea9
```


try with own account:

```
export CACHE_IMAGE=user/image
export IMAGE=user/image
docker-compose build
...
```
