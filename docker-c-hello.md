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

## docker login
```
antonio@labnet5:~/docker/docker-c-hello$ docker login 
Authenticating with existing credentials... [Username: antonioesposito1]

i Info → To login with a different account, run 'docker logout' followed by 'docker login'


Login Succeeded
antonio@labnet5:~/docker/docker-c-hello$
```

## Pubblichiamo l'immagine

```
antonio@labnet5:~/docker/docker-c-hello$ docker image tag example/docker-c-hello:latest docker.io/antonioesposito1/docker-c-hello:latest
antonio@labnet5:~/docker/docker-c-hello$ 
```

```
antonio@labnet5:~/docker/docker-c-hello$ docker image build -t docker.io/antonioesposito1/docker-c-hello:latest .
[+] Building 0.9s (10/10) FINISHED                                                                                                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                          0.0s
 => => transferring dockerfile: 200B                                                                                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/gcc:latest                                                                                                                                                 0.8s
 => [auth] library/gcc:pull token for registry-1.docker.io                                                                                                                                                    0.0s
 => [internal] load .dockerignore                                                                                                                                                                             0.0s
 => => transferring context: 2B                                                                                                                                                                               0.0s
 => [internal] load build context                                                                                                                                                                             0.0s
 => => transferring context: 377B                                                                                                                                                                             0.0s
 => [1/4] FROM docker.io/library/gcc:latest@sha256:00a29c626f3566021df4c7bb03629f672cfe47299f5c8a25d8661eaae1d8793a                                                                                           0.0s
 => CACHED [2/4] COPY . /data/app/                                                                                                                                                                            0.0s
 => CACHED [3/4] WORKDIR /data/app                                                                                                                                                                            0.0s
 => CACHED [4/4] RUN gcc temp.c -o temp;                                                                                                                                                                      0.0s
 => exporting to image                                                                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                                                                       0.0s
 => => writing image sha256:4c8820d856575a1ebf02f0790e263e59b633d6d7eb089ae14660ed9e5822c6ca                                                                                                                  0.0s
 => => naming to docker.io/antonioesposito1/docker-c-hello:latest                                                                                                                                             0.0s

 1 warning found (use docker --debug to expand):
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 4)
antonio@labnet5:~/docker/docker-c-hello$ 
```

```
antonio@labnet5:~/docker/docker-c-hello$ docker image ls 
REPOSITORY                        TAG       IMAGE ID       CREATED             SIZE
antonioesposito1/docker-c-hello   latest    4c8820d85657   About an hour ago   1.54GB
example/docker-c-hello            latest    4c8820d85657   About an hour ago   1.54GB
<none>                            <none>    200a9a795056   2 hours ago         1.54GB
<none>                            <none>    2924c4cc61cb   2 hours ago         1.54GB
example/docker-node-hello         latest    52f273faacd7   5 days ago          1.02GB
alpine                            latest    9234e8fb04c4   2 months ago        8.31MB
<none>                            <none>    0dccf5ee8cd6   18 months ago       1.02GB
antonio@labnet5:~/docker/docker-c-hello$ 

```


```
antonio@labnet5:~/docker/docker-c-hello$ docker image push antonioesposito1/docker-c-hello:latest
The push refers to repository [docker.io/antonioesposito1/docker-c-hello]
71cde1629419: Pushed 
5f70bf18a086: Mounted from antonioesposito1/docker-node-hello 
084dbd300a0d: Pushed 
938f3fec0aa1: Mounted from library/gcc 
0f13bd1c281f: Mounted from library/gcc 
cd9afcfdbf90: Mounted from library/gcc 
a6d5b81d8677: Mounted from library/gcc 
25bde18331a6: Mounted from library/gcc 
698d92e1248d: Mounted from library/gcc 
1260506aec83: Mounted from library/gcc 
a5ec5ec9d16c: Mounted from library/gcc 
latest: digest: sha256:85da5f5f11d8f8ba7e3374ab9a952ed14fc4eba72b795ff12b19060f7a9858b7 size: 2628
antonio@labnet5:~/docker/docker-c-hello$ 
```

<img width="1650" height="283" alt="image" src="https://github.com/user-attachments/assets/d23e73f4-8cac-4751-9a07-1a953c0a0281" />

## Scarichiamo l'immagine dal registro

Ora la mia immagine è pronta per essere scaricata dal registro, ovviamente se lo faccio dallo stesso computer la cosa non avrà efetto visto che io ho già questa immagine presente nel mio elenco
```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker pull antonioesposito1/docker-c-hello:latest
latest: Pulling from antonioesposito1/docker-c-hello
Digest: sha256:85da5f5f11d8f8ba7e3374ab9a952ed14fc4eba72b795ff12b19060f7a9858b7
Status: Image is up to date for antonioesposito1/docker-c-hello:latest
docker.io/antonioesposito1/docker-c-hello:latest
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ ls
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image sl
docker: unknown command: docker image sl

Usage:  docker image

Run 'docker image --help' for more information
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                        TAG       IMAGE ID       CREATED             SIZE
antonioesposito1/docker-c-hello   latest    4c8820d85657   About an hour ago   1.54GB
example/docker-c-hello            latest    4c8820d85657   About an hour ago   1.54GB
<none>                            <none>    200a9a795056   2 hours ago         1.54GB
<none>                            <none>    2924c4cc61cb   2 hours ago         1.54GB
example/docker-node-hello         latest    52f273faacd7   5 days ago          1.02GB
alpine                            latest    9234e8fb04c4   2 months ago        8.31MB
<none>                            <none>    0dccf5ee8cd6   18 months ago       1.02GB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 


```
Per fare un test cancelliamo l'immagine

```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm example/docker-c-hello
Untagged: example/docker-c-hello:latest
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                        TAG       IMAGE ID       CREATED             SIZE
antonioesposito1/docker-c-hello   latest    4c8820d85657   About an hour ago   1.54GB
<none>                            <none>    200a9a795056   2 hours ago         1.54GB
<none>                            <none>    2924c4cc61cb   2 hours ago         1.54GB
example/docker-node-hello         latest    52f273faacd7   5 days ago          1.02GB
alpine                            latest    9234e8fb04c4   2 months ago        8.31MB
<none>                            <none>    0dccf5ee8cd6   18 months ago       1.02GB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$

antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm antonioesposito1/docker-c-hello
Error response from daemon: conflict: unable to remove repository reference "antonioesposito1/docker-c-hello" (must force) - container 8336d7ba6aaa is using its referenced image 4c8820d85657
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$

```



```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker ps -as
CONTAINER ID   IMAGE          COMMAND    CREATED             STATUS                         PORTS     NAMES               SIZE
8336d7ba6aaa   4c8820d85657   "./temp"   About an hour ago   Exited (0) About an hour ago             tender_easley       0B (virtual 1.54GB)
bb6ddc5711de   200a9a795056   "./temp"   2 hours ago         Exited (0) 2 hours ago                   nifty_johnson       0B (virtual 1.54GB)
61afc00c4727   2924c4cc61cb   "./temp"   2 hours ago         Exited (0) 2 hours ago                   objective_chaum     0B (virtual 1.54GB)
1bf4ca051a91   2924c4cc61cb   "./temp"   2 hours ago         Exited (0) 2 hours ago                   silly_lamport       0B (virtual 1.54GB)
8e69e9fc644b   2924c4cc61cb   "./temp"   2 hours ago         Exited (0) 2 hours ago                   exciting_bhaskara   0B (virtual 1.54GB)
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm antonioesposito1/docker-c-hello:latest 
Error response from daemon: conflict: unable to remove repository reference "antonioesposito1/docker-c-hello:latest" (must force) - container 8336d7ba6aaa is using its referenced image 4c8820d85657
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker rm 8336d7ba6aaa
8336d7ba6aaa
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker ps -as
CONTAINER ID   IMAGE          COMMAND    CREATED       STATUS                   PORTS     NAMES               SIZE
bb6ddc5711de   200a9a795056   "./temp"   2 hours ago   Exited (0) 2 hours ago             nifty_johnson       0B (virtual 1.54GB)
61afc00c4727   2924c4cc61cb   "./temp"   2 hours ago   Exited (0) 2 hours ago             objective_chaum     0B (virtual 1.54GB)
1bf4ca051a91   2924c4cc61cb   "./temp"   2 hours ago   Exited (0) 2 hours ago             silly_lamport       0B (virtual 1.54GB)
8e69e9fc644b   2924c4cc61cb   "./temp"   2 hours ago   Exited (0) 2 hours ago             exciting_bhaskara   0B (virtual 1.54GB)
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 


```


```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                  TAG       IMAGE ID       CREATED         SIZE
<none>                      <none>    200a9a795056   2 hours ago     1.54GB
<none>                      <none>    2924c4cc61cb   2 hours ago     1.54GB
example/docker-node-hello   latest    52f273faacd7   5 days ago      1.02GB
alpine                      latest    9234e8fb04c4   2 months ago    8.31MB
<none>                      <none>    0dccf5ee8cd6   18 months ago   1.02GB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 200a9a795056
Error response from daemon: conflict: unable to delete 200a9a795056 (must be forced) - image is being used by stopped container bb6ddc5711de
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker con
config     (Manage Swarm configs)  container  (Manage containers)     context    (Manage contexts)       
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker cont
container  (Manage containers)  context    (Manage contexts)    
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker container rm bb6ddc5711de
bb6ddc5711de
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 



```


```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 200a9a795056
Deleted: sha256:200a9a795056a55f66f948c43ba3e0d4821654de8e255409c3d06777a5883398
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 2924c4cc61cb
Error response from daemon: conflict: unable to delete 2924c4cc61cb (must be forced) - image is being used by stopped container 8e69e9fc644b
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker container rm 8e69e9fc644b
8e69e9fc644b
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 2924c4cc61cb
Error response from daemon: conflict: unable to delete 2924c4cc61cb (must be forced) - image is being used by stopped container 1bf4ca051a91
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker container rm 1bf4ca051a91
1bf4ca051a91
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 2924c4cc61cb
Error response from daemon: conflict: unable to delete 2924c4cc61cb (must be forced) - image is being used by stopped container 61afc00c4727
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker container rm 61afc00c4727
61afc00c4727
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 2924c4cc61cb
Deleted: sha256:2924c4cc61cb87f6f8730a105e8c3bc692fb8f38f2d784d82e191cd67650dbec
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 


```
```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                  TAG       IMAGE ID       CREATED         SIZE
example/docker-node-hello   latest    52f273faacd7   5 days ago      1.02GB
alpine                      latest    9234e8fb04c4   2 months ago    8.31MB
<none>                      <none>    0dccf5ee8cd6   18 months ago   1.02GB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image rm 0dccf5ee8cd6
Deleted: sha256:0dccf5ee8cd6d2b58c767802dd85a87bcf2fecc8c1c3d39138feedf8226aef69
Deleted: sha256:9aee5a0e0725ff8e4f6748515e3f9f64d506ae963c428beaf3736a8c6dac87b4
Deleted: sha256:76a9a329311187da570fb128fd198e569da7a2d3045e38b444e124326d324ccf
Deleted: sha256:0ac91a902de3bdda95a60359210fdcba9ccb625d503eeb4e9927c8b2368cac63
Deleted: sha256:d26430ad6f30ebaf59ac8f4628417d055d9b7103186b4142e797abf512124fa8
Deleted: sha256:02d794a9797b062d201e2394327f50fa2f36b86b510800cd82f781891134f1df
Deleted: sha256:60afd8e4a66d65bde3bd218fb8f637253916e36833866ae0fbc1a04c8167b410
Deleted: sha256:540c56a10da54fb43d2d43b13b108e6c9333647b93e2490b9b8c4e7c3467ab30
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 
```
```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
example/docker-node-hello   latest    52f273faacd7   5 days ago     1.02GB
alpine                      latest    9234e8fb04c4   2 months ago   8.31MB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker ps -as
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES     SIZE
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 
```
Finalmento dovremmo poter scaricare di nuovo l'immagine dal registro


```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker pull antonioesposito1/docker-c-hello:latest
latest: Pulling from antonioesposito1/docker-c-hello
cae3b572364a: Already exists 
bd090f42c4b7: Already exists 
f0c9d6d993ac: Already exists 
a2ade626d67a: Already exists 
608530f52d02: Already exists 
7796c506c112: Already exists 
83ec84e8a445: Already exists 
675ac3dabdd6: Already exists 
fb8a35fefdf2: Already exists 
4f4fb700ef54: Already exists 
6752cca14e99: Already exists 
Digest: sha256:85da5f5f11d8f8ba7e3374ab9a952ed14fc4eba72b795ff12b19060f7a9858b7
Status: Downloaded newer image for antonioesposito1/docker-c-hello:latest
docker.io/antonioesposito1/docker-c-hello:latest
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker image ls
REPOSITORY                        TAG       IMAGE ID       CREATED        SIZE
antonioesposito1/docker-c-hello   latest    4c8820d85657   2 hours ago    1.54GB
example/docker-node-hello         latest    52f273faacd7   5 days ago     1.02GB
alpine                            latest    9234e8fb04c4   2 months ago   8.31MB
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 


```

Come di vede comunqe la maggiorparte del layer di questa immagine erano comqune gia presenti sul mio pc.

```
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ docker run -it antonioesposito1/docker-c-hello
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
antonio@labnet5:~/docker/antonioesposito1-docker-c-hello$ 
```

