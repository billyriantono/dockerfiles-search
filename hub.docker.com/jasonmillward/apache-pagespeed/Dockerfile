FROM ubuntu:19.04

ENV TINI_VERSION v0.18.0

RUN apt-get update && apt-get install apache2 wget -y && rm -rf /var/lib/apt/lists/*
RUN wget https://dl-ssl.google.com/dl/linux/direct/mod-pagespeed-stable_current_amd64.deb
RUN dpkg -i mod-pagespeed-*.deb && apt-get -fy install --no-install-recommends && rm -rf /var/lib/apt/lists/* && rm mod-pagespeed-*.deb  

RUN ln -sf /proc/self/fd/1 /var/log/apache2/access.log && \
    ln -sf /proc/self/fd/1 /var/log/apache2/error.log

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

COPY rootfs /

EXPOSE 80 443

CMD [ "/run.sh" ]