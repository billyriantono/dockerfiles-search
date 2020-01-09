FROM greatbsky/centos7:latest
MAINTAINER architect.bian
LABEL name="kibana" license="MIT" build-date="20190330"

ENV VERSION 6.5.4

RUN cd /data/softs && wget https://artifacts.elastic.co/downloads/kibana/kibana-$VERSION-linux-x86_64.tar.gz && tar -zxf kibana-$VERSION-linux-x86_64.tar.gz && mkdir -p /data/env/elastic/kibana && mv kibana-$VERSION-linux-x86_64/* /data/env/elastic/kibana && rm -rf /data/softs/*

EXPOSE 5601
WORKDIR /data/env/elastic/kibana

CMD ["bin/kibana"]