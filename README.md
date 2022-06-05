# tile38cluster

Simple tile38 cluster with a leader and a follower. In front sits a haproxy instance that checks for the leader and 
forwards traffic to the leader.

## Quickstart

This sample only requires docker 19.03.0+.

```shell
docker compose up -d
```

With the cluster up and running you can connect to it via 127.0.0.1 on port 9851 with redis-cli.

## WARNING

!!!This is a single node setup and won't help to improve your availability!!!

The purpose of this project is to take notes of the necessary steps to configure a til38 cluster. But instead of
creating a bunch of VMs it relies on docker. If you bring the configs to proper VMs and distribute these over different
servers you can reuse the configs from this project.

An alternative to docker would have been vagrant but still I didn't want to deal with the overhead of VMs just for
testing some configs.