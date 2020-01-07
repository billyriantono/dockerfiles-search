FROM elasticsearch:1.6.2
MAINTAINER Teng Fei "i@feit.me"

RUN apt-get update && \
    apt-get install -y --no-install-recommends --force-yes maven openjdk-8-jdk && \
    rm -rf /var/lib/apt/lists/*
ADD https://github.com/medcl/elasticsearch-analysis-ik/archive/v1.2.6.tar.gz /tmp/elasticsearch-analysis-ik.tar.gz
RUN tar -xvf /tmp/elasticsearch-analysis-ik.tar.gz -C /tmp && \
    cd /tmp/elasticsearch-analysis-ik-1.2.6 && \
    mvn package && \
    unzip target/releases/elasticsearch-analysis-ik-1.2.6.zip -d /usr/share/elasticsearch/plugins/ik && \
    cd / && \
    rm -rf /tmp/elasticsearch-analysis-ik*
