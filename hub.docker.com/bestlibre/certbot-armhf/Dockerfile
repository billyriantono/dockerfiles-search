FROM bestlibre/tiny-armhf
# Default configuration
RUN [ "cross-build-start" ]

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y -t jessie-backports certbot && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /etc/apt/sources.list.d/jessie-backports.list

RUN [ "cross-build-end" ]

ENTRYPOINT ["/tini", "--"]

CMD ["certbot"]


