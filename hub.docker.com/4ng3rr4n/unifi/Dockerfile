FROM debian:jessie

# Set environment variables
# UniFi version tracking
ENV DEBIAN_FRONTEND noninteractive
ENV UNIFI_VERSION 5.4.15

# Add repository keys, non-default sources, update apt
# Install dependencies and mongodb, download UniFi .deb, install it and remove .deb
# Clean after apt to reduce image size
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
 echo "deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen" \
   | tee -a /etc/apt/sources.list.d/mongodb.list && \
 echo "deb http://ftp.debian.org/debian jessie-backports main" \
   | tee -a /etc/apt/sources.list.d/jessie-backports.list && \
 apt-get update -q && \
 apt-get --no-install-recommends -y install \
   supervisor \
   binutils \
   wget && \
 apt-get -t jessie-backports --no-install-recommends -y install \
   openjdk-8-jre-headless && \
 apt-get --no-install-recommends -y install \
   jsvc \
   mongodb-server && \
 wget -nv https://www.ubnt.com/downloads/unifi/$UNIFI_VERSION/unifi_sysvinit_all.deb && \
 dpkg --install unifi_sysvinit_all.deb && \
 rm unifi_sysvinit_all.deb && \
 apt-get -y autoremove wget && \
 apt-get -q clean && \
 rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*.deb /tmp/* /var/tmp/* 

# Expose needed ports
# 3478/udp - UDP port used for STUN
# 5656-5699/udp - ports for AP-EDU broadcasts
# 6789/tcp - port used for throughput measurement
# 8080/tcp - port for UniFi devices to inform controller
# 8443/tcp - port for controller web GUI / API
# 8843/tcp - port for HTTPS portal redirect
# 8880/tcp - port for HTTP portal redirect
# 10001/udp - L2 discovery
# More info availaible at https://help.ubnt.com/hc/en-us/articles/218506997-UniFi-Ports-Used
EXPOSE 3478/udp 6789/tcp 8080/tcp 8443/tcp 8843/tcp 8880/tcp 10001/udp

# Set internal volume
VOLUME ["/usr/lib/unifi/data", "/usr/lib/unifi/logs"]

# Set working directory
WORKDIR /usr/lib/unifi

# Add supervisor config
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]