FROM ubuntu:xenial

COPY ./scrapyd.conf /etc/scrapyd/
RUN mkdir -p /var/lib/scrapyd

RUN apt-get update && \
    apt-get -y install \
        cron \
        build-essential \
        libssl-dev \
        libffi-dev \
        libxml2-dev \
        libxslt1.1 \
        libxslt1-dev \
        libtool \
        libxml2-dev \
        python3-pip \
        libxml2 \
        vim-tiny \
        && \
    pip3 install Scrapy scrapyd && \
    apt-get clean



EXPOSE 6800

CMD ["scrapyd"]
