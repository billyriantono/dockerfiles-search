# customized buntu image

FROM ubuntu:14.04
MAINTAINER Zhiheng NIU <niuzhiheng@gmail.com>

RUN echo 'deb http://mirror.nus.edu.sg/ubuntu trusty main universe' > /etc/apt/sources.list

# this forces dpkg not to call sync() after package extraction and speeds up install
RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup

# we don't need and apt cache in a container
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

RUN apt-get update && apt-get install -y \
 dnsmasq
