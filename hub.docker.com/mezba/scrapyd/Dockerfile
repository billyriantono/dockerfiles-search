FROM ubuntu:18.04

RUN set -xe \
    && apt-get update \
    && apt-get install -y python3 \
                          python3-dev \
                          python3-pip \
                          libxml2-dev \
                          libxslt1-dev \
                          zlib1g-dev \
                          libffi-dev \
                          libssl-dev \
    && pip3 install scrapyd==1.2.1 \
    && rm -rf /var/lib/apt/lists/*

COPY ./scrapyd.conf /etc/scrapyd/
VOLUME /etc/scrapyd/ /var/lib/scrapyd/

EXPOSE 6800
CMD ["scrapyd", "--pidfile="]
