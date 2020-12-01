## List of Docker commands

### General 

See space used by docker 
```
# docker system df
TYPE                TOTAL               ACTIVE              SIZE                RECLAIMABLE
Images              66                  49                  13.54GB             5.68GB (41%)
Containers          206                 87                  948.4MB             249.6MB (26%)
Local Volumes       20                  20                  0B                  0B
Build Cache         0                   0                   0B                  0B
```


### Images

List of images
```
# podman images
REPOSITORY                    TAG              IMAGE ID      CREATED       SIZE
docker.io/library/nginx       latest           bc9a0695f571  6 days ago    137 MB
```

Pull docker image
```
~# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:6b1daa9462046581ac15be20277a7c75476283f969cb3a61c8725ec38d3b01c3
Status: Image is up to date for nginx:latest

```

Pushing image
```
root@chandi-allinone1:~# docker image push chandidas/nginx
The push refers to repository [docker.io/chandidas/nginx]
7e914612e366: Preparing
f790aed835ee: Preparing
850c2400ea4d: Preparing
7ccabd267c9f: Preparing
f5600c6330da: Preparing
```

Tagging Image
```
root@chandi-allinone1:~# docker tag -h
Flag shorthand -h has been deprecated, please use --help

Usage:  docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```

History of the image (as it builds layer-by-layer)
```
# docker history nginx
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
bc9a0695f571        6 days ago          /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B
<missing>           6 days ago          /bin/sh -c #(nop)  STOPSIGNAL SIGQUIT           0B
<missing>           6 days ago          /bin/sh -c #(nop)  EXPOSE 80                    0B
<missing>           6 days ago          /bin/sh -c #(nop)  ENTRYPOINT ["/docker-entr…   0B
<missing>           6 days ago          /bin/sh -c #(nop) COPY file:0fd5fca330dcd6a7…   1.04kB
<missing>           6 days ago          /bin/sh -c #(nop) COPY file:08ae525f517706a5…   1.95kB
<missing>           6 days ago          /bin/sh -c #(nop) COPY file:e7e183879c35719c…   1.2kB
<missing>           6 days ago          /bin/sh -c set -x     && addgroup --system -…   63.6MB
<missing>           6 days ago          /bin/sh -c #(nop)  ENV PKG_RELEASE=1~buster     0B
<missing>           6 days ago          /bin/sh -c #(nop)  ENV NJS_VERSION=0.4.4        0B
<missing>           6 days ago          /bin/sh -c #(nop)  ENV NGINX_VERSION=1.19.5     0B
<missing>           13 days ago         /bin/sh -c #(nop)  LABEL maintainer=NGINX Do…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>           13 days ago         /bin/sh -c #(nop) ADD file:d2abb0e4e7ac17737…   69.2MB
```

Metadata of the image
```
root@chandi-allinone1:~# docker inspect nginx
[
    {
        "Id": "sha256:bc9a0695f5712dcaaa09a5adc415a3936ccba13fc2587dfd76b1b8aeea3f221c",
        "RepoTags": [
            "nginx:latest"
        ],
        "RepoDigests": [
            "nginx@sha256:6b1daa9462046581ac15be20277a7c75476283f969cb3a61c8725ec38d3b01c3"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2020-11-25T00:30:19.011398516Z",
        "Container": "279e6916c4aaaf5d61e468508abd96933f4e48194bd979dc692e0196cde2d59d",
        "ContainerConfig": {
            "Hostname": "279e6916c4aa",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.19.5",
                "NJS_VERSION=0.4.4",
                "PKG_RELEASE=1~buster"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"nginx\" \"-g\" \"daemon off;\"]"
            ],
            "Image": "sha256:2b3c3cbe8cc157ef2c15e693980ae186cffc7b7be17afb34f35de8d7c57a3169",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "DockerVersion": "19.03.12",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.19.5",
                "NJS_VERSION=0.4.4",
                "PKG_RELEASE=1~buster"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "sha256:2b3c3cbe8cc157ef2c15e693980ae186cffc7b7be17afb34f35de8d7c57a3169",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 132895204,
        "VirtualSize": 132895204,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/snap/microk8s/common/var/lib/docker/overlay2/641c5f37350d77faeba0dcc92a565389a4b7290d66523f21521228827d073aad/diff:/var/snap/microk8s/common/var/lib/docker/overlay2/7403e791cdbb4b8d7556ddacfd549d986bfed410cb22351d0b6dd0707ca644b2/diff:/var/snap/microk8s/common/var/lib/docker/overlay2/eef47b5dce6151949e84772743d2e9703c503f4347563d2421492395ec2e939c/diff:/var/snap/microk8s/common/var/lib/docker/overlay2/99e5808fb8d56bc7c15ddd4f945730a6a8d7cac7d3f051a1782ea5d81043d592/diff",
                "MergedDir": "/var/snap/microk8s/common/var/lib/docker/overlay2/f4ed41857775fdcdadd9664dd410592406da594ba048516a08d06b9ecd3760c5/merged",
                "UpperDir": "/var/snap/microk8s/common/var/lib/docker/overlay2/f4ed41857775fdcdadd9664dd410592406da594ba048516a08d06b9ecd3760c5/diff",
                "WorkDir": "/var/snap/microk8s/common/var/lib/docker/overlay2/f4ed41857775fdcdadd9664dd410592406da594ba048516a08d06b9ecd3760c5/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:f5600c6330da7bb112776ba067a32a9c20842d6ecc8ee3289f1a713b644092f8",
                "sha256:7ccabd267c9f125d6eeac54e32f6fbb338431828a3ee4c61600a301205e16627",
                "sha256:850c2400ea4dc52c17a0a8f8dd740628fbbf2fac8c24ce12f5c540f2d8e4a835",
                "sha256:f790aed835eec5d82dae9e0cbb9021063d9fe71885542f11b7a46631176301f7",
                "sha256:7e914612e36657b45436586984a556f9d3762e8e03374c6cd8c5d9e460a00c51"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

Build docker image
```
# docker image build -t image_name:tag .

# docker image build -t image_name:tag  -f Dockerfile
```

Remove a image
```
# docker rmi chandidas/nginx
Untagged: chandidas/nginx:latest
```

Cleanup dangling images
```
# docker image prune
WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] y
Deleted Images:
```


### Network

A Docker container connected to a `Private Virtual Network` by default and it is of type `Bridge`. We can create different network if the default one needs to be changed. Each of these `Virtual Network`s route the packets through NAT Firewall on Host IP.

When you want to specify the network to attach a container use `--net=<>` option

List of Networks
```
# podman network ls
NAME    VERSION  PLUGINS
podman  0.4.0    bridge,portmap,firewall,tuning
```

Create a New Network
```
[root@cha-ceph-wrkr-1 ~]# podman network create my-net
/etc/cni/net.d/my-net.conflist
[root@cha-ceph-wrkr-1 ~]# podman network ls
NAME    VERSION  PLUGINS
podman  0.4.0    bridge,portmap,firewall,tuning
my-net  0.4.0    bridge,portmap,firewall
```

Inspect the Network
```
[root@cha-ceph-wrkr-1 ~]# podman  network inspect my-net
[
  {
    "cniVersion": "0.4.0",
    "name": "my-net",
    "plugins": [
      {
        "bridge": "cni-podman1",
        "hairpinMode": true,
        "ipMasq": true,
        "ipam": {
          "ranges": [
            [
              {
                "gateway": "10.89.0.1",
                "subnet": "10.89.0.0/24"
              }
            ]
          ],
          "routes": [
            {
              "dst": "0.0.0.0/0"
            }
          ],
          "type": "host-local"
        },
        "isGateway": true,
        "type": "bridge"
      },
      {
        "capabilities": {
          "portMappings": true
        },
        "type": "portmap"
      },
      {
        "backend": "",
        "type": "firewall"
      }
    ]
  }
]

```

Attach the network
```
[root@cha-ceph-wrkr-1 ~]# podman container run -d --net my-net --name test-cont nginx
6dc57d2a98197173f7d6f8fc7d87adf18f963b940643e4265464497a42006b61
```

Containers on the same `Virtual Network` can talk to each other without exposing Port. However, if a container wants to talk to external world it must Publish port.
When a container need to attach to the Host network itself we need to use `--net=host` option.

Publish a Port
```
[root@cha-ceph-wrkr-1 ~]# podman container run -d -p 3080:80 --net my-net --name test-cont nginx

-p Port-on-HOST:Port-on-Container

```

As container's IP assignment is dynamic, container IP would change across reboot. DNS helps here to identify a container. A container's name is used to resolve it's IP address. Whenever a new container gets created, it's name and IP is recorded a DNS entry by the docker.




### Storage
