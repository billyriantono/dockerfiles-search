# Dockerfile for builing a Nexus Maven Repository.

# ubuntu 14.04 with oracle java 1.7.0_67
FROM tifayuki/java:7

MAINTAINER Kris Davison

# Install utilities needed to download and unzip nexus
RUN apt-get update && \
    apt-get install -y unzip wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Download and unzip nexus
RUN wget http://download.sonatype.com/nexus/oss/nexus-2.11.1-01-bundle.zip && \
    unzip nexus-2.11.1-01-bundle.zip && \
    ln -s nexus-2.11.1-01 nexus && \
    rm -rf nexus-2.11.1-01-bundle.zip

# change config to allow nexus to run as root
RUN sed -i 's/#RUN_AS_USER=/RUN_AS_USER=root/g' /nexus/bin/nexus

EXPOSE 8081

VOLUME /sonatype-work/nexus/conf
VOLUME /sonatype-work/nexus/storage

CMD /nexus/bin/nexus console

