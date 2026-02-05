# Docker su om1l242

## Docker Version
La versione di API  minima lato client deve essere 1.24
```
[EspositoA1@om1l242 ~]$ sudo docker version
Client: Docker Engine - Community
 Version:           27.5.1
 API version:       1.47
 Go version:        go1.22.11
 Git commit:        9f9e405
 Built:             Wed Jan 22 13:43:02 2025
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.5.1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.11
  Git commit:       4c9b3b0
  Built:            Wed Jan 22 13:41:59 2025
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v2.1.5
  GitCommit:        fcd43222d6b07379a4be9786bda52438f0dd16a1
 runc:
  Version:          1.3.3
  GitCommit:        v1.3.3-0-gd842d771
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
[EspositoA1@om1l242 ~]$
```
## Server Information

- Containers: 19 Ci sono 19 container up and running
- C'è una sola immagine, quindi tutti i container usano la stessa immagine probabilente
- Kernel Version: 4.18.0-552.1.1.el8.x86_64
- Plugins: sono le features installate su docker, in pratica cosa riesce a fare deocker.
- Docker Root Dir: /var/lib/docker qui è dove si trovano le immagini e i container
- Runtimes: io.containerd.runc.v2 runc. runc è il default runtime di docker. 

```
[EspositoA1@om1l242 ~]$ sudo docker system info
[sudo] password for EspositoA1: 
Client: Docker Engine - Community
 Version:    27.5.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.30.1
    Path:     /usr/libexec/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /usr/libexec/docker/cli-plugins/docker-compose

Server:
 Containers: 19
  Running: 19
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 27.5.1
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: fcd43222d6b07379a4be9786bda52438f0dd16a1
 runc version: v1.3.3-0-gd842d771
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
 Kernel Version: 4.18.0-552.1.1.el8.x86_64
 Operating System: CentOS Stream 8
 OSType: linux
 Architecture: x86_64
 CPUs: 80
 Total Memory: 251.2GiB
 Name: om1l242.omnitel.it
 ID: 8a3f8d2b-81e1-43fb-a717-caafbc5abb14
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

[EspositoA1@om1l242 ~]$ 
```


```
[root@om1l242 ~]# cd /var/lib/docker/
[root@om1l242 docker]# ls -la
total 16
drwx--x---. 12 root root  171 Nov 28 17:58 .
drwxr-xr-x. 65 root root 4096 Nov 28 17:58 ..
drwx--x--x.  3 root root  123 Nov 28 17:58 buildkit
drwx--x---. 21 root root 4096 Jan 29 16:13 containers
-rw-------.  1 root root   36 Nov 28 17:58 engine-id
drwx------.  3 root root   22 Nov 28 17:58 image
drwxr-x---.  3 root root   19 Nov 28 17:58 network
drwx--x---. 42 root root 4096 Jan 29 16:13 overlay2
drwx------.  3 root root   17 Nov 28 17:58 plugins
drwx------.  2 root root    6 Nov 28 17:58 runtimes
drwx------.  2 root root    6 Nov 28 17:58 swarm
drwx------.  2 root root    6 Nov 28 18:16 tmp
drwx-----x.  2 root root   50 Nov 28 17:58 volumes
[root@om1l242 docker]# 
```


```
[root@om1l242 etc]# docker ps
CONTAINER ID   IMAGE                             COMMAND                  CREATED      STATUS      PORTS     NAMES
1b4fae2ff77b   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivpe036d
b95cc09fce1b   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivpe035d
50861ee27560   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-rmvar201d
97239aaa1a37   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivrr131d
1ecf316c53d6   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-bovar201d
344ba841ef3f   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-rmvpe036d
49c70fb7fd50   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivrr249d
9e01ba844c21   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-bovpe015d
6dafeb22380d   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivpe015d
e7f8e8fbaa8e   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-navar101d
afeb05440884   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivar211d
eb42b40af0a7   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-bovpe016d
b02b403bf92f   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-rmvar101d
0a0ef8ac12d6   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-rmvpe035d
0c34f63fff40   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivar102d
59daefef8a97   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivar202d
5527a66e48c1   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-navar201d
c500789e4b32   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-bovar101d
45e29b3f777e   ios-xr/xrd-control-plane:25.2.2   "/usr/local/sbin/init"   6 days ago   Up 6 days             clab-vnetd-mivpe016d
[root@om1l242 etc]# 

```


```
[root@om1l242 etc]# docker container inspect 1b4fae2ff77b
[
    {
        "Id": "1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933",
        "Created": "2026-01-29T15:13:46.52591069Z",
        "Path": "/usr/local/sbin/init",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 1078171,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2026-01-29T15:13:50.51839871Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:82593760b429b01297d77b125bd2555a173c397e21e78c85592a99ab54f7353f",
        "ResolvConfPath": "/var/lib/docker/containers/1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933/hostname",
        "HostsPath": "/var/lib/docker/containers/1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933/hosts",
        "LogPath": "/var/lib/docker/containers/1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933/1b4fae2ff77b9161a19d35de2bb8b31e0fd19f1c26a13bbce3c527264e3b3933-json.log",
        "Name": "/clab-vnetd-mivpe036d",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/first-boot.cfg:/etc/xrd/first-boot.cfg",
                "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/xr-storage:/xr-storage",
                "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/mgmt_intf_v6_addr.sh:/etc/xrd/mgmt_intf_v6_addr.sh"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "clab",
            "PortBindings": null,
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                0,
                0
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [
                "10.21.25.110"
            ],
            "DnsOptions": null,
            "DnsSearch": null,
            "ExtraHosts": [
                "mivpe036d:172.20.20.15",
                "mivpe036d:3fff:172:20:20::15",
                "bovpe015d:172.20.20.16",
                "bovpe015d:3fff:172:20:20::16",
                "mivar211d:172.20.20.20",
                "mivar211d:3fff:172:20:20::20",
                "navar101d:172.20.20.8",
                "navar101d:3fff:172:20:20::8",
                "mivrr131d:172.20.20.10",
                "mivrr131d:3fff:172:20:20::10",
                "bovar101d:172.20.20.4",
                "bovar101d:3fff:172:20:20::4",
                "rmvar201d:172.20.20.7",
                "rmvar201d:3fff:172:20:20::7",
                "mivrr249d:172.20.20.11",
                "mivrr249d:3fff:172:20:20::11",
                "mivar102d:172.20.20.2",
                "mivar102d:3fff:172:20:20::2",
                "mivpe016d:172.20.20.13",
                "mivpe016d:3fff:172:20:20::13",
                "mivpe015d:172.20.20.12",
                "mivpe015d:3fff:172:20:20::12",
                "navar201d:172.20.20.9",
                "navar201d:3fff:172:20:20::9",
                "rmvar101d:172.20.20.6",
                "rmvar101d:3fff:172:20:20::6",
                "rmvpe035d:172.20.20.18",
                "rmvpe035d:3fff:172:20:20::18",
                "rmvpe036d:172.20.20.19",
                "rmvpe036d:3fff:172:20:20::19",
                "bovar201d:172.20.20.5",
                "bovar201d:3fff:172:20:20::5",
                "mivar202d:172.20.20.3",
                "mivar202d:3fff:172:20:20::3",
                "bovpe016d:172.20.20.17",
                "bovpe016d:3fff:172:20:20::17",
                "mivpe035d:172.20.20.14",
                "mivpe035d:3fff:172:20:20::14"
            ],
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": true,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": [
                "label=disable"
            ],
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": null,
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": [
                {
                    "Name": "nofile",
                    "Hard": 262144,
                    "Soft": 262144
                }
            ],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": null,
            "ReadonlyPaths": null
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/cacfc8bdd3c613bb4f584957a1079642480f324b8f101c5928db58b639dc0d6c-init/diff:/var/lib/docker/overlay2/33c07ebdbb0de59d7b36b965246f9b95ff363d313db99c4729671768128643d6/diff",
                "MergedDir": "/var/lib/docker/overlay2/cacfc8bdd3c613bb4f584957a1079642480f324b8f101c5928db58b639dc0d6c/merged",
                "UpperDir": "/var/lib/docker/overlay2/cacfc8bdd3c613bb4f584957a1079642480f324b8f101c5928db58b639dc0d6c/diff",
                "WorkDir": "/var/lib/docker/overlay2/cacfc8bdd3c613bb4f584957a1079642480f324b8f101c5928db58b639dc0d6c/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/mgmt_intf_v6_addr.sh",
                "Destination": "/etc/xrd/mgmt_intf_v6_addr.sh",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/first-boot.cfg",
                "Destination": "/etc/xrd/first-boot.cfg",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d/xr-storage",
                "Destination": "/xr-storage",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
            "Hostname": "mivpe036d",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "CLAB_LABEL_CONTAINERLAB=vnetd",
                "CLAB_LABEL_CLAB_NODE_NAME=mivpe036d",
                "CLAB_LABEL_CLAB_NODE_GROUP=",
                "CLAB_LABEL_CLAB_TOPO_FILE=/home/EspositoA1/vnetd/topology.clab.yml",
                "XR_INTERFACES=linux:Gi0-0-0-0,xr_name=Gi0/0/0/0;linux:Gi0-0-0-1,xr_name=Gi0/0/0/1;linux:Gi0-0-0-3,xr_name=Gi0/0/0/3;linux:Gi0-0-0-4,xr_name=Gi0/0/0/4;linux:Gi0-0-0-5,xr_name=Gi0/0/0/5;linux:Gi0-0-0-12,xr_name=Gi0/0/0/12;",
                "CLAB_LABEL_CLAB_NODE_LAB_DIR=/home/EspositoA1/vnetd/clab-vnetd/mivpe036d",
                "CLAB_LABEL_CLAB_OWNER=EspositoA1",
                "CLAB_LABEL_CLAB_NODE_KIND=xrd",
                "XR_FIRST_BOOT_CONFIG=/etc/xrd/first-boot.cfg",
                "XR_MGMT_INTERFACES=linux:eth0,xr_name=Mg0/RP0/CPU0/0,chksum,snoop_v4,snoop_v6",
                "NO_PROXY=localhost,127.0.0.1,::1,*.local,172.20.20.0/24,172.20.20.10,172.20.20.11,172.20.20.12,172.20.20.13,172.20.20.14,172.20.20.15,172.20.20.16,172.20.20.17,172.20.20.18,172.20.20.19,172.20.20.2,172.20.20.20,172.20.20.3,172.20.20.4,172.20.20.5,172.20.20.6,172.20.20.7,172.20.20.8,172.20.20.9,3fff:172:20:20::/64,3fff:172:20:20::10,3fff:172:20:20::11,3fff:172:20:20::12,3fff:172:20:20::13,3fff:172:20:20::14,3fff:172:20:20::15,3fff:172:20:20::16,3fff:172:20:20::17,3fff:172:20:20::18,3fff:172:20:20::19,3fff:172:20:20::2,3fff:172:20:20::20,3fff:172:20:20::3,3fff:172:20:20::4,3fff:172:20:20::5,3fff:172:20:20::6,3fff:172:20:20::7,3fff:172:20:20::8,3fff:172:20:20::9,bovar101-201,bovar101-rm101,bovar101d,bovar111-bo101,bovar201-mi211,bovar201-rm201,bovar201d,bovpe015-101,bovpe015-16,bovpe015d,bovpe016-201,bovpe016d,bovpe111-bo101,ctvpe025-na101,ctvpe026-na201,labnet-mgmt,mi35-fsn30-cgn,mi36-fsn31-cgn,mibng037-vpe035,mibng037-vpe036,mivar042-mi211,mivar102-202,mivar102-bo,mivar102-rm,mivar102-vrr,mivar102d,mivar111-951z,mivar111-bo111,mivar111-mi102,mivar111-mi211,mivar111-na101,mivar111-rm101,mivar111-vpe111,mivar202-bo,mivar202-rm,mivar202-vrr,mivar202d,mivar211-851z,mivar211-bo201,mivar211-mi202,mivar211-rm211,mivar211-vpe211,mivar211d,mivce501-vpe015,mivce502-vpe016,mivpe015-102,mivpe015-16,mivpe015d,mivpe016-202,mivpe016d,mivpe035-102,mivpe035-36,mivpe035-fsn30,mivpe035d,mivpe036-202,mivpe036-fsn31,mivpe036d,mivpe045-102,mivpe046-202,mivpe111-102,mivpe111-na101,mivpe111-rm101,mivpe211-202,mivrr131d,mivrr249d,navar101-201,navar101-bo,navar101-rm,navar101d,navar201-bo,navar201-rm,navar201-rm211,navar201d,rmvar101-201,rmvar101-bo,rmvar101d,rmvar201-bo,rmvar201d,rmvar211-rm201,rmvpe015-101,rmvpe016-201,rmvpe035-101,rmvpe035-36,rmvpe035d,rmvpe036-201,rmvpe036d,rmvpe211-na201,rmvpe211-rm201",
                "CLAB_LABEL_CLAB_NODE_LONGNAME=clab-vnetd-mivpe036d",
                "CLAB_LABEL_CLAB_NODE_TYPE=",
                "CLAB_INTFS=6",
                "XR_EVERY_BOOT_SCRIPT=/etc/xrd/mgmt_intf_v6_addr.sh",
                "no_proxy=localhost,127.0.0.1,::1,*.local,172.20.20.0/24,172.20.20.10,172.20.20.11,172.20.20.12,172.20.20.13,172.20.20.14,172.20.20.15,172.20.20.16,172.20.20.17,172.20.20.18,172.20.20.19,172.20.20.2,172.20.20.20,172.20.20.3,172.20.20.4,172.20.20.5,172.20.20.6,172.20.20.7,172.20.20.8,172.20.20.9,3fff:172:20:20::/64,3fff:172:20:20::10,3fff:172:20:20::11,3fff:172:20:20::12,3fff:172:20:20::13,3fff:172:20:20::14,3fff:172:20:20::15,3fff:172:20:20::16,3fff:172:20:20::17,3fff:172:20:20::18,3fff:172:20:20::19,3fff:172:20:20::2,3fff:172:20:20::20,3fff:172:20:20::3,3fff:172:20:20::4,3fff:172:20:20::5,3fff:172:20:20::6,3fff:172:20:20::7,3fff:172:20:20::8,3fff:172:20:20::9,bovar101-201,bovar101-rm101,bovar101d,bovar111-bo101,bovar201-mi211,bovar201-rm201,bovar201d,bovpe015-101,bovpe015-16,bovpe015d,bovpe016-201,bovpe016d,bovpe111-bo101,ctvpe025-na101,ctvpe026-na201,labnet-mgmt,mi35-fsn30-cgn,mi36-fsn31-cgn,mibng037-vpe035,mibng037-vpe036,mivar042-mi211,mivar102-202,mivar102-bo,mivar102-rm,mivar102-vrr,mivar102d,mivar111-951z,mivar111-bo111,mivar111-mi102,mivar111-mi211,mivar111-na101,mivar111-rm101,mivar111-vpe111,mivar202-bo,mivar202-rm,mivar202-vrr,mivar202d,mivar211-851z,mivar211-bo201,mivar211-mi202,mivar211-rm211,mivar211-vpe211,mivar211d,mivce501-vpe015,mivce502-vpe016,mivpe015-102,mivpe015-16,mivpe015d,mivpe016-202,mivpe016d,mivpe035-102,mivpe035-36,mivpe035-fsn30,mivpe035d,mivpe036-202,mivpe036-fsn31,mivpe036d,mivpe045-102,mivpe046-202,mivpe111-102,mivpe111-na101,mivpe111-rm101,mivpe211-202,mivrr131d,mivrr249d,navar101-201,navar101-bo,navar101-rm,navar101d,navar201-bo,navar201-rm,navar201-rm211,navar201d,rmvar101-201,rmvar101-bo,rmvar101d,rmvar201-bo,rmvar201d,rmvar211-rm201,rmvpe015-101,rmvpe016-201,rmvpe035-101,rmvpe035-36,rmvpe035d,rmvpe036-201,rmvpe036d,rmvpe211-na201,rmvpe211-rm201",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": null,
            "Image": "ios-xr/xrd-control-plane:25.2.2",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/usr/local/sbin/init"
            ],
            "OnBuild": null,
            "Labels": {
                "clab-mgmt-net-bridge": "br-9a1e080830af",
                "clab-node-group": "",
                "clab-node-kind": "xrd",
                "clab-node-lab-dir": "/home/EspositoA1/vnetd/clab-vnetd/mivpe036d",
                "clab-node-longname": "clab-vnetd-mivpe036d",
                "clab-node-name": "mivpe036d",
                "clab-node-type": "",
                "clab-owner": "EspositoA1",
                "clab-topo-file": "/home/EspositoA1/vnetd/topology.clab.yml",
                "com.cisco.ios-xr.build-info.lineup": "r252x.lu%EFR-00000476448",
                "com.cisco.ios-xr.build-info.timestamp": "Sat Sep 20 22:34:24 UTC 2025",
                "com.cisco.ios-xr.build-info.version": "25.2.2",
                "com.cisco.ios-xr.build-info.workspace": "/auto/srcarchive11/prod/25.2.2/xrd-control-plane/ws",
                "com.cisco.ios-xr.platform": "xrd-control-plane",
                "containerlab": "vnetd",
                "io.buildah.version": "1.27.2"
            },
            "StopSignal": "SIGRTMIN+3"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "c35ab00c9dd6d7bd26a063557d5cc1852ba36aaa71001b803e5f6750886b44e7",
            "SandboxKey": "/var/run/docker/netns/c35ab00c9dd6",
            "Ports": {},
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "clab": {
                    "IPAMConfig": {
                        "IPv4Address": "172.20.20.15",
                        "IPv6Address": "3fff:172:20:20::15"
                    },
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:14:14:0f",
                    "DriverOpts": null,
                    "NetworkID": "9a1e080830affb0a3cebe7427080018bf6c1c8bad13f276bce89665df2fb046f",
                    "EndpointID": "8a35b7226ccd6223b28761db677c5fbce728c7ca4b768baf4561233a0cab2196",
                    "Gateway": "172.20.20.1",
                    "IPAddress": "172.20.20.15",
                    "IPPrefixLen": 24,
                    "IPv6Gateway": "3fff:172:20:20::1",
                    "GlobalIPv6Address": "3fff:172:20:20::15",
                    "GlobalIPv6PrefixLen": 64,
                    "DNSNames": [
                        "clab-vnetd-mivpe036d",
                        "1b4fae2ff77b",
                        "mivpe036d"
                    ]
                }
            }
        }
    }
]
[root@om1l242 etc]# 
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
