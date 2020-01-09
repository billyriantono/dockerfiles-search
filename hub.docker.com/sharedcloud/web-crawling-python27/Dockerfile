FROM ubuntu:18.10
LABEL maintainer "Sharedcloud <admin@sharedcloud.io>"

RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip

RUN pip install requests bs4 lxml Scrapy

RUN mkdir -p /data

WORKDIR /data

CMD /bin/bash && python3.6 -c "$CODE"
