# Docker MongoDb

Docker Image for MongoDb based on airdock/base:latest

Purpose of this image is:

- provide a mongodb server
- based on airdock/base:latest

> Name: airdock/mongodb

***Dependency***: airdock/base:latest

***Few links***:

- [Dockerizing MongoDB](https://docs.docker.com/examples/mongodb/)
- [Iron Pinguin dockerfile](https://github.com/ironpinguin/docker-mongodb/blob/master/Dockerfile)
- [Sharded Cluster](https://sebastianvoss.com/docker-mongodb-sharded-cluster.html)

# Usage

You should have already install [Docker](https://www.docker.com/) and [Fig](http://www.fig.sh/) for more complex usage.
Download [automated build](https://registry.hub.docker.com/u/airdock/) from public [Docker Hub Registry](https://registry.hub.docker.com/):
`docker search airdock`

Execute:

	'docker run -t -i -p 27017:27017 --name mongodb airdock/mongodb '


## With a persistent storage


	'docker run -d -p 27017:27017 -v /var/lib/mongodb:/var/lib/mongodb --name mongodb airdock/mongodb'

Take care about your permission on host folder named '/var/lib/mongodb'.

The user mongodb (uid 4203) in your container should be known into your host.
See [How Managing user in docker container](https://github.com/airdock-io/docker-base/blob/master/README.md#how-managing-user-in-docker-container) and  [Common User List](https://github.com/airdock-io/docker-base/blob/master/CommonUserList.md).

So you should create an user with this uid:gid:

```
  sudo groupadd mongodb -g 4203
  sudo useradd -u 4203  --no-create-home --system --no-user-group mongodb
  sudo usermod -g mongodb mongodb
```

And then set owner and permissions on your host directory:

```
	chown -R mongodb:mongodb /var/lib/mongodb
```




### Notes:

- configuration file: /etc/mongod.conf
- data file: /var/lib/mongodb


TODO add sharded cluster DockerFig sample

# Change Log

## latest (current)

- add mongodb 2.6.7
- add variable MONGODB_VERSION
- Listen on all address
- Output log to stdout
- Add volume to data (/var/lib/mongodb) and log folder (/var/log/mongodb)
- launch mongod with mongodb:mongodb

# Build

Alternatively, you can build an image from [Dockerfile](https://github.com/airdock-io/docker-nginx).
Install "make" utility, and execute: `make build`

In Makefile, you could retrieve this *variables*:

- NAME: declare a full image name (aka airdock/mongodb)
- VERSION: declare image version

And *tasks*:

- all: alias to 'build'
- clean: remove all container which depends on this image, and remove image previously builded
- build: clean and build the current version
- tag_latest: tag current version with ":latest"
- release: build and execute tag_latest, push image onto registry, and tag git repository
- debug: launch default command with builded image in interactive mode
- run: run image as daemon and print IP address.



# License

```
 Copyright (c) 1998, 1999, 2000 Thai Open Source Software Center Ltd

 Permission is hereby granted, free of charge, to any person obtaining
 a copy of this software and associated documentation files (the
 "Software"), to deal in the Software without restriction, including
 without limitation the rights to use, copy, modify, merge, publish,
 distribute, sublicense, and/or sell copies of the Software, and to
 permit persons to whom the Software is furnished to do so, subject to
 the following conditions:

 The above copyright notice and this permission notice shall be included
 in all copies or substantial portions of the Software.

 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
 EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
 MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
 IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
 CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
 TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
 SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
