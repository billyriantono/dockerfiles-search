FROM vrviumichael/ubuntu:16.04

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF \
    && echo "deb http://repos.mesosphere.com/ubuntu xenial main" | tee /etc/apt/sources.list.d/mesosphere.list \
    && apt-get -y update && apt-get -y install mesos \
    && apt-get clean

RUN mkdir -p /export/app \
    && cd /export/app \
    && wget http://downloads.mesosphere.com/marathon/v1.4.7/marathon-1.4.7.tgz \
    && tar xvf marathon-1.4.7.tgz \
    && rm -rvf marathon-1.4.7.tgz

ENTRYPOINT ["/export/app/marathon-1.4.7/bin/start"]
