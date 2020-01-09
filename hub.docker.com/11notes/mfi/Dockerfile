# :: Header
FROM ubuntu:14.04
ENV mfiVersion=2.1.11-4990
ARG DEBIAN_FRONTEND=noninteractive

# :: Run
USER root
RUN apt-get update \
    && apt-get install apt-transport-https apt-utils wget curl -y

RUN mkdir -p /var/log/mfi \
    && ln -sf /dev/stdout /var/log/mfi/mongod.log

RUN echo "deb http://dl.ubnt.com/mfi/distros/deb/ubuntu ubuntu ubiquiti" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50

RUN apt-get update \
    && apt-get install -y openjdk-7-jre-headless jsvc libcommons-daemon-java libboost-filesystem1.54.0 libboost-program-options1.54.0 \
    libboost-system1.54.0 libboost-thread1.54.0 libgoogle-perftools4 libpcap0.8 libpcrecpp0 libsnappy1 libtcmalloc-minimal4 libunwind8 libv8-3.14.5 \
    && wget -O /tmp/mongodb-clients.deb http://archive.ubuntu.com/ubuntu/pool/universe/m/mongodb/mongodb-clients_2.4.9-1ubuntu2_amd64.deb && dpkg -i /tmp/mongodb-clients.deb \
    && wget -O /tmp/mongodb-server.deb http://archive.ubuntu.com/ubuntu/pool/universe/m/mongodb/mongodb-server_2.4.9-1ubuntu2_amd64.deb && dpkg -i /tmp/mongodb-server.deb

RUN apt-get install -y mfi=${mfiVersion}

ADD ./source/healthcheck.sh /usr/local/bin/healthcheck.sh
RUN chmod +x /usr/local/bin/healthcheck.sh

# :: docker -u 1000:1000 (no root initiative)
RUN addgroup --gid 1000 mfi \
    && useradd --uid 1000 -s /sbin/nologin mfi -g mfi \
    && chown -R mfi:mfi \
    /usr/lib/jvm \
    /usr/share/java \
    /var/lib/mfi \
    /var/log/mfi \
    /usr/lib/mfi \
    /usr/bin/java

# :: Volumes
VOLUME ["/var/lib/mfi"]

# :: Monitor
HEALTHCHECK CMD /usr/local/bin/healthcheck.sh || exit 1

# :: Start
USER mfi
ENTRYPOINT ["/usr/bin/java", "-Xmx1024M", "-jar", "/usr/lib/mfi/lib/ace.jar"]
CMD ["start"]