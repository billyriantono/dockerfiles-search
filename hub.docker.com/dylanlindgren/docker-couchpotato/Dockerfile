FROM debian:wheezy

MAINTAINER “Dylan Lindgren” <dylan.lindgren@gmail.com>

WORKDIR /var/lib

RUN echo 'deb ftp://ftp.us.debian.org/debian/ wheezy non-free' >> /etc/apt/sources.list.d/wheezy.non-free.list
RUN echo 'deb http://security.debian.org/ wheezy/updates non-free' >> /etc/apt/sources.list.d/wheezy.non-free.list

# Install CouchPotatoServer prerequisites
RUN apt-get update -y && \
    apt-get install -y \
    git \
    unrar \
    python2.7 && \
    rm -rf /var/lib/apt/lists/*

# Install CouchPotatoServer
RUN git clone https://github.com/RuudBurger/CouchPotatoServer.git

# Add the startup scripts
ADD config/cp-start.sh /opt/bin/cp-start.sh
RUN adduser -c "CouchPotato User" couchpotato && \
    mkdir -p /data/couchpotato && \
    chmod u=rwx /opt/bin/cp-start.sh && \
    chown -R couchpotato:couchpotato /var/lib/CouchPotatoServer /data/couchpotato /opt/bin/cp-start.sh
VOLUME ["/data/couchpotato"]

EXPOSE 5050

USER couchpotato

ENTRYPOINT ["/opt/bin/cp-start.sh"]
