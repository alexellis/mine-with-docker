mine-with-docker
=================

This repository contains Docker images that lets you get from zero to mining in around 5 minutes on any Linux host anywhere.

CPU mining can be profitable using algorithmns like: Cryptonight, Hodl or Equihash. Find out more about [profitability here](https://www.nicehash.com/profitability-calculator).

Disclaimer: this software is provided with no warranty. Use at your own risk. If you plan to mine on a cloud check the terms and conditions before you start. The same applies if you are using private equipment or an on-site datacenter for mining. Mining will use all the CPU resources available on the machine.

## Pre-reqs

We need to install Docker so that we can run a container. The container holds all the mining code and dependencies as a single immutable image.

* Install Docker:

```
curl -sL get.docker.com | sh
```

> If not running as a root user then you should look at the final message about using `usermod` to grant access to Docker to your user account.

## Start mining

Create a service and enter your bitcoin wallet ID:

```
docker service rm miner
docker service create --name miner alexellis2/cpu-opt:2018-1-2 ./cpuminer \
  -a cryptonight -o stratum+tcp://cryptonight.eu.nicehash.com:3355 \
  -u 1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o.cloud1
```

Replace "1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o" with your wallet ID and "cloud1" with the name of the host you're mining on if you want to track it.

## Stop/pause mining

To pause mining type in `docker service scale miner=0`. To resume set the replicas to `1`.

To completely stop mining use `docker service rm miner`

## Rebuild the image

This is optional. If you need to rebuild the Docker image for updates or for a different CPU architecture:

```
git clone https://github.com/alexellis/mine-with-docker
cd mine-with-docker/cpu-opt
docker build -t cpu-opt:latest .
```

## Donate

Donate via BTC: 1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o
Donate via ETH: 0x0D0c7108AD4180486E03B4Fc44AD794a209eCb37

Copyright Alex Ellis 2017
