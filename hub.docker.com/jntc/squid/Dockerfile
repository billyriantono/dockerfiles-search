FROM ubuntu:14.04.3
MAINTAINER james.turner@yellow.co.nz

ENV SQUID_CACHE_DIR=/var/spool/squid3 \
    SQUID_LOG_DIR=/var/log/squid3 \
    SQUID_USER=proxy
RUN sed -i "s/http:\/\/archive./http:\/\/nz.archive./g" /etc/apt/sources.list
RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y squid3

#COPY squid.conf /etc/squid3/squid.conf

# COPY entrypoint.sh /sbin/entrypoint.sh
# RUN chmod 755 /sbin/entrypoint.sh
#
# RUN mkdir -p ${SQUID_LOG_DIR} \
#    chmod -R 755 ${SQUID_LOG_DIR} \
#    chown -R ${SQUID_USER}:${SQUID_USER} ${SQUID_LOG_DIR} \
#    mkdir -p ${SQUID_CACHE_DIR} \
#    chown -R ${SQUID_USER}:${SQUID_USER} ${SQUID_CACHE_DIR} \


EXPOSE 3128/tcp
VOLUME ["/etc/squid3"]
ENTRYPOINT ["squid3", "-NYCd 1"]
#ENTRYPOINT ["/sbin/entrypoint.sh"]
