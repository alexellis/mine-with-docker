mine-with-docker
=================

This repository contains Docker images and Dockerfiles that let you get from zero to mining in around 5 minutes on any Linux host anywhere.

CPU mining can be profitable using algorithmns like: Cryptonight, Hodl or Equihash. Find out more about [profitability here](https://www.nicehash.com/profitability-calculator).

Disclaimer: this software is provided with no warranty. Use at your own risk. If you plan to mine on a cloud check the terms and conditions before you start. The same applies if you are using private equipment or an on-site datacenter for mining.

> Tip: Mining will use all the CPU resources available on the machine so do not run it where you have critical applications.

## How does it work?

Instead of mining BitCoin or other currencies on your own this software works by connecting your CPU / GPU to a mining pool. You get paid for the shares your computer makes towards solving a block. The NiceHash mining pool used in this example lets you mine using two dozen different algorithms and can tell you what is most profitable for your hardware.

* What should I mine?

At time of writing a quad-core Intel CPU would be best mining Cryptonight, Hodl or Equihash.

* What is the barrier to entry?

There barrier to entry is super low - you just have to have a Linux system connected to the Internet where you can install Docker. That's it. You then run the image I've already built and start accruing Bitcoins.

* Can I use my Raspberry Pi cluster?

Absolutely not.. there is no point even going there and believe me I've tried. You may find an obscure "alt coin" that can be mined with a Raspberry Pi but getting the money out of an obscure mining pool or exchange is more trouble than it's worth.

* Is it profitable?

It can be profitable depending on your hardware and electricity costs. If you have a single node and can get paid 2-5USD / day for instance then that's going to equate to 60-150 USD / month. Now if you actually have 20 or 50 nodes you can apply a multiplier.

> Tip: If you have credits with a cloud provider or are using the Spot Instance market then this could be a way for you to generate some coin at a low cost.

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
  -a cryptonight \
  -o stratum+tcp://cryptonight.eu.nicehash.com:3355 \
  -u 1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o.cloud1
```

* Replace "1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o" with your wallet ID and "cloud1" with the name of the host you're mining on if you want to track it.

* If you live outside the EU then find your [nearest Stratum proxy server from Nicehash](https://www.nicehash.com/asic-mining) and replace the `eu` URL with your nearest location.

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

Can I ask you a question? You can follow me on Twitter [@alexellisuk](https://twitter.com/alexellisuk) or make a donation with Bitcoin or Ethereum below:

Donate via BTC: 1M2KME8VBx24RsU3Ed2dEkF9EFghn3jR2o

Donate via ETH: 0x0D0c7108AD4180486E03B4Fc44AD794a209eCb37

## License

MIT

Copyright Alex Ellis 2017
