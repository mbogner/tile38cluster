# ybcluster

This is a setup for YugabyteDB cluster based on docker compose.

It consists of 3 master nodes:
 - ybmaster1
 - ybmaster2
 - ybmaster3

There is a haproxy instance to load balance admin web interface requests between those 3: 
[http://127.0.0.1:7000](http://127.0.0.1:7000)

Further there are 3 tablet servers registered:
 - ybtserver1 ([http://127.0.0.1:9001](http://127.0.0.1:9001), SQL port 5434)
 - ybtserver2 ([http://127.0.0.1:9002](http://127.0.0.1:9002), SQL port 5435)
 - ybtserver3 ([http://127.0.0.1:9003](http://127.0.0.1:9003), SQL port 5436)

As you can see it is possible to connect to every single table server's postgresql port (listed above). But the config
also include a load balances 5433 port via haproxy.

Haproxy is configured to serve stats via [http://127.0.0.1:9000](http://127.0.0.1:9000]).

## YEDIS

YugabyteDB also include a Redis compatible server which is mapped via haproxy to 127.0.0.1:6379. By default this doesn't
require a password but this can be changed by connecting to the server and configuring one like so:

```shell
redis-cli # using default 127.0.0.1 on default port so no extra args needed
127.0.0.1:6379> CONFIG SET requirepass "yugabyte"
# from now on the password yugabyte is required
```

This uses redis database number 0. Seems like for now other numbers aren't supported yet.

## Quickstart

This sample only requires docker 19.03.0+.

```shell
docker compose up -d
```

With the cluster up and running you can connect to it via 127.0.0.1 on port 5433 with login `yugabyte:yugabyte`.

## WARNING

!!!This is a single node setup and won't help to improve your availability!!!

The purpose of this project is to take notes of the necessary steps to configure a yugabytedb cluster. But instead of
creating a bunch of VMs it relies on docker. If you bring the configs to proper VMs and distribute these over different
servers you can reuse the configs from this project.

An alternative to docker would have been vagrant but still I didn't want to deal with the overhead of VMs just for
testing some configs.