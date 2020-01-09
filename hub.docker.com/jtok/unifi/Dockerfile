### Dockerfile for unifi
FROM phusion/baseimage:0.10.0
LABEL maintainer="jtok"

# Set argument variables
ARG DEBIAN_FRONTEND="noninteractive"

# Set environment variables
ENV UNIFI_VERSION="5.7.20"
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Use Phusion's init system.
CMD ["/sbin/my_init"]

# Configure user nobody to match unRAID's settings
RUN \
    usermod -u 99 nobody && \
    usermod -g 100 nobody && \
    usermod -d /home nobody && \
    chown -R nobody:users /home

# Install sudo
RUN apt-get update -q \
    && apt-get install -y sudo \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install mongodb, java, and unifi controller
RUN \
    apt-key adv --keyserver keyserver.ubuntu.com --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5 \
    && echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.6.list \
    && apt-get update -q \
    && apt-get -y install --no-install-recommends \
        mongodb-org-server \
        openjdk-8-jre-headless \
        binutils \
        jsvc \
    && curl -L -o /tmp/unifi_sysvinit_all.deb "http://dl.ubnt.com/unifi/${UNIFI_VERSION}/unifi_sysvinit_all.deb" \
    && dpkg -i /tmp/unifi_sysvinit_all.deb \
    && apt-get -q clean && apt-get -y autoremove && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /tmp/* /var/tmp/*


COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod +x /sbin/entrypoint.sh

# Expose ports AP discovery, STUN, UniFi mobile speedtest, device communication, shutdown/management, https, http
EXPOSE 10001/udp 3478/udp 6789/tcp 8080/tcp 8081/tcp 8443/tcp 8843/tcp 8880/tcp

WORKDIR /usr/lib/unifi

VOLUME ["/config"]

HEALTHCHECK CMD curl --fail https://localhost:8443/ || exit 1

ENTRYPOINT [ "/sbin/entrypoint.sh" ]
