# Creare un docker gcc

## il file .c

```
#include <stdio.h>

int power (int m, int n);

int power (int base, int n) {
  int i, p;

  p = 1;
  for (i = 1; i <= n; i++)
    p = p * base;
  return p;
}

int main () {
  int i;

  for (i = 0; i < 10; ++i)
    printf("%d %d %d %d\n", i, power(2,i), power(-3,i), power(4,i));
}
```

## Doclerfile
```
FROM gcc:latest
ARG email="antonio.esposito@etik.com"
LABEL "maintainer"=$email
ENV AP /data/app
COPY . $AP/
WORKDIR $AP
RUN gcc temp.c -o temp;
CMD ["./temp"]

```
## build images
```
antonio@labnet5:~/docker/docker-c-hello$ docker build -t example/docker-c-hello:latest .
[+] Building 1.2s (10/10) FINISHED                                                                                                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                          0.0s
 => => transferring dockerfile: 200B                                                                                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/gcc:latest                                                                                                                                                 0.8s
 => [auth] library/gcc:pull token for registry-1.docker.io                                                                                                                                                    0.0s
 => [internal] load .dockerignore                                                                                                                                                                             0.0s
 => => transferring context: 2B                                                                                                                                                                               0.0s
 => [internal] load build context                                                                                                                                                                             0.0s
 => => transferring context: 253B                                                                                                                                                                             0.0s
 => CACHED [1/4] FROM docker.io/library/gcc:latest@sha256:00a29c626f3566021df4c7bb03629f672cfe47299f5c8a25d8661eaae1d8793a                                                                                    0.0s
 => [2/4] COPY . /data/app/                                                                                                                                                                                   0.0s
 => [3/4] WORKDIR /data/app                                                                                                                                                                                   0.0s
 => [4/4] RUN gcc temp.c -o temp;                                                                                                                                                                             0.2s
 => exporting to image                                                                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                                                                       0.0s
 => => writing image sha256:4c8820d856575a1ebf02f0790e263e59b633d6d7eb089ae14660ed9e5822c6ca                                                                                                                  0.0s
 => => naming to docker.io/example/docker-c-hello:latest                                                                                                                                                      0.0s

 1 warning found (use docker --debug to expand):
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 4)
antonio@labnet5:~/docker/docker-c-hello$ 
```
## run container

```
antonio@labnet5:~/docker/docker-c-hello$ docker run -it example/docker-c-hello:latest 
0 1 1 1
1 2 -3 4
2 4 9 16
3 8 -27 64
4 16 81 256
5 32 -243 1024
6 64 729 4096
7 128 -2187 16384
8 256 6561 65536
9 512 -19683 262144
antonio@labnet5:~/docker/docker-c-hello$ 

```
