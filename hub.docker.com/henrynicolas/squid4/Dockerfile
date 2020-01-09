FROM alpine:latest

RUN apk add --no-cache squid py-pip \
    && pip install --no-input j2cli


# Configuration environment
ENV MITM_CERT= \
    ICAP_HOST= \
    LOCALNET_V4= \ 
    LOCALNET_V6= \ 
    DNS_NAMESERVER= \
    VISIBLE_HOSTNAME=docker-squid4 \
    MAX_CACHE_SIZE=40000 \
    MAX_OBJECT_SIZE="128 MB" \
    CACHE_MEM="2 GB" 

# Entrypoint script and jinja templates
COPY squid.conf.j2 /root/squid.conf.j2
COPY docker-entrypoint.sh /usr/local/bin
RUN ln -s usr/local/bin/docker-entrypoint.sh / # backwards compat
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3128
CMD ["squid", "-N"]
