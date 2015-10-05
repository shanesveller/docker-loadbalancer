## Installing Prerequisites

```shell
brew update
brew install caskroom/cask/brew-cask
brew cask install dockertoolbox
brew install direnv
```

## Readying Docker

```shell
docker-machine create -d virtualbox dev
docker-machine upgrade dev
docker-machine start up
eval $(docker-machine env dev)
docker version
docker ps
```

## Boot A Variant

From within the subdirectory:

```shell
docker-compose pull && docker-compose build
docker-compose up
```

## Inspection
### Consul Registered Services

```shell
curl http://`boot2docker ip 2>/dev/null`:8500/v1/catalog/services
```

### Visit LB In Default Browser

```shell
open "http://$(docker-machine ip dev)/"
```

## Adding/Removing Backend Containers

```shell
docker-compose scale app=4
docker-compose scale app=1
```

## Gotchas
* Auto-detected advertise IP for Consul-in-Docker on Boot2docker is not routable from the Nginx container. Use the following to look up the IP to set for `-advertise`:

```shell
docker-machine ssh dev "ifconfig eth0 | grep 'inet addr'"
```
