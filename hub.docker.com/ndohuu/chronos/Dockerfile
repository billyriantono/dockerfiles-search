FROM ubuntu:14.04

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
echo deb http://repos.mesosphere.io/ubuntu trusty main > /etc/apt/sources.list.d/mesosphere.list && \
apt-get update && \
apt-get -y install chronos=2.4.0-0.1.20151007110204.ubuntu1404 mesos=0.26.0-0.2.145.ubuntu1404

COPY entrypoint.sh /

RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]