FROM dockerimages/java
MAINTAINER Frank Lemanschik @ Direkt SPEED Europe <frank@dspeed.eu>

# ADD http://downloads.mesosphere.io/master/debian/7/mesos_0.20.0-1.0.debian75_amd64.deb /tmp/mesos.deb
# RUN dpkg -i /tmp/mesos.deb && rm /tmp/mesos.deb

RUN echo "NOTE: We add Mesos ubuntu repo for trusty run apt update and install it and some dependencys" \
 && echo "deb http://repos.mesosphere.io/ubuntu trusty main" | sudo tee /etc/apt/sources.list.d/mesosphere.list \
 && sudo apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF \
 && apt-get update \
 && apt-get install \
    --fix-missing \
    libsasl2-2 \
    libcurl3 \
    curl \
    wget \
    unzip \
    default-jre-headless \
    python python2.7 python-setuptools python-pip python-protobuf \
    mesos \
 && echo "NOTE: We Overwrite the Init Settings of Mesos" \
 && echo manual > /etc/init/mesos-slave.override \
 && echo manual > /etc/init/mesos-master.override
EXPOSE 5051
EXPOSE 5050
CMD ["/usr/local/sbin/mesos-slave"]
#CMD ["/usr/local/sbin/mesos-master"]
