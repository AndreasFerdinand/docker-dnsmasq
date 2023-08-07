# docker-dnsmasq
dnsmasq in docker

# Build docker image

```bash
sudo docker build --tag "andreasferdinand/dnsmasq:latest" .
```

## Create configuration

```bash
sudo mkdir /etc/dnsmasq/
sudo touch 0.base.conf
sudo touch 1.hosts.conf
```

### Content of `0.base.conf`
This file contains base configuration of dnsmasq. Is uses google dns servers (`8.8.8.8`,`8.8.4.4`).
```
# 0.base.conf

domain-needed
bogus-priv
no-hosts
keep-in-foreground
no-resolv
expand-hosts
server=8.8.8.8
server=8.8.4.4
cache-size=1000
```

### Content of `1.hosts.conf`
This file contains the dns entries.

```
# 1.hosts.conf

local=/localnet/
local=/fritz.box/

address=/my.additionalhost.net/192.168.1.52
```

## Run docker container

```sh
sudo docker run -d \
  --name dnsmasq \
  -p 53:53/udp \
  --volume /etc/dnsmasq:/etc/dnsmasq \
  --restart unless-stopped \
  andreasferdinand/dnsmasq:latest 
```
