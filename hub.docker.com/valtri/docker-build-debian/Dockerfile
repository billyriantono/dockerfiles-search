FROM debian:stretch
MAINTAINER František Dvořák <valtri@civ.zcu.cz>

RUN apt-get update \
&& apt-get install -y bzip2 less mc screen ssh pbzip2 pigz vim

RUN apt-get update \
&& apt-get install -y build-essential debhelper git quilt lintian

RUN ln -s /usr/share/mc/bin/mc.sh /etc/profile.d/
RUN ln -s /usr/share/mc/bin/mc.csh /etc/profile.d/

RUN apt-get clean \
&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT /bin/bash -l
