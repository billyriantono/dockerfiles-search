FROM debian:buster-slim

LABEL maintainer="Martin Etmajer <metmajer@getcloudnative.io>"

RUN apt-get update && \
    apt-get -y install python2.7 python-pip libmariadbclient-dev && \
    rm -rf /var/lib/apt/lists/* /tmp/*

ADD ./ /getcloudn8tv-tweet-bot
WORKDIR /getcloudn8tv-tweet-bot
RUN pip install -r requirements.txt

CMD /bin/bash
