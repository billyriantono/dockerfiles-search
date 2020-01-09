FROM alpine:3.4
MAINTAINER Stephen Bunn "scbunn@sbunn.org"

COPY docker-entrypoint.sh /
RUN apk update &&\
    apk add --no-cache su-exec &&\
    apk add --no-cache squid=3.5.20-r0 && \
    mkdir -p /var/cache/squid &&\
    chmod +x /docker-entrypoint.sh
COPY conf/squid.conf /etc/squid/squid.conf
ENTRYPOINT [ "/docker-entrypoint.sh" ]
CMD [ "squid" ]
EXPOSE 3128 3130
