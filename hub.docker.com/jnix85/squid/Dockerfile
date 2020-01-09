FROM jnix85/centos:8
LABEL maintainer="jparks@jpconsulted.com"
LABEL version="1.0.0" 

ENV SQUID_CACHE_DIR=/var/spool/squid \
    SQUID_LOG_DIR=/var/log/squid \
    SQUID_USER=squid

RUN dnf makecache && \
    dnf install squid golang git -y && \
    dnf clean all

COPY files/squid.conf /etc/squid/squid.conf
COPY files/storeid.conf /etc/squid/storeid.conf

COPY files/runSquid.sh /runSquid.sh
RUN chmod 755 /runSquid.sh

EXPOSE 3128

ENTRYPOINT ["/runSquid.sh"]
