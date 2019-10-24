```
[node1] (local) root@192.168.0.13 ~
$ docker network create -d macvlan \
>   --subnet=172.16.86.0/24 \
>   --gateway=172.16.86.1 \
>   -o parent=eth0 \
>   my-macvlan-net
d8776ae116df4fb55a88e1d98f6dcdfb120404b69c9b4b2e9db223b2a5c7536a


[node1] (local) root@192.168.0.13 ~
$ docker run --rm -itd   --network my-macvlan-net   --name my-macvlan-alpine   alpine:latest   ash
298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d




[node1] (local) root@192.168.0.13 ~
$ docker container inspect my-macvlan-alpine
[
    {
        "Id": "298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d",
        "Created": "2019-06-12T12:33:21.88338797Z",
        "Path": "ash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 24229,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2019-06-12T12:33:23.338789146Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:055936d3920576da37aa9bc460d70c5f212028bda1c08c0879aedf03d7a66ea1",
        "ResolvConfPath": "/var/lib/docker/containers/298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d/hostname",
        "HostsPath": "/var/lib/docker/containers/298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d/hosts",
        "LogPath": "/var/lib/docker/containers/298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d/298a778214d64262e2ec489dd110b0101093c5382639892742ee52ccf1238e4d-json.log",
        "Name": "/my-macvlan-alpine",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "my-macvlan-net",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": true,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
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
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "DiskQuota": 0,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/5a76d19a434877960200554093e59b835d427bc103be01827ab8b244a4d65392-init/diff:/var/lib/docker/overlay2/ac3dc2eb9921c9f1ef6480594973405dfa96d061fe5eafc7c141be1a6d2ecc1a/diff",
                "MergedDir": "/var/lib/docker/overlay2/5a76d19a434877960200554093e59b835d427bc103be01827ab8b244a4d65392/merged",
                "UpperDir": "/var/lib/docker/overlay2/5a76d19a434877960200554093e59b835d427bc103be01827ab8b244a4d65392/diff",
                "WorkDir": "/var/lib/docker/overlay2/5a76d19a434877960200554093e59b835d427bc103be01827ab8b244a4d65392/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "298a778214d6",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "ash"
            ],
            "Image": "alpine:latest",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "e6e7b1e66b137c04f1502b3330aa8b999c64e4ebf398fda791d5ca34abe14042",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/e6e7b1e66b13",
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
                "my-macvlan-net": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "298a778214d6"
                    ],
                    "NetworkID": "d8776ae116df4fb55a88e1d98f6dcdfb120404b69c9b4b2e9db223b2a5c7536a",
                    "EndpointID": "4d582f223b91378503338bdbf745ade7cef871db89892549cc8267e8cdab742b",
                    "Gateway": "172.16.86.1",
                    "IPAddress": "172.16.86.2",
                    "IPPrefixLen": 24,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:10:56:02",
                    "DriverOpts": null
                }
            }
        }
    }
]

"Adding change 1"
"Adding change 2"
[node1] (local) root@192.168.0.13 ~
[node1] (local) root@192.168.0.13 ~
$ docker exec my-macvlan-alpine ip addr show eth0
74: eth0@if18374: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UNKNOWN
    link/ether 02:42:ac:10:56:02 brd ff:ff:ff:ff:ff:ff
    inet 172.16.86.2/24 brd 172.16.86.255 scope global eth0
       valid_lft forever preferred_lft forever
       
 


```
