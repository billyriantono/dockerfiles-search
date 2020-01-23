FROM phusion/baseimage:0.9.22

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Tell debconf to run in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive


RUN apt-get  update && apt-get install -y unzip wget default-jre-headless nmap iputils-ping nano vim
RUN export JAVA_HOME=/usr/lib/jvm/default-java

RUN wget https://nexus.opendaylight.org/content/repositories/public/org/opendaylight/integration/distribution-karaf/0.6.0-Carbon/distribution-karaf-0.6.0-Carbon.zip
RUN unzip distribution-karaf-0.6.0-Carbon.zip
RUN rm -rf distribution-karaf-0.6.0-Carbon.zip
WORKDIR distribution-karaf-0.6.0-Carbon
RUN mkdir /scripts
VOLUME /distribution-karaf-0.6.0-Carbon
VOLUME /scripts
WORKDIR /distribution-karaf-0.6.0-Carbon/bin
