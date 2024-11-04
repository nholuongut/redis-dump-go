# Redis-dump-go

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

Dump Redis keys to a file. Similar in spirit to https://www.npmjs.com/package/redis-dump and https://github.com/delano/redis-dump but:

* Will dump keys across **several processes & connections**
* Uses SCAN rather than KEYS * for much **reduced memory footprint** with large databases
* Easy to deploy & containerize - **single binary**.
* Generates a [RESP](https://redis.io/topics/protocol) file rather than a JSON or a list of commands. This is **faster to ingest**, and [recommended by Redis](https://redis.io/topics/mass-insert) for mass-inserts.

Warning: like similar tools, Redis-dump-go does NOT provide Point-in-Time backups. Please use [Redis backups methods](https://redis.io/topics/persistence) when possible.

## Features

* Dumps all databases present on the Redis server
* Keys TTL are preserved by default
* Configurable Output (Redis commands, RESP)
* Redis password-authentication

## Installation

Download the appropriate version for your operating system on [ŧhe release page](https://github.com/nholuongut/redis-dump-go/releases),
or use the [Docker image](https://github.com/users/nholuongut/packages/container/package/redis-dump-go):

```bash
$ docker run ghcr.io/nholuongut/redis-dump-go:latest -h
Usage of /redis-dump-go:
[...]
```
_Bandwidth costs_: Redis-dump-go is hosted on on Github Container Registry which is currently in Beta. During that period,
[bandwidth is free](https://docs.github.com/en/packages/guides/about-github-container-registry). After that period,
a Github Account might be required / bandwidth costs might be applicable.

## Run

```
$ ./bin/redis-dump-go -h
Usage of ./bin/redis-dump-go:
  -batchSize int
        HSET/RPUSH/SADD/ZADD only add 'batchSize' items at a time (default 1000)
  -db uint
        only dump this database (default: all databases)
  -filter string
        Key filter to use (default "*")
  -host string
        Server host (default "127.0.0.1")
  -n int
        Parallel workers (default 10)
  -noscan
        Use KEYS * instead of SCAN - for Redis <=2.8
  -output string
        Output type - can be resp or commands (default "resp")
  -port int
        Server port (default 6379)
  -s    Silent mode (disable logging of progress / stats)
  -ttl
        Preserve Keys TTL (default true)

$ ./bin/redis-dump-go > dump.resp
Database 0: 9 element dumped
Database 1: 1 element dumped
```

For password-protected Redis servers, set the shell variable REDISDUMPGO\_AUTH:

```
$ export REDISDUMPGO_AUTH=myRedisPassword
$ redis-dump-go
```

## Build

Given a correctly configured Go environment:

```
$ go get github.com/nholuongut/redis-dump-go
$ cd ${GOPATH}/src/github.com/nholuongut/redis-dump-go
$ go test ./...
$ go install
```

## Importing the data

```
redis-cli --pipe < redis-backup.txt
```

## Release Notes & Gotchas

 * By default, no cleanup is performed before inserting data. When importing the resulting file, hashes, sets and queues will be merged with data already present in the Redis.

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: Nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)
* [PayPal.me](https://www.paypal.com/paypalme/nholuongut)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License