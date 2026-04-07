# install docker su debian13 labnet6

```
antonio@labnet6:~$ su
Password: 
root@labnet6:/home/antonio# apt update
Trovato:1 http://deb.debian.org/debian trixie InRelease
Trovato:2 http://security.debian.org/debian-security trixie-security InRelease
Trovato:3 http://deb.debian.org/debian trixie-updates InRelease
Tutti i pacchetti sono aggiornati.         
root@labnet6:/home/antonio# 

```


```
root@labnet6:/home/antonio# apt install ca-certificates curl
ca-certificates è già alla versione più recente (20250419).
Installazione:
  curl

Riepilogo:
  Aggiornamento: 0, Installazione: 1, Rimozione: 0, Non aggiornati: 0
  Dimensione scaricamento: 270 kB
  Spazio richiesto: 506 kB / 863 GB disponibile

Continuare? [S/n] S
Scaricamento di:1 http://deb.debian.org/debian trixie/main amd64 curl amd64 8.14.1-2+deb13u2 [270 kB]
Recuperati 270 kB in 16s (17,3 kB/s)                                                                                                                                                                              
Selezionato il pacchetto curl non precedentemente selezionato.
(Lettura del database... 156949 file e directory attualmente installati.)
Preparativi per estrarre .../curl_8.14.1-2+deb13u2_amd64.deb...
Estrazione di curl (8.14.1-2+deb13u2)...
Configurazione di curl (8.14.1-2+deb13u2)...
Elaborazione dei trigger per man-db (2.13.1-1)...
root@labnet6:/home/antonio# 

```
Il comando
install -m 0755 -d /etc/apt/keyrings viene utilizzato per creare la directory /etc/apt/keyrings con permessi di lettura ed esecuzione per tutti gli utenti, ma di scrittura solo per il proprietario (root). 
Descrizione dei parametri

install: Un'utilità versatile che combina la creazione di directory, la copia di file e l'impostazione dei permessi in un unico passaggio. 
-m 0755: Imposta la modalità (permessi) della directory a 0755 (rwxr-xr-x). Questo assicura che il sistema APT possa leggere le chiavi GPG memorizzate all'interno, mentre solo l'utente root può modificarle.
-d: Indica al comando di creare una directory anziché copiare un file.
/etc/apt/keyrings: Il percorso della directory di destinazione. Questa è la posizione standard raccomandata per memorizzare chiavi GPG di terze parti (come quelle per Docker o altri repository esterni) su versioni recenti di Debian e Ubuntu. 

Perché si usa?
Nelle versioni più recenti di Linux (come Ubuntu 22.04+ e Debian 12+), il comando apt-key è deprecato per motivi di sicurezza. La pratica corretta è ora scaricare le chiavi GPG direttamente in questa directory specifica. 
Esempio di utilizzo tipico:
bash

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg




```
root@labnet6:/home/antonio# install -m 0755 -d /etc/apt/keyrings
root@labnet6:/home/antonio#
```


```
root@labnet6:/home/antonio# curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
root@labnet6:/home/antonio# 
```


```
root@labnet6:/home/antonio# cd /etc/apt/keyrings/
root@labnet6:/etc/apt/keyrings# ls -lrt
totale 4
-rw-rw-r-- 1 root root 3817  7 apr 15.56 docker.asc
root@labnet6:/etc/apt/keyrings# sudo chmod a+r /etc/apt/keyrings/docker.asc
root@labnet6:/etc/apt/keyrings# ls -lrt
totale 4
-rw-rw-r-- 1 root root 3817  7 apr 15.56 docker.asc
root@labnet6:/etc/apt/keyrings# 

```


```
root@labnet6:/etc/apt/keyrings# tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: trixie
Components: stable
Architectures: amd64
Signed-By: /etc/apt/keyrings/docker.asc
root@labnet6:/etc/apt/keyrings#
```



```
root@labnet6:/etc/apt/keyrings# cat /etc/apt/sources.list.d/docker.sources
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: trixie
Components: stable
Architectures: amd64
Signed-By: /etc/apt/keyrings/docker.asc
root@labnet6:/etc/apt/keyrings#

```



```
root@labnet6:/etc/apt/keyrings# apt update
Trovato:1 http://deb.debian.org/debian trixie InRelease
Trovato:2 http://security.debian.org/debian-security trixie-security InRelease
Trovato:3 http://deb.debian.org/debian trixie-updates InRelease
Scaricamento di:4 https://download.docker.com/linux/debian trixie InRelease [32,5 kB]
Scaricamento di:5 https://download.docker.com/linux/debian trixie/stable amd64 Packages [31,4 kB]
Recuperati 63,9 kB in 0s (420 kB/s) 
Tutti i pacchetti sono aggiornati.         
root@labnet6:/etc/apt/keyrings#
```


```
root@labnet6:/home/antonio# apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Installazione:                             
  containerd.io  docker-buildx-plugin  docker-ce  docker-ce-cli  docker-compose-plugin

Installazione dipendenze: 
  docker-ce-rootless-extras  pigz

Pacchetti suggeriti:
  cgroupfs-mount  | cgroup-lite  docker-model-plugin

Riepilogo:
  Aggiornamento: 0, Installazione: 7, Rimozione: 0, Non aggiornati: 0
  Dimensione scaricamento: 94,5 MB / 94,5 MB
  Spazio richiesto: 364 MB / 863 GB disponibile

Continuare? [S/n] S
Scaricamento di:1 https://download.docker.com/linux/debian trixie/stable amd64 containerd.io amd64 2.2.2-1~debian.13~trixie [23,6 MB]
Scaricamento di:2 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-cli amd64 5:29.4.0-1~debian.13~trixie [16,9 MB]
Scaricamento di:3 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce amd64 5:29.4.0-1~debian.13~trixie [22,7 MB]                                                                              
Scaricamento di:4 https://download.docker.com/linux/debian trixie/stable amd64 docker-buildx-plugin amd64 0.33.0-1~debian.13~trixie [16,9 MB]                                                                     
Scaricamento di:5 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-rootless-extras amd64 5:29.4.0-1~debian.13~trixie [6.557 kB]                                                             
Scaricamento di:6 https://download.docker.com/linux/debian trixie/stable amd64 docker-compose-plugin amd64 5.1.1-1~debian.13~trixie [7.846 kB]                                                                    
Recuperati 94,0 MB in 17s (5.604 kB/s)                                                                                                                                                                            
Selezionato il pacchetto containerd.io non precedentemente selezionato.
(Lettura del database... 156961 file e directory attualmente installati.)
Preparativi per estrarre .../0-containerd.io_2.2.2-1~debian.13~trixie_amd64.deb...
Estrazione di containerd.io (2.2.2-1~debian.13~trixie)...
Selezionato il pacchetto docker-ce-cli non precedentemente selezionato.
Preparativi per estrarre .../1-docker-ce-cli_5%3a29.4.0-1~debian.13~trixie_amd64.deb...
Estrazione di docker-ce-cli (5:29.4.0-1~debian.13~trixie)...
Selezionato il pacchetto docker-ce non precedentemente selezionato.
Preparativi per estrarre .../2-docker-ce_5%3a29.4.0-1~debian.13~trixie_amd64.deb...
Estrazione di docker-ce (5:29.4.0-1~debian.13~trixie)...
Selezionato il pacchetto pigz non precedentemente selezionato.
Preparativi per estrarre .../3-pigz_2.8-1_amd64.deb...
Estrazione di pigz (2.8-1)...
Selezionato il pacchetto docker-buildx-plugin non precedentemente selezionato.
Preparativi per estrarre .../4-docker-buildx-plugin_0.33.0-1~debian.13~trixie_amd64.deb...
Estrazione di docker-buildx-plugin (0.33.0-1~debian.13~trixie)...
Selezionato il pacchetto docker-ce-rootless-extras non precedentemente selezionato.
Preparativi per estrarre .../5-docker-ce-rootless-extras_5%3a29.4.0-1~debian.13~trixie_amd64.deb...
Estrazione di docker-ce-rootless-extras (5:29.4.0-1~debian.13~trixie)...
Selezionato il pacchetto docker-compose-plugin non precedentemente selezionato.
Preparativi per estrarre .../6-docker-compose-plugin_5.1.1-1~debian.13~trixie_amd64.deb...
Estrazione di docker-compose-plugin (5.1.1-1~debian.13~trixie)...
Configurazione di docker-buildx-plugin (0.33.0-1~debian.13~trixie)...
Configurazione di containerd.io (2.2.2-1~debian.13~trixie)...
Created symlink '/etc/systemd/system/multi-user.target.wants/containerd.service' → '/usr/lib/systemd/system/containerd.service'.
Configurazione di docker-compose-plugin (5.1.1-1~debian.13~trixie)...
Configurazione di docker-ce-cli (5:29.4.0-1~debian.13~trixie)...
Configurazione di pigz (2.8-1)...
Configurazione di docker-ce-rootless-extras (5:29.4.0-1~debian.13~trixie)...
Configurazione di docker-ce (5:29.4.0-1~debian.13~trixie)...
Created symlink '/etc/systemd/system/multi-user.target.wants/docker.service' → '/usr/lib/systemd/system/docker.service'.
Created symlink '/etc/systemd/system/sockets.target.wants/docker.socket' → '/usr/lib/systemd/system/docker.socket'.
Elaborazione dei trigger per man-db (2.13.1-1)...
root@labnet6:/home/antonio#
```

```
root@labnet6:/home/antonio# sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-04-07 16:05:22 CEST; 26s ago
 Invocation: 1b32fd2ffef14c7ea522e057ef839eec
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2805 (dockerd)
      Tasks: 14
     Memory: 31.9M (peak: 32.9M)
        CPU: 305ms
     CGroup: /system.slice/docker.service
             └─2805 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.280666328+02:00" level=info msg="Restoring containers: start."
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.366784721+02:00" level=info msg="Deleting nftables IPv4 rules" error="exit status 1" output="Error: Could not process rule: No such file or direc>
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.398993552+02:00" level=info msg="Deleting nftables IPv6 rules" error="exit status 1" output="Error: Could not process rule: No such file or direc>
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.798835140+02:00" level=info msg="Loading containers: done."
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.804578822+02:00" level=info msg="Docker daemon" commit=daa0cb7 containerd-snapshotter=true storage-driver=overlayfs version=29.4.0
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.804679078+02:00" level=info msg="Initializing buildkit"
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.854590284+02:00" level=info msg="Completed buildkit initialization"
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.857882955+02:00" level=info msg="Daemon has completed initialization"
apr 07 16:05:22 labnet6 dockerd[2805]: time="2026-04-07T16:05:22.857925820+02:00" level=info msg="API listen on /run/docker.sock"
apr 07 16:05:22 labnet6 systemd[1]: Started docker.service - Docker Application Container Engine.
root@labnet6:/home/antonio#
```
```
root@labnet6:/home/antonio# sudo systemctl enable docker
Synchronizing state of docker.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable docker
root@labnet6:/home/antonio# 
root@labnet6:/home/antonio#
```
```
root@labnet6:/home/antonio# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
d5e71e642bf5: Download complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

root@labnet6:/home/antonio# 
```
```
root@labnet6:/home/antonio# docker --version
Docker version 29.4.0, build 9d7ad9f
root@labnet6:/home/antonio#
```
```
```
```
```
```
```
```
```
```
```
```
```
```
```
