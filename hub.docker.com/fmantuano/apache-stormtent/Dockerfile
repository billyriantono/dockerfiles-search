FROM java:8-jdk
MAINTAINER Alan Schegrer <flyinprogrammer@gmail.com>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv E56151BF && \
    echo "deb http://repos.mesosphere.com/debian jessie main" > /etc/apt/sources.list.d/mesosphere.list && \
    apt-get -y update && \
    apt-get -y install mesos && \
    rm -rf /var/lib/{apt,dpkg,cache,log}


ENV CP_VERSION=2.4.3 \
    CP_SHA1=2c469a0e79a7ac801f1c032c2515dd0278134790

RUN set -x && \
    curl -fSL "https://github.com/joyent/containerpilot/releases/download/${CP_VERSION}/containerpilot-${CP_VERSION}.tar.gz" -o cp.tar.gz && \
    echo "${CP_SHA1}  ./cp.tar.gz" | sha1sum -c - && \
    tar -xzvf cp.tar.gz && \
    mv ./containerpilot /bin/ && \
    chmod +x /bin/containerpilot && \
    rm cp.tar.gz && \
    containerpilot -version
