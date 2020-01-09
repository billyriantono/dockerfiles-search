FROM ubuntu:xenial

RUN apt-get update && apt-get install -y wget libcurl3-gnutls libgeoip1 psmisc libxml2 \
    dnsutils \
    mc \
    && echo deb http://apt.bitninja.io/debian/ bitninja non-free >> /etc/apt/sources.list.d/bitninja.list \
    && wget -O- http://apt.bitninja.io/7F8B47DC.gpg | apt-key add - \
    && apt-get update \
    && apt-get install -y bitninja bitninja-ssl-termination bitninja-waf inotify-tools \
    && mkdir /MalwareDetection \
    && rm -rf /var/lib/apt/lists/*

COPY ./docker-entrypoint.sh /
RUN chmod 700 /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["bitninja"]

