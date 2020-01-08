FROM jenkins:2.0

MAINTAINER Bjoern Heneka <bheneka@codebee.de>

USER root

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
    echo "deb http://repos.mesosphere.io/debian jessie main" | \
      tee /etc/apt/sources.list.d/mesosphere.list

RUN apt-get update && \
    apt-get install -y mesos vim && \
    apt-get clean && \
    rm -fr /var/lib/apt/lists/*

USER ${user}