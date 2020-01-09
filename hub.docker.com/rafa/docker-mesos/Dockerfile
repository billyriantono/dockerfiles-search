FROM ubuntu:14.04
MAINTAINER Rafael Capucho <rafael.capucho@gmail.com>

RUN apt-get -y update && \
apt-get -y install openjdk-7-jdk wget build-essential autoconf libtool curl python-pip python-protobuf python-dev python-boto libcurl4-nss-dev libsasl2-dev maven libapr1-dev libsvn-dev zookeeperd git-core && \
apt-get clean

RUN echo 1 | sudo dd of=/var/lib/zookeeper/myid
RUN sudo mkdir -p /etc/mesos-master && echo in_memory | sudo dd of=/etc/mesos-master/registry

# export environment
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

ENV PATH $PATH:$JAVA_HOME/bin

# include libmesos on library path
ENV LD_LIBRARY_PATH /usr/local/lib

# The following code download the last version available (may be unstable)
RUN cd /home && git clone --depth=1 http://git-wip-us.apache.org/repos/asf/mesos.git mesos && cd mesos && ./bootstrap

# The following code download use one specific release
# RUN cd /home && wget https://github.com/apache/mesos/archive/0.24.0.zip && unzip 0.24.0.zip && rm -f 0.24.0.zip && mv mv mesos-* mesos && cd mesos && ./bootstrap

RUN cd /home/mesos && mkdir build && cd build && ../configure && cd /home/mesos/build && make -j 1 V=0

RUN cd /home/mesos/build && make install

# make sure mesos-executor can find libmesos
RUN ldconfig

