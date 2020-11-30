## List of Docker commands

### General 

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
