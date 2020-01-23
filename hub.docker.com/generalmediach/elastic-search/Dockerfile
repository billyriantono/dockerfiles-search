FROM ubuntu:14.04

ENV DEBIAN_FRONTEND=noninteractive

RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000


# ELASTICSEARCH <= 1.7.2 is required because of elastica-bundle v3.2.1

RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4 && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
    echo "deb http://packages.elastic.co/elasticsearch/1.7/debian stable main" > etc/apt/sources.list.d/elastic.list && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > etc/apt/sources.list.d/java.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends elasticsearch software-properties-common  && \
    (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections) && \
    apt-get install --no-install-recommends -y oracle-java8-installer && \
    rm -rf /var/cache/oracle-jdk8-installer && \
    echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-8-oracle/jre/lib/security/java.security && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


WORKDIR /usr/share/elasticsearch

COPY elasticsearch/logging.yml /usr/share/elasticsearch/config/
COPY elasticsearch/elasticsearch.yml /usr/share/elasticsearch/config/

RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head

# just ".../plugin install cloud-aws" on  2.x  https://devhub.io/zh/repos/elastic-elasticsearch-cloud-aws

RUN /usr/share/elasticsearch/bin/plugin install elasticsearch/elasticsearch-cloud-aws/2.7.1

RUN mkdir -p /data && chown elasticsearch:elasticsearch -R /data

RUN rm -rf /data/plugins && ln -s /usr/share/elasticsearch/plugins /data/plugins

RUN set -ex && for path in /data/log /data/plugins /data/data config config/scripts; do \
        mkdir -p "$path"; \
        chown -R elasticsearch:elasticsearch "$path"; \
    done



USER elasticsearch
ENV PATH=$PATH:/usr/share/elasticsearch/bin

CMD ["elasticsearch"]
EXPOSE 9200 9300
